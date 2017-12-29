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
