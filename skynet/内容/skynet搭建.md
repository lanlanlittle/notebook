## skynet搭建

github地址：https://github.com/cloudwu/skynet

windows下比较麻烦，需要安装虚拟机

1、git代码

```
git clone https://github.com/cloudwu/skynet.git
cd skynet
make 'PLATFORM'  # PLATFORM can be linux, macosx, freebsd now
```

2、测试skynet

```
./skynet examples/config	# Launch first skynet node  (Gate server) and a skynet-master (see config for standalone option)
./3rd/lua/lua examples/client.lua 	# Launch a client, and try to input hello.
```

3、最简单的helloworld

文件清单

```
skynet
+--skynet_demo
	+--helloword
		|--config
		|--main.lua
```

config文件

```
skynetroot = "../skynet/" 
projroot = "./helloworld/"

thread = 8
logger = nil
harbor = 0
start = "main"	-- main script
bootstrap = "snlua bootstrap"	-- The service for bootstrap

snax = nil
cpath = skynetroot .. "cservice/?.so"

lualoader = skynetroot .. "lualib/loader.lua"
luaservice = skynetroot .. "service/?.lua;" .. projroot .. "?.lua"
lua_path = skynetroot .. "lualib/?.lua"
lua_cpath = skynetroot .. "luaclib/?.so"
```

main.lua文件

```
local skynet = require "skynet"

skynet.start(function()
	skynet.error("hello world!")
	skynet.exit()
end)
```

执行：

```
cd skynet_demo
../skynet/skynet ./helloworld/config
```

配置说明

这些配置项可以通过 `skynet.getenv` 获取。

- **thread** 启动多少个工作线程。通常不要将它配置超过你实际拥有的 CPU 核心数。

- **logger** 它决定了 skynet 内建的 `skynet_error` 这个 C API 将信息输出到什么文件中。如果 logger 配置为 nil ，将输出到标准输出。你可以配置一个文件名来将信息记录在特定文件中。

- **harbor** 可以是 1-255 间的任意整数。一个 skynet 网络最多支持 255 个节点。每个节点有必须有一个唯一的编号。如果 harbor 为 0 ，skynet 工作在单节点模式下。此时 **master** 和 **address** 以及 **standalone** 都不必设置。

- **start** 这是 bootstrap 最后一个环节将启动的 lua 服务，也就是你定制的 skynet 节点的主程序。默认为 main ，即启动 main.lua 这个脚本。这个 lua 服务的路径由下面的 **luaservice** 指定。

- **bootstrap** skynet 启动的第一个服务以及其启动参数。默认配置为 snlua bootstrap ，即启动一个名为 bootstrap 的 lua 服务。通常指的是 service/bootstrap.lua 这段代码。

  

- **snax** 用 snax 框架编写的服务的查找路径。

- **cpath** 用 C 编写的服务模块的位置，通常指 cservice 下那些 .so 文件。如果你的系统的动态库不是以 .so 为后缀，需要做相应的修改。这个路径可以配置多项，以 ; 分割。

  

- **lualoader** 用哪一段 lua 代码加载 lua 服务。通常配置为 lualib/loader.lua ，再由这段代码解析服务名称，进一步加载 lua 代码。snlua 会将下面几个配置项取出，放在初始化好的 lua 虚拟机的全局变量中。具体可参考实现。

- **luaservice** lua 服务代码所在的位置。可以配置多项，以 ; 分割。 如果在创建 lua 服务时，以一个目录而不是单个文件提供，最终找到的路径还会被添加到 package.path 中。比如，在编写 lua 服务时，有时候会希望把该服务用到的库也放到同一个目录下。

- **lua_path** 将添加到 package.path 中的路径，供 require 调用。

- **lua_cpath** 将添加到 package.cpath 中的路径，供 require 调用。

更多配置请看官网https://github.com/cloudwu/skynet/wiki/Config