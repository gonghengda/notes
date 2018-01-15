
通过 [`PostCSS`](https://github.com/postcss/postcss) 的 [`Autoprefixer`](https://github.com/postcss/autoprefixer) 插件解析 `CSS`，能自动添​​加浏览器的前缀到 `CSS` 代码。它由 Google 推荐并用于Twitter和淘宝。  

## Autoprefixer
[`Autoprefixer`](https://github.com/postcss/autoprefixer) 是 `CSS` 的后处理器，您可以将其与预处理器（如Sass，Stylus或LESS）一起使用。  

使用 [`Autoprefixer`](https://github.com/postcss/autoprefixer) 很简单：根据最新的 W3C 规范，编写普通的 CSS。 [`Autoprefixer`](https://github.com/postcss/autoprefixer) 支持选择器（如:fullscreen和::selection），单元函数（calc()），at-rules（@supports和@keyframes）和属性。您可以尝试 [`Autoprefixer`](http://autoprefixer.github.io/) 的互动演示。  
```css
a {
  display : flex
}
::placeholder {
  color : #ccc
}

```
编译为：
```css
a {
  display : -webkit-box;
  display : -webkit-flex;
  display : -moz-box;
  display : -ms-flexbox;
  display : flex
}
:-ms-input-placeholder {
  color : #ccc
}
::-moz-placeholder {
  color : #ccc
}
::-webkit-input-placeholder {
  color : #ccc
}
::placeholder {
  color : #ccc
}
```
## 只有实际的前缀
`Autoprefixer` 同样会清理过期的前缀和不必要的前缀（如border-radius或CSS库生成的前缀）。因此下面的代码：
```css
a {
  -webkit-border-radius : 5px;
  border-radius : 5px
}
```
编译成：
```css
a {
  border-radius : 5px
}
```

## 安装 

```shell
$ npm install autoprefixer -g
```
## 跨浏览器兼容
`Autoprefixer` 使用 `Browserslist`，因此，您可以通过 `last 2 versions` (每个浏览器的最后2个版本)、`> 5%` (由全局使用统计信息选择的版本)、`not ie <=8` (排除先前查询选择的浏览器) 这样的查询来指定要在项目中定位的浏览器。

更多查询请参阅 [Browserslist](https://github.com/ai/browserslist#queries) 文档。
## 配置 Autoprefixer

你可以在 `webpack` 中使用 `postcss-loader` 和 `autoprefixer` 等[postcss插件](https://github.com/postcss/postcss#plugins)。

```js
const autoprefixer = require('autoprefixer');
module.exports = {
  module: {
    rules: [
      {test: /\.css$/,
        use: [
          require.resolve('style-loader'),
          {
            loader: require.resolve('postcss-loader'),
            options: {
              ident: 'postcss', // https://webpack.js.org/guides/migrating/#complex-options
              plugins: () => [
                require('postcss-flexbugs-fixes'),
                autoprefixer({
                  browsers: [
                    '>1%',
                    'last 4 versions',
                    'Firefox ESR',
                    'not ie < 9', // React doesn't support IE8 anyway
                  ],
                  flexbox: 'no-2009',
                }),
              ],
            },
          },
        ],
      },
    ]
  }
}
```

