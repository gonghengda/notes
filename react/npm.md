# npm 基础讲解 


> **[npm](https://www.npmjs.com/)** 是随同NodeJS一起安装的包管理工具。

- 允许用户从npm服务器下载`第三方包`到本地使用。
- 允许用户从npm服务器下载`命令行工具`到本地使用。
- 允许用户`上传`自己编写的`包`或`工具`到npm服务器。

## 安装

新版的[nodejs](http://nodejs.cn/)已经集成了npm，因此可以通过`npm -v` 查看是否安装成功或版本信息，如：

```shell
npm -v
5.5.1
```

## 升级

```shell
npm install npm -g
```

## 安装模块

```shell
npm install <Module Name>
```

### 全局安装与本地安装

npm 的包安装分为本地安装（local）、全局安装（global）两种，从 *命令行* 来看，差别是是否存在参数 `-g`，如：

```shell
npm install doc-cli -g    # 全局安装

npm install doc-cli       # 本地安装
```

- 本地安装
  - 将安装包放在 `./node_modules` 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 `npm` 命令的目录下自动生成。  
  - 可以引入本地安装的包。  
- 全局安装
  - 将安装包放在 `/usr/local` 下或者你 `node` 的安装目录。  
  - 可以直接在命令行里使用。  

如果你希望具备两者功能，则需要在两个地方安装它或使用 `npm link`。

## 卸载模块

```shell
npm uninstall <Module Name>
```

## 升级模块

```shell
npm update <Module Name>
```

## package.json

`package.json` 是npm依赖的配置文件，位于模块的目录下，用于定义包的属性，如：

```json
{
  "name": "doc-example",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "react-doc -c src/component -d home,introduce,faq,doc,about --clean"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

### 属性说明

- `name` - 包名。
- `version` - 包的版本号。
- `description` - 包的描述。
- `homepage` - 包的官网 url 。
- `author` - 包的作者姓名。
- `contributors` - 包的其他贡献者姓名。
- `dependencies` - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
- `repository` - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
- `main` - main 字段指定了程序的主入口文件，默认值是index.js。
- `scripts` - npm执行命令。
- `keywords` - 关键字。

## 版本号

npm 版本号分为`X.Y.Z`三位，分别代表主版本号、次版本号和补丁版本号。

- 如果只是修复bug，需要更新Z位。
- 如果是新增了功能，但是向下兼容，需要更新Y位。
- 如果有大变动，向下不兼容，需要更新X位。

