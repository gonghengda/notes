
网络应用程序，分为前端和后端两个部分。由于前端设备层出不穷，因此，必须有一种统一的机制，方便不同的前端设备与后端进行通信。这导致API构架的流行。  
[RESTful API](https://en.wikipedia.org/wiki/Representational_state_transfer) 是目前比较成熟的一套互联网应用程序的API设计理论。

## REST

REST是所有Web应用都应该遵守的架构设计原则。REST 意思是：资源在网络中以某种形式进行状态转移（英文：Representational State Transfer）  
REST架构设计，遵循的各项标准和准则，就是HTTP协议的表现，换句话说，HTTP协议就是属于REST架构的设计模式。  
面向资源（Resource）是REST最明显的特征，对于同一个资源的一组不同的操作。REST要求，对于每个资源只能执行一组有限的操作。
### API路径

举例来说，有一个API提供动物园 `zoo` 的信息，还包括各种动物 `animals` 和雇员 `employees` 的信息，则它的路径应该设计成下面这样。

```
/v1/zoos

/v1/animals

/v1/employees
```
### 方法

有了资源的URL设计，所有针对资源的操作都是使用HTTP方法指定的，方法有（括号中为对应的`SQL`命令）：

```jsx
- GET   （SELECT）   // 从服务器取出资源（一项或多项）。
- POST  （CREATE）   // 在服务器新建一个资源。
- PUT   （UPDATE）   // 在服务器更新资源（客户端提供改变后的完整资源）。
- PATCH （UPDATE）   // 在服务器更新资源（客户端提供改变的属性）。
- DELETE（DELETE）   // 从服务器删除资源。
- HEAD  （SELECT）   // 获取资源的元数据。
- OPTIONS           // 获取信息，关于资源的哪些属性是客户端可以改变的。
```
下面是一些例子。

```jsx
- GET     /zoos     // 列出所有动物园
- POST    /zoos     // 新建一个动物园
- GET     /zoos/:Id // 获取某个指定动物园的信息
- PUT     /zoos/:Id // 更新某个指定动物园的信息（提供该动物园的全部信息）
- PATCH   /zoos/:Id // 更新某个指定动物园的信息（提供该动物园的部分信息）
- DELETE  /zoos/:Id // 删除某个动物园
- GET     /zoos/:Id/animals     // 列出某个指定动物园的所有动物
- DELETE  /zoos/:Id/animals/:Id // 删除某个指定动物园的指定动物
```

## RESTful API

[RESTful API](https://en.wikipedia.org/wiki/Representational_state_transfer) 就是符合`REST`设计标准的`API`。

### 特征和优点

- `客户端-服务器（Client-Server）` : 提供服务的服务器和使用服务的客户端分离；

  1. 提高客户端的便捷性（操作简单）
  2. 简化服务器提高可伸缩性（高性能、低成本）
  3. 允许客户端服务端分组优化，彼此不受影响
  
- `无状态（Stateless）` : 来自客户端的每一个请求必须包含服务器处理该请求所需的所有信息（请求信息唯一性）；

  1. 提高可见性（可以单独考虑每个请求）
  2. 提高可靠性（更容易故障恢复）
  3. 提高了可扩展性（降低了服务器资源使用）
  
- `可缓存（Cachable）` : 服务器必须让客户端知道请求是否可以被缓存？如果可以，客户端可以重用之前的请求信息发送请求；

  1. 减少交互连接数
  2. 减少连接过程的网络时延
  
- `分层系统（Layered System）` : 允许服务器和客户端之间的中间层（代理，网关等）代替服务器对客户端的请求进行回应，而客户端不需要关心与它交互的组件之外的事情；

  1. 提高了系统的可扩展性
  2. 简化了系统的复杂性
  
- `统一接口（Uniform Interface）` : 客户和服务器之间通信的方法必须是统一化的。（例如:GET,POST,PUT,DELETE）

  1. 提高交互的可见性
  2. 鼓励单独优化改善组件
  
- `支持按需代码（Code-On-Demand）` : 服务器可以提供一些代码或者脚本并在客户的运行环境中执行。

   提高可扩展性


## HTTP 状态码

```jsx
200 ok                     // 成功返回状态，对应，GET,PUT,PATCH,DELETE.
201 created                // 成功创建。
304 not modified           // HTTP缓存有效。
400 bad request            // 请求参数有误；语义有误，当前请求无法被服务器理解。
401 unauthorized           // 未授权。
403 forbidden              // 鉴权成功，但是该用户没有权限。
404 not found              // 请求的资源不存在
405 method not allowed     // 该http方法不被允许。
410 gone                   // 这个url对应的资源现在不可用。
415 unsupported media type // 请求类型错误。
422 unprocessable entity   // 校验错误时用。
429 too many request       // 请求过多。
500 internal server error  // 通用错误响应
503 Service Unavailable    // 服务端当前无法处理请求
```
