
## CSS预处理器

> CSS 预处理器是为了方便写css代码而专门设计的一种“类似编程的语言”，经过编译后形成普通的css文件，无需考虑浏览器的兼容性问题。

[`less`](http://less.bootcss.com/)、[`sass`](https://www.sass.hk/)、[`stylus`](http://stylus-lang.com/try.html) 是目前最主流的CSS预处理器。

## sass、less、stylus语法区别 

Sass 和 Less 都使用的是标准的 CSS 语法，因此可以很方便的将已有的 CSS 代码转为预处理器代码，默认 Sass 使用 `.sass` 扩展名，而 Less 使用 `.less` 扩展名。

```css
/* style.scss or style.less */
h1 { color: #0982C1; }
```

而 Stylus 支持的语法要更多样性一点，它默认使用 `.styl` 的文件扩展名。且省略了`{}` `:` 及 `;`。

```stylus
/* style.styl */
h1 { color: #0982C1; }
/* 去掉{}和冒号 */
h1
  color #0982C1
```
## 变量声明

你可以把反复使用的css属性值定义成变量，然后通过变量名来引用它们。

#### Sass

sass变量必须是以`$`开头的，然后变量和值之间使用英文冒号（`:`）隔开，和css属性是一样的，例如：

```scss
$maincolor : #092873;
$siteWidth : 1024px;
$borderStyle : dotted;

body {
  color: $maincolor;
  border: 1px $borderStyle $mainColor;
  max-width: $siteWidth;
}
```
#### Less

在less中通过`@`符号定义变量。其余与sass都是一样的，例如：

```less
@maincolor : #092873;
@siteWidth : 1024px;
@borderStyle : dotted;

body {
  color: @maincolor;
  border: 1px @borderStyle @mainColor;
  max-width: @siteWidth;
}
```
#### Stylus

stylus 对变量是没有任何设定的，可以是以$开头，或者任何的字符，而且与变量之间可以用冒号，空格隔开，但是在**stylus中不能用@开头**，例如：    

```stylus
maincolor = #092873
siteWidth = 1024px
borderStyle = dotted

body 
  color maincolor
  border 1px borderStyle mainColor
  max-width siteWidth
```
以上三种写法都如同一下这种css：

```css
body {
  color: #092873;
  border: 1px dotted #092873;
  max-width: 1024px;
}
```

这样做的好处也是显而易见的，在修改多处相同颜色的时候，这时就只需要修改变量值即可。

### 示例

下面以 LESS 为例：

```less
.opacity(@opacity: 100) {
  opacity: @opacity / 100;
  filter: ~"alpha(opacity=@{opacity})";
}

.sidebar {
  .opacity(50);
}
```

将以上less代码，编译成css：

```css
.sidebar {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
```

可以看到，编译前与编译后是完全不同的语言。

## CSS后处理器

`CSS`后处理器是对`CSS`进行处理，并最终生成 `CSS` 的预处理器。  

典型的后处理工具

- 自动加前缀：Autoprefixer（基于 PostCSS）
- PostCSS

下面以 PostCSS 的 [`Autoprefixer`](https://github.com/postcss/autoprefixer) 插件为例：

```css
.container {
  display: flex;
}
```

将以上标准CSS，编译为带有浏览器私有前缀的CSS：

```css
.container {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
}
```
## PostCSS 

[`PostCSS`](https://github.com/postcss/postcss) 可以理解为一个平台，通过 [`PostCSS`](https://github.com/postcss/postcss) 平台提供的插件能够为 CSS 提供额外的功能。

通常情况下 [`PostCSS`](https://github.com/postcss/postcss) 是配合预处理器（less、sass、stylus）一起使用的,他们能将各自最擅长的部分添加到你的工作流中，让你工作变得更加轻松。

目前，[`PostCSS`](https://github.com/postcss/postcss) 拥有200多个个插件。您可以在[插件列表](https://github.com/postcss/postcss/blob/master/docs/plugins.md)或[可搜索的目录](https://www.postcss.parts/)中找到所有插件。下面推荐两个 [`PostCSS`](https://github.com/postcss/postcss) 插件，建议与预处理器（less、sass、stylus）一起使用

- [`Autoprefixer`](https://github.com/postcss/autoprefixer) 添加浏览器的私有前缀。
- [`stylelint`](https://github.com/stylelint/stylelint) 可以帮助您避免错误，并在样式表中自动修复。


