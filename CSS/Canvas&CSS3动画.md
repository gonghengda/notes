## Canvas 

`canvas` 是一个 `html` 标签，它给 `JavaScript` 提供了接口，通过js代码可以在 `canvas` 元素上绘制 2D 图形。

<img alt="canvas" src="./assets/canvas.jpg"/>

上图是通过canvas绘制的图形

### Canvas 基本绘画

向 HTML5 页面添加 `canvas` 元素。规定元素的 id、宽度和高度：

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

通过 JavaScript 来绘制 `canvas`， **`canvas`本身是没有绘图能力的**。所有的绘制工作必须在JavaScript内部完成：

```html
<script type="text/javascript">
  var c = document.getElementById("myCanvas");  // 获取 canvas 元素
  var cxt = c.getContext("2d");                 // 获取绘图环境（画布）
  cxt.fillStyle = "#FF0000";                    // 设置填充颜色
  cxt.fillRect(0,0,150,75);                     // 绘制填充矩形 x,y,w,h
</script>
```
上面代码通过 `canvas`，绘画出了一个红色矩形。更多绘图方法参考 [`W3C`](http://www.w3school.com.cn/html5/html_5_canvas.asp) 。

## CSS3动画

CSS*3*动画，可以取代许多网页动画图像(如:Flash动画)。CSS3属性中有关于制作动画的三个属性：`Transition`、`Transform`、`Animation`。

### Transition(过渡)

transition主要包含四个属性值：

- `transition-property` : 定义过渡效果的CSS属性的名称
- `transition-duration` : 定义过渡效果时长(秒或毫秒)
- `transition-timing-function` : 定义过渡速度曲线
- `transition-delay` : 定义过渡效果何时开始

下面代码表示将鼠标指针放到 div 元素上，其宽度会在2秒内从 100px 逐渐变为 300px：

```css
div {
  width: 100px;
  height: 100px;
  background: blue;
  transition: width 2s;
  transition-timing-function: ease; /* 先加速后减速 */
}

div:hover {
  width: 300px;
}
```
更多用法请参考 [W3C-transitions](https://www.w3.org/TR/css-transitions-1/#animatable-types)  

### transform(形变)

在CSS3中`transform`主要包括以下几种：旋转`rotate`、扭曲`skew`、缩放`scale`和移动`translate`以及矩阵变形`matrix`。

以`rotate`(旋转)为例，rotate()参数如果设置的值为正数表示顺时针旋转，如果设置的值为负数，则表示逆时针旋转。

```css
div {
  white: 100px;
  height: 100px;
  transform: rotate(30deg);
}
```
更多用法请参考 [W3C-transform](https://www.w3.org/TR/css-transforms-1/)  


### Animation(动画)

> CSS3中通过`@keyframes` 定义动画。

下面示例代码表示 `myfirst` 动画效果定义了三个状态，分别为起始（0%）、中（50%）和结束（100%）。使用百分比来规定变化发生的时间。

```css
/* keyframes 声明动画名称 */
@keyframes myfirst {
  0% { background: red; }
  50% { background: yellow; }
  100% { background: blue; }
}
```

`@Keyframes` 定义好了以后,通过 `Animation` 把 `myfirst` 动画捆绑到 `div` 元素，并设置时长：5 秒，动画开始时颜色为红色，执行到一半时为黄色，结束时为蓝色

```css
div:hover {
  animation-name: myfirst; /* 指定动画名称 */
  animation-duration: 5s;  /* 规定动画完成一个周期所花费的秒或毫秒。默认是 0。 */
}
```

更多用法请参考 [W3C-Animation](https://www.w3.org/TR/css-animations-1/)
