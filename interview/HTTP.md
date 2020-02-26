# HTTP

## HTTPS

https是利用ca认证的证书来加密的.

## URI和URL的区别

uri是资源的身份,而url是指向资源的路径.

uri包含这url,url是一种特殊的uri.

## http常见的方法

- get
- post
- put
- head,用于认证uri是否有效,只返回header,不返回body
- delete
- options,用于获取资源支持的方法

## 请求报文

![HTTP/Untitled.png](HTTP/Untitled.png)

## 响应报文

![HTTP/Untitled%201.png](HTTP/Untitled%201.png)

[https](HTTP/https.md)

## 常见状态码

- 200 正确处理
- 204 被处理但是没有资源
- 301 永久重定向
- 302 临时重定向
- 400 参数有无
- 401 需要认证
- 403 禁止访问
- 404 资源不存在
- 500 服务器错误
- 503 服务器繁忙

## 优化

- tcp复用,使用keepalive,让服务器可以复用tcp链接
- 缓存
- 压缩
- ssl加速

## http2特性

- 二进制分帧

    http2采用二进制传输数据,而不是http1.1的文本格式,http2将请求和响应数据分割为帧,传输数据效率更高.各个数据帧可以乱序,通过头部信息拼接.

- 多路复用

    http1.1中,并发请求一般要躲开多个tcp链接,但是每个域名一般会有6-8个限制.http2使用的二进制分帧后,一个域名可以使用一个tcp链接进行并发请求,性能更高.

- 服务器推送

    http1.1只允许客户端对服务端发起请求,http2服务端可以主动向客户端推送数据.

- 头部压缩

    http每次请求都会发送头部信息,携带cookie等数据,头部越来越大.http2使用一种专门的算法HPACK压缩头部信息,减少带宽占用