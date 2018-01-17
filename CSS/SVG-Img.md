
## SVG技术

> SVG可缩放矢量图形（Scalable Vector Graphics）是基于可扩展标记语言（XML），用于描述二维矢量图形的一种图形格式。

## SVG VS 图片

**SVG优势**

- 文件体积小，可压缩性更强
- 图片可无限放大而不失真
- 能够实现互动和滤镜效果
- 图像保留了可编辑和可搜寻的状态，根据需要可以自己编辑图像
- 所有的SVG可以全部在一个文件中，节省HTTP请求

## SVG VS Base64

`base64` 编码图片本质上是将图片的二进制大小以一些字母的形式展示，被完全嵌入到 `CSS` 文件中，虽然被压缩过，但效果不明显；作为背景图片，`IE6/IE7` 并不支持。  
而 `svg` 直接切图时使用 `svg` 格式保存，引入到文件中。既解决了兼容性问题，并且可压缩性更强。

## SVG基本使用

方法一：直接使用 `img` 标签的 `src` 属性引入保存好的图片，如下：

```html
<img alt="babel" height="50" src="./assets/babel-logo.svg"/>
```

效果如下：

<img alt="babel" height="50" src="./assets/babel-logo.svg"/>

方法二：直接将切好的 `svg` 图片代码放入HTML代码中，如下：

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="-6 -6 120 120">
  <title>React Logo</title>
  <circle cx="0" cy="0" r="1.05" fill="#1178C2"/>
  <g stroke="#1178C2" stroke-width="1" fill="none">
    <ellipse rx="5" ry="2.5"/>
    <ellipse rx="5" ry="2.5" transform="rotate(60)"/>
    <ellipse rx="5" ry="2.5" transform="rotate(120)"/>
  </g>
</svg>
```

效果如下：

<div width="100%" style="overflow-x: auto;"> 
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="-6 -6 120 120">
    <title>React Logo</title>
    <circle cx="0" cy="0" r="1.05" fill="#1178C2"/>
    <g stroke="#1178C2" stroke-width="1" fill="none">
      <ellipse rx="5" ry="2.5"/>
      <ellipse rx="5" ry="2.5" transform="rotate(60)"/>
      <ellipse rx="5" ry="2.5" transform="rotate(120)"/>
    </g>
  </svg>
</div>
