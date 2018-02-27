[React.js](https://reactjs.org/) 用于构建用户界面的 JavaScript 库，开发环境依赖于 [Node.js](https://nodejs.org/zh-cn/) 和 [npm](https://www.npmjs.com/)。


## 创建新应用

[Create React App](https://github.com/facebookincubator/create-react-app) 是构建React项目的命令行工具。

### 安装 create-react-app

```bash
npm install -g create-react-app
```

### 初始化项目

```bash
create-react-app my-app

cd my-app
npm start
```

安装记录:

```bash
Creating a new React app in ~/demos/my-app.

Installing packages. This might take a couple minutes.
Installing react, react-dom, and react-scripts...

> fsevents@1.1.2 install ~/demos/my-app/node_modules/fsevents
> node install

[fsevents] Success: "~/demos/my-app/node_modules/fsevents/lib/binding/Release/node-v57-darwin-x64/fse.node" already installed
Pass --update-binary to reinstall or --build-from-source to recompile

> uglifyjs-webpack-plugin@0.4.6 postinstall ~/demos/my-app/node_modules/uglifyjs-webpack-plugin
> node lib/post_install.js

npm notice created a lockfile as package-lock.json. You should commit this file.
+ react-scripts@1.0.17
+ react@16.2.0
+ react-dom@16.2.0
added 1274 packages in 93.668s

Success! Created my-app at ~/demos/my-app
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd my-app
  npm start

Happy hacking!
```

目录结构

```
.
├── README.md
├── package-lock.json
├── package.json
├── node_modules
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── registerServiceWorker.js
```

启动后会自动打开浏览器 http://localhost:3000 ，如看到如下页面表示环境搭建成功！

![启动图片](./fed/react/1515069343537.jpg)

