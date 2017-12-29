# widths-heights

> HTML中常常会使用到元素的各种宽度(width)和高度(height)以及距左距右的距离，例如 `clientWidth` `clientHeight` `scrollTop` `offsetLeft` ...，但他们代表什么样的距离值，哪个地方的值都没有认真了解过😅.

*网络上有张图片解释的很清楚*

![](./wh.jpg)

***从这张图大致可以将这些值分为四类***

- `client*`
- `offset*`
- `style*`
- `scroll*`

## client

> 当前元素的距`顶部`、`左边界`、`内部宽度` `内部高度`的值  

- `clientTop`
- `clientLeft`
> 说白了就是边框(`border`)的值，跟`style.borderTop` `style.borderLeft`一致

- `clientWidth`
- `clientHeight`
> 当前元素内容可显示的最大宽度和高度

## offset

- `offsetHeight`
- `offsetWidth`
> `边框尺寸` + `内部尺寸` = 当前元素的`offset*`

- `offsetLeft`
- `offsetTop`
> 当前元素`外部边界`距离`直接父级` **内部**(`clientWidth` `clientHeight`) 的`距左距右`距离

## style

> 当前元素样式指定的值

- `padding`
- `margin`
- `border`

## scroll

- `scrollHeight`
- `scrollWidth`
> 当前元素的宽高，包括`verflow: hidden`的值

- `scrollTop`
- `scrollLeft`
> 当前元素滚动的距离(`水平滚动`，`垂直滚动`)

## 参考文档

- [令人头疼的clientTop、scrollTop、offsetTop](https://www.cnblogs.com/gagarinwjj/p/conflict_client_offset_scroll.html)
