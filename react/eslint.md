# ESLint 基础讲解 

本文参考  [ESLint-官方文档](https://eslint.org/) [ESLint-使用入门](https://csspod.com/getting-started-with-eslint/)

在团队协作中，为避免低级 Bug、产出风格统一的代码，会预先制定编码规范。  
使用 Lint 工具和代码风格检测工具，则可以辅助编码规范执行，有效控制代码质量。
## Eslint的安装

如果你想把ESLint作为你的项目构建系统的一部分,我们建议在本地安装。
```shell
  npm install eslint -g         # 全局安装
  npm install eslint --save-dev # 本地安装
  eslint --init                 # 自动生成 .eslintrc 配置文件          
```
`.eslintrc` 放在项目根目录，则会应用到整个项目；如果子目录中也包含 .eslintrc 文件，  
则子目录会忽略根目录的配置文件，应用该目录中的配置文件。这样可以方便地对不同环境的代码应用不同的规则。

## .eslintrc 文件示例

```shell
{
  "env": {
    "browser": true,
  },
  "parserOptions": {
    "ecmaVersion": 6,
  },
  "rules": {
    "camelcase": 2,
    "curly": 2,
  }
}
```

## EsLint的配置

### Environments

Environment可以预设好的其他环境的全局变量，如brower、node环境变量、es6环境变量、mocha环境变量等  
可以参考 [Specifying Environments](https://eslint.org/docs/user-guide/configuring#specifying-environments)

```shell
{
 "env": {
  "browser": true,
  "node": true
 }
}
```
如果你想使用插件中的环境变量，你可以使用plugins指定，如下

```shell
{
 "plugins": ["example"],
 "env": {
  "example/custom": true
 }
}
```

### parserOptions

ESLint允许你指定你想要支持的JavaScript语言选项。默认情况下，ESLint预计ECMAScript 5语法。  
您可以覆盖该设置，以使用解析器选项启用对其他ECMAScript版本以及JSX的支持。  
可以参考 [Specifying Parser Options](https://eslint.org/docs/user-guide/configuring#specifying-parser-options)
```shell
{
 "parserOptions": {
  "ecmaVersion": 6,       //指定ECMAScript支持的版本，6为ES6
  "sourceType": "module", //指定来源的类型，有两种”script”或”module”
  "ecmaFeatures": {
   "jsx": true            //启动JSX
  },
 }
}
```

### Globals

指定你所要使用的全局变量，true代表允许重写、false代表不允许重写

```shell
{
 "globals": {
  "var1": true,
  "var2": false
 }
}
```

### Parser

EsLint默认使用esprima做脚本解析，当然你也切换他，比如切换成babel-eslint解析
```shell
{
 "parser": "esprima" //默认，可以设置成babel-eslint，支持jsx
}
```
### Rules

自定义规则，一般格式：
> "off" or 0 - 关闭规则  
> "warn" or 1 - 将规则视为一个警告（不会影响退出码）  
> "error" or 2 - 将规则视为一个错误 (退出码为1)  
>

自定义规则可以参考 [Rules-官方文档](http://eslint.org/docs/rules/) [Eslint-规则说明](http://blog.csdn.net/helpzp2008/article/details/51507428)

```shell
{
 "plugins": [
  "react"
 ],
 "rules": {
    'no-var': 'error',// no-var
    'init-declarations': 2, // 要求或禁止 var 声明中的初始化
    'quotes': ['error', 'single'], // 强制使用单引号
    'semi': ['error', 'never'],// 要求或禁止使用分号而不是 ASI
    'indent': ['error', 2, {'SwitchCase': 1}], // 空格2个
 }
}
```
所有的规则默认都是禁用的。在[配置文件](http://eslint.cn/docs/user-guide/configuring#extending-configuration-files)中，使用 `"extends": "eslint:recommended"` 来启用规则
### Plugins

ESLint 内置的规则不可能包罗所有需求。可以通过插件实现自定义规则，这是 `ESLint` 最有卖点的功能。  
在 `NPM` 上以 `eslintplugin` 为关键词，可以搜索到很多插件，包括 `eslint-plugin-react`。  
以 `eslint-plugin-react` 为例，安装以后，需要在 `ESLint` 配置中开启插件，其中 `eslint-plugin-` 前缀可以省略：

```shell
{
 "plugins": [
  "react" 
  ]
}
```
接下来开启 `JSX` 然后就可以配置插件提供的规则了
```shell
{
  "ecmaFeatures": {
    "jsx": true
  },
   "rules": {
    "react/display-name": 1,
    "react/jsx-boolean-value": 1
  }
}
```
在  文件中的scripts字段中配置如下3个属性即可:
### 配置 package.json

在 `package.json` 文件中配置如下:
```shell
 "scripts": {
    "lint": "eslint .",
  },
```

## 设置忽略文件
### .eslintignore
在 `.eslintrc` 同级目录下面新建一个文件 `.eslintignore`  
 -  ESLint总是忽略 `/node_modules/*` 和 `/bower_components/*` 中的文件。   
 -  以 # 开头的行被当作注释，不影响忽略模式。  
 -  路径是相对于 .eslintignore 的位置或当前工作目录。  
 -  以 ! 开头的行是否定模式，它将会重新包含一个之前被忽略的模式。  

例如：把下面 .eslintignore 文件放到当前工作目录里，将忽略 `node_modules` 以及 `lib` 目录下除了 `lib/index.js` 的所有文件。
```shell
node_modules/*
lib/*
!lib/index.js
```

## 检查代码

如需要手动检查所有代码的问题 ,可以打开控制台,输入 `eslint .` or `eslint src/index.js`

## 自动修复

如需要自动修复一些不规范的代码问题 ,例如 没有分号的问题,可以输入
```shell
 eslint . --fix
``` 
可以参考 [Rules-官方文档](http://eslint.org/docs/rules/) 带小扳手的规则都可以自动修复.
