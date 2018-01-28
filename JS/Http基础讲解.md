

## http协议

> http(超文本传输协议)是一个基于`TCP/IP`通信协议来传递数据，它允许将超文本标记语言(HTML)文档从Web服务器传送到客户端的浏览器。

### 工作原理

http协议工作于`CS`架构上。浏览器作为客户端通过`URL`向`服务端`(Web服务器)发送所有请求。

### 常见请求方法

`POST`、`DELETE`、`PUT`、`GET`；一般对应着对资源的 `增删改查` 4 个操作。

### GET 与 POST的区别

- 参数传递方式不同
  - GET参数会放在`URL`之后，以`？`分割，参数之间以`&`相连。  
  - POST参数放在请求`body`中。  
- 数据容量不同
  - GET 提交的数据大小有限制（因为浏览器对 URL 的长度有限制）
  - POST 方法提交的数据没有限制。
- 安全性能不同
  - GET方式参数直接显示在URL中，因此安全性更低


### http常见状态码

* 200 : 请求成功
* 301 : 资源(网页等)被永久转移到其他 URL
* 404 : 请求的资源(网页等)不存在
* 500 : 内部服务错误

## https协议

https协议是由`SSL` + `http`协议构建的可加密传输、身份认证的网络协议，比http协议安全。  
主要作用可以分为两种：一种是建立一个信息安全通道，来保证数据传输的安全；另一种就是确认网站的真实性。

## headers

> Headers 是 http 请求和相应的核心，它承载了关于用户端浏览器，请求页面，伺服器等相关的资讯。

```
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding:gzip, deflate, br
Accept-Language:zh-CN,zh;q=0.9,en;q=0.8
Cache-Control:max-age=0
Connection:keep-alive
Host:localhost:3990
If-None-Match:W/"16a-COI6vpxK/hNny4EVpoF/SrJouy8"
Referer:http://localhost:3990/
Upgrade-Insecure-Requests:1
User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36
```

* `Accept`: 定义浏览器可以接受的媒体类型，例如：`Accept: text/html`表示接受的媒体类型是`html`文档。
* `Accept-Encoding`: 浏览器接收的编码方法。
* `Accept-Language`: 浏览器接受的语言。
* `Connection`: `keep-alive`当一个网页打开完成后，客户端和服务器之间用于传输 http 数据的 TCP 连接不会关闭。
* `Host`: (发送请求时，该报头域是必须的)请求报头域用于指定被请求资源的Internet主机和端口号，它通常从HTTP-URL中提取出来的。
* `Referer`: 定义服务器我是从哪个页面链接过来的。
* `User-Agent`: 客户端使用的操作系统和浏览器的名称和版本。
* `Cache-Control`: 网页的缓存控制是由 http 头中的“Cache-control”来实现的。
* `Cookie`: 存储一些用户信息以便让服务器辨别用户身份的。
* `If-Modified-Since`: 浏览器缓存时间对比。

## response

响应分为`响应头`和`响应正文`两个部分。

### 响应头

- `Server`: 服务器名字
- `Date`: 当前的GMT时间
- `Content-Type`: MIME类型
- `Content-Length`: 内容长度
- `Connection`: 是否需要持久连接
- `Last-Modified`: 文档最后更改时间
- `Expires`: 过期时间
- `Content-Encoding`: 文档编码

### 响应正文

响应正文就是服务器返回的数据。
