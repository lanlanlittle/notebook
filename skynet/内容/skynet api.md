[TOC]

# skynet api

##### skynet.start(start_func)

用 func 函数初始化服务，并将消息处理函数注册到 C 层，让该服务可以工作。

- 初始化
- 注册消息处理函数



##### skynet.uniqueservice

```lua
skynet.uniqueservice(global, ...)
默认不跨节点
示例：
	skynet.uniqueservice("foobar")
	skynet.uniqueservice(true, "foobar")
```



#### 消息分发

##### skynet.call(addr, typename, ...)

用 type 类型发送一个消息到 addr ，并等待对方的回应。

发送时经过 pack 打包流程，收到回应后，经 unpack 流程。

它会在内部生成一个唯一 session ，并向 address 提起请求，并阻塞等待对 session 的回应（可以不由 address 回应）。**但每次有阻塞 api 调用时，脚本都可能发生重入，这点务必小心**。

- addr：服务数字地址
- typename：消息类别，数字或别名
- ... 消息内容参数

```lua
例： 
local id = skynet.newservice("test")

skynet.call(id, "lua", "print", "call lua 消息")
or
skynet.call(id, skynet.PTYPE_LUA, "print", "call lua 消息")

--消息内容参数2个 "print" "send lua 消息"
```



##### skynet.rawcall(addr, typename, msg, sz)

用 type 类型发送一个已经打包好的消息到 addr ，并等待对方的回应，但不对回应信息解包。

它和 `skynet.call` 功能类似（也是阻塞 API）。但发送时不经过 pack 打包流程，收到回应后，也不走 unpack 流程。

- addr：服务数字地址
- typename：消息类别，数字或别名
- msg：userdata（表示任意存储在变量中的C数据结构）
- sz：消息的长度

```lua
例：
local id = skynet.newservice("test")
local msg, sz = skynet.pack("print", "rawcall lua 消息")
skynet.rawcall(id, "lua", msg, sz)

--传入userdata和size 或 string
```



##### skynet.send(addr, typename, ...)

用 type 类型向 addr 发送一个消息。

它会先经过事先注册的 pack 函数打包 ... 的内容。

`skynet.send` 是一条非阻塞 API ，发送完消息后，coroutine 会继续向下运行，这期间服务不会重入。

- addr：服务数字地址
- typename：消息类别，数字或别名
- ... 消息内容参数

```lua
例：
local id = skynet.newservice("test")
skynet.send(id, "lua", "print", "send lua 消息")

--消息内容参数2个 "print" "send lua 消息"
```



##### skynet.redirect(addr,source,typename,session,...)

伪装成 source 地址，向 addr 发送一个消息。

它和 `skynet.send` 功能类似 （也是非阻塞 API）。但发送时不经过 pack 打包流程，收到回应后，也不走 unpack 流程。

- addr：服务数字地址
- source：消息源
- typename：消息类别，数字或别名
- session：消息标识0
- ... 消息内容参数

```lua
例：
local id = skynet.newservice("test")
local msg, sz = skynet.pack("print", "redirect lua 消息")
skynet.redirect(id, 0, "lua", 0, msg, sz)

--传入userdata和size 或 string
```



**对比**

| skynet.call    | skynet.rawcall   | skynet.send        | skynet.redirect    |
| -------------- | ---------------- | ------------------ | ------------------ |
| 阻塞（可重入） | 阻塞（可重入）   | 非阻塞（不可重入） | 非阻塞（不可重入） |
| 经pack、unpack | 不经pack、unpack | 经pack、unpack     | 不经pack、unpack   |
| 响应           | 响应             | 不响应             | 不响应             |



#### 消息序列化

##### skynet.tostring(msg, sz) 

将一个指针和长度定义的消息包转换成一个字符串。



##### skynet.pack(...) 

用默认的 lua 类型打包一个消息，返回可供内部调用的指针和长度。



##### skynet.packstring(...) 

用默认的 lua 类型打包一个消息，返回一个 lua 字符串。



##### skynet.unpack(msg [, sz]) 

将 pack 或 packstring 打包的消息解包，若没有 sz 则 msg 必须为一个 lua 字符串 。



```
	例：
	print(skynet.tostring(skynet.pack("123", {a=1})))
	等价于
	print(skynet.packstring("123",{a=1}))
```



#### 消息回应

##### skynet.ret(msg, sz) 

将打包好的消息回应给当前任务的请求源头。

同一个消息处理的 coroutine 中只可以被调用一次。



##### skynet.retpack(...)

将消息用 pack 打包，并调用 ret 回应。

```lua
例：
	skynet.retpack("123")
	等价于
	skynet.ret(skynet.pack("123"))
```



##### skynet.response(pack)

生成一个回应函数，用于在将来回应当前任务。当消息不使用默认的 lua 类型时，需提供对应的消息打包函数。

回应的时候已经在别的 coroutine 中了。

```lua
例：
	skynet.dispatch("lua", function ( session, source, cmd, ... )
		print(string.format("收到lua消息:session=%d source=%d cmd=%s", session, source, cmd))
		local f = assert(CMD[cmd])
		local val = f(...)
		local rf = skynet.response(skynet.pack)
		skynet.fork(function ()
			skynet.sleep(100)
			
			local ok = rf("TEST")
			if ok then
				rf(true, val)
			else
				rf(false)
			end
		end)
	end)
```

