模块化主要是解决代码分割、作用域隔离、模块之间的依赖管理以及发布到生产环境时的自动化打包与处理等多个方面的问题。

## 优点

1. **可维护性**：因为模块是独立的，一个设计良好的模块，会让其他模块对自己的依赖越少越好，这样自己就可以独立去更新和改进。

2. **命名空间**：在 JavaScript 里面，如果一个变量在最顶级的函数之外声明，它就直接变成全局可用。因此，常常会因不小心而出现命名冲突的情况。使用模块化开发来封装变量，可以避免污染全局环境。

3. **重用代码**：我们有时候会喜欢从之前写过的项目中拷贝代码到新的项目，这没有问题，但是更好的方法是，通过模块引用的方式，来避免重复的代码库。

## 模块加载规范

随着前端快速发展，前辈们的努力，在前端产生了几种标准：

### CMD规范

CMD（通用模块规范）规范的前身是Modules/Wrappings规范，代表工具[Sea.js](https://github.com/seajs/seajs)，[官网](https://seajs.github.io/seajs/docs/)，下面用两个实例祭奠它。

实例一

```js
// seajs 的简单配置
seajs.config({
  base: "../sea-modules/",
  alias: {
    "jquery": "jquery/jquery/1.10.1/jquery.js"
  }
})

// 加载入口模块
seajs.use("../static/hello/src/main")
```

实例二

```js
// 所有模块都通过 define 来定义
define(function(require, exports, module) {

  // 通过 require 引入依赖
  var $ = require('jquery');
  var Spinning = require('./spinning');

  // 通过 exports 对外提供接口
  exports.doSomething = ...

  // 或者通过 module.exports 提供整个接口
  module.exports = ...

});
```

### AMD规范

<a href="http://requirejs.org/"><img alt="redux" height="74" src="./assets/require-logo.svg"/></a>

AMD（异步模块规范）是一个在浏览器端模块化开发的规范，随着[RequireJS](http://requirejs.org/)成为最流行的实现方式，异步模块规范（AMD）在前端界一度被广泛认同，同样祭出实例：

```js
requirejs.config({
  //除了在项目中可能已经拥有的baseUrl或路径配置之外，还可以添加map这个配置。
  map: {
    // 意思是对所有加载的模块，使用这个 * 配置依赖 “jquery-private”。如果有一个更具体的map配置，那么将优先于 * 配置。
    '*': { 'jquery': 'jquery-private' },

    // jQuery-private 想要获得真正的jQuery模块。需要添加这个配置，否则将会有一个无法解决的循环依赖关系。
    'jquery-private': { 'jquery': 'jquery' }
  }
});

// jquery-private.js 文件中的 'jquery-private'模块：
define(['jquery'], function (jq) {
  return jq.noConflict( true );
});
```
根据AMD规范，我们可以使用 `define` 定义模块，使用 `require` 调用模块。
更多配置可参考 [RequireJS API](http://requirejs.org/docs/api.html)

### CommonJS规范

CommonJS 是服务器端模块的规范。Node.JS 采用了 `js` 模块化的概念，也就是说，在该模块内部定义的变量，无法被其他模块读取，除非定义为 `global` 对象的属性。

输出模块最好的方法是使用 module.exports 对象。

```js
var max = 30;

module.exports = function () {
 for (var i = 1; i < max;i++; ) {
  console.log(i);
 }
};
```

上面代码通过 module.exports 对象，定义了一个函数，该函数就是模块外部与内部通信的桥梁。
加载模块使用 `require` 方法，该方法读取一个文件并执行，最后返回文件内部的 module.exports 对象。

下图简述了模块化开发的工作流程：

```shell
             ┌──────────────────┐                        
             │    创建模块方案    │                        
             └──────────────────┘                        
                       │                                 
         ┌─────────────┴─────────────┐                   
┌──────────────┐               ┌──────────────┐          
│  渲染服务器端  │               │  渲染浏览器端  │          
└──────────────┘               └──────────────┘          
        │                     ┌────────┴───────┐       
┌──────────────┐        ┌───────────┐    ┌───────────┐
│   CommonJS   │        │    AMD    │    │    CMD    │
└──────────────┘        └───────────┘    └───────────┘
        │                     │                │      
┌──────────────┐        ┌───────────┐    ┌───────────┐
│     Node     │        │ RequireJS │    │   SeaJS   │
└──────────────┘        └───────────┘    └───────────┘
```
