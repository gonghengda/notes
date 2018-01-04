# Babel 基础使用

本文参考 [阮一峰《Babel 入门教程》](http://www.ruanyifeng.com/blog/2016/01/babel.html)，

## 配置文件
Babel的配置文件是 `.babelrc` ，存放在项目的根目录下。使用Babel的第一步，就是配置这个文件。  
该文件用来设置转码规则和插件，基本格式如下。

```json
{
"presets": [],
"plugins": []
}
```

`plugins` 用来存放一些插件   
`presets` 字段设定转码规则，官方提供以下的规则集，你可以根据需要安装。

```shell
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```

然后，将这些规则加入 `.babelrc` 。

```json
  {
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```

## 命令行转码babel-cli

Babel提供babel-cli工具，用于命令行转码。  
它的安装命令如下。

```shell
$ npm install --save-dev babel-cli
```

基本用法如下。

```shell
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# 编译整个src目录并将其输出到一个连接文件。
$ babel src --out-file script-compiled.js

# -s 参数生成source map文件
$ babel src -d lib -s
```
然后，改写package.json。

```json
{
  "scripts": {
    "build": "babel src -d lib"
  },
}
```
转码的时候，就执行下面的命令。

```
$ npm run build
```
