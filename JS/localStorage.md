## `localStorage` 与 `cookie` 的异同

**相同点**  

都是在浏览器端存储在本地的数据，需要时可以直接从本地获取。

**不同点**  

1. `cookie` 数据始终在同源的 `http` 请求中携带。而 `localStorage` 不会自动把数据发给服务器，仅在本地保存。
2. `cookie` 数据不能超过4k，所以 `cookie` 只适合保存很小的数据。而 `localStorage` 可以达到5M或更大。
3. `localStorage` 始终有效，窗口或浏览器关闭也一直保存。`cookie` 在过期时间之前一直有效，即使窗口或浏览器关闭。

## 存入和读取

### localStorage的使用

1. 写入数据

```js
localStorage.setItem("name","caibin"); // 在localStorage中存储为 name:"caibin"
// 或
localStorage.name = "lucy";            // 改变localStorage中存入的值 
```

2. 读取数据

```js
localStorage.getItem("name");          // 打印结果为 caibin
// 或
let name = window.localStorage.name;   // 数据调取也可以使用这种方法
```

3. 删除数据

```js
localStorage.removeItem("name");       // 删除name字段存储的数据
```

4. 清空数据

```js
 localStorage.clear();                 // 清空所有存储的数据
```

5. 对象存取

```js
const students = {
  xiaomin: {
    name: "xiaoming",
    grade: 1
  },
  teemo: {
    name: "teemo",
    grade: 3
  }
}

const stuStr = JSON.stringify(students); // {"xiaomin":{"name":"xiaoming","grade":1},"teemo":{"name":"teemo","grade":3}}
localStorage.setItem("students",stuStr);

const stus = JSON.parse(localStorage.getItem("students"));
```
以上代码结果可以在控制台中的 `Application` 查看。
### cookie的使用

1. 设置cookie的值

> 每个 `cookie` 都是一个键值对，可以把下面的字符串赋值给 `document.cookie`：

```js
document.cookie="userId=828";
```

2. 修改cookie值

> 重新赋值即为修改。

```js
document.cookie="userId=929";
```

3. cookie的读取

```js
let strCookie = document.cookie;
console.log(strCookie); // userId=828
```

4. 设置cookie的失效日期

> 在默认情况下，一个 `cookie` 的生命周期就是在浏览器关闭的时候结束。如果想要 `cookie` 能在浏览器关掉之后还可以使用，就必须要为该 `cookie` 设置有效期，也就是 `cookie` 的失效日期。

```js
let date=new Date();
//将date设置为10天以后的时间
date.setTime(date.getTime()+10*24*3600*1000);
//将userId 的 cookie 设置为10天后过期
document.cookie="userId=929;expires=" + date.toGMTString();
```

5. 设置cookie可访问的路径 

> 为了控制cookie可以访问的目录，需要使用path参数设置cookie

```js
document.cookie="userId=929;path=/shop"; // 表示当前cookie仅在shop目录下使用。

document.cookie="userId=929;path=/";     // 表示当前cookie在整个网站下可用。
```


## sessionStorage与localStorage
```
Web Storage实际上由两部分组成：sessionStorage与localStorage。

sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。

localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

```
## userData

```
语法：

XML   <Prefix: CustomTag ID=sID STYLE="behavior:url('#default#userData')" />

HTML   <ELEMENT STYLE="behavior:url('#default#userData')" ID=sID>
```

## Scripting
```
 object .style.behavior = "url('#default#userData')"

object .addBehavior ("#default#userData")

属性:

expires 设置或者获取 userData behavior 保存数据的失效日期。

XMLDocument 获取 XML 的引用。

方法:

getAttribute() 获取指定的属性值。

load(object) 从 userData 存储区载入存储的对象数据。

removeAttribute() 移除对象的指定属性。

save(object) 将对象数据存储到一个 userData 存储区。

setAttribute() 设置指定的属性值。
```
## localStorage
方法：
```
localStorage.getItem(key):获取指定key本地存储的值

localStorage.setItem(key,value)：将value存储到key字段

localStorage.removeItem(key):删除指定key本地存储的值
```
