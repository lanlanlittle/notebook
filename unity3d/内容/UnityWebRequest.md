





请求头添加：

1、非断点续传

2、断点续传

​	请求头添加 **Range**

​	服务器支持且匹配 响应码206，回应**Content-Range**响应头；否则响应码200

> **HTTP/1.1 200 Ok（不使用断点续传方式）** 
> **HTTP/1.1 206 Partial Content（使用断点续传方式）**



http断点续传-https://www.cnblogs.com/songsu/p/11770746.html

http断点续传-https://www.cnblogs.com/findumars/p/5745345.html

If-Range-https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Range

http条件请求-https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Conditional_requests

curl-https://catonmat.net/cookbooks/curl

大部分不支持If-Range(似乎都支持If-Match，猜测可能原因是If-Range的传值为etag|date，If-Match 传入的是etag，可以作为强制验证)-https://blog.csdn.net/weixin_34190136/article/details/89649390

1KB=1000B 1KiB=1024B-https://www.zhihu.com/question/324130684

容量硬件厂商标志和操作系统算法https://zhidao.baidu.com/question/1901322086709279500.html



curl -v -i -H 'Range: bytes=200-400' -H 'If-Range: "C28387D730B817BC82C33229DCB3C14D"' http://bowarrow-d-test.oss-cn-hangzhou.aliyuncs.com/Test/1.png