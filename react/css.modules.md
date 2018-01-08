[CSS Modules](https://github.com/css-modules/css-modules) 不是将 CSS 改造成编程语言，只是加入了局部作用域和模块依赖。通过代码理解 [CSS Modules](https://github.com/css-modules/css-modules) 的工作原理。

下面是一个 React 组件 `Header.js`

```jsx
import React, { Component } from 'react';
import styles from './header.css';

export default class Header extends Component {
  render() {
    return <div className={styles.header}>头部内容</div>;
  }
}
```

上面代码中，我们将样式文件 `header.css` 输入到 `styles` 对象，然后引用 `styles.header` 代表一个 `class` 的名字 。

```css
/* header.css */
.header {
  font-size: 30px;
}
```

构建工具会将类名 `styles.header` 编译成一个哈希字符串，上面 css 中的 `.header` 被编译成 `._1YanEaTYJjuxFRwj3aH0JJ` 如下：

```css
._1YanEaTYJjuxFRwj3aH0JJ {
  font-size: 30px;
}
```

同时 HTML 的 class 也会被编译成一样哈希名字。

```html
<div class="_1YanEaTYJjuxFRwj3aH0JJ">
  头部内容
</div>
```

## 定义全局类名

```less
.title {
  color: yellow;
}
:global(.title) {
  color: green;
}
```

使用

```jsx
<div className={styles.title}></div>  // yellow
<div className="title"></div>         // green
```

## 定制哈希类名

很可能你再开发模式为了便于调试，样式名字不想被命名为哈希值，这个时候我们可以通过配置 [css-loader](https://github.com/webpack-contrib/css-loader) 来实现这一需求。

假设你的 webpack.conf.js 配置如下

```js
module.exports = {
  entry: __dirname + '/index.js',
  output: {
    publicPath: '/',
    filename: './bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        loader: require.resolve('babel-loader')
      },
      {
        test: /\.(css|less)$/,
        use: [
          require.resolve('style-loader'),
          {
            loader: require.resolve('css-loader'),
            options: {
              modules: true,
              localIdentName: '[name]-[hash:base64:5]'
            }
          }
        ]
      }
    ]
  }
};
```

设置你的 `css-loader` 配置，localIdentName 可以设置成 `[path][name]__[local]--[hash:base64:5]`， 如果你对这种规则不满意，可以通过 `css-loader` 提供的方法来定义自己的规则。

```js
{
  loader: 'css-loader',
  options: {
    modules: true,
    localIdentName: '[path][name]__[local]--[hash:base64:5]',
    getLocalIdent: (context, localIdentName, localName, options) => {
      return 'whatever_random_class_name'
    }
  }
}
```

## 组合样式

在 CSS Modules 中，两个选择器，被同一个标签组合[composition](https://github.com/css-modules/css-modules#composition)使用，提供一个方法来搞定这种引用方式。

```less
.className {
  color: green;
  background: red;
}
.otherClassName {
  composes: className;
  color: yellow;
}
```

HTML 最终被编译成两个样式名被引用，如下：

```html
<div class="_1c4SX _29UIc"></div>
```

## 引入文件组合样式

style.css

```css
.className {
  background-color: blue;
}
```

引入 `style.css` 文件

```css
.otherClassName {
  composes: className from './style.css';
}
```

在 HTML 中引入 `<div className={styles.otherClassName}></div>` 在 css 文件中生成了两个样式，Dom 节点上同样引用了这两个样式。

```html
<div class="_1c4SX _29UIc"></div>
```
