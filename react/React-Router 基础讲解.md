
[React Router](http://react-guide.github.io/react-router-cn/index.html) 是一个基于 [React](https://reactjs.org/) 之上的强大路由库，它可以让你向应用中快速地添加视图和数据流，同时保持页面与 URL 间的同步。

## 快速开始

一种简单的快速创建 React web 项目的方式是使用 Create React App 工具，此工具由 Facebook 开发维护。  
如果你还没有使用过 create-react-app,你需要先安装，然后就可以创建一个新项目。

## React Router 安装命令

```jsx
npm install react-router-dom
// 或
yarn add react-router-dom
```

使用时，路由器`Router`就是 React 的一个组件。

## 使用方法

```jsx
import { Router } from 'react-router-dom';
render(<Router />, document.getElementById('app'));
```

`Router`组件本身只是一个容器，真正的路由要通过`Route`组件定义。或者，我们可以把它看做是 react 路由的一个路由外层盒子，它里面的内容就是我们单页面应用的路由以及路由组件

```jsx
import { Router, Route, hashHistory } from 'react-router-dom';
render(
  <Router history={hashHistory}>
    <Route path="/" component={App} />
  </Router>,
  document.getElementById('app')
);
```

上面代码中，用户访问根路由`/`，组件 APP 就会加载到`document.getElementById('app')`.也就是说，`<Router>`容器中包含多个 `<Route>`,每一个`<Router>`都有一个有效的 URL 路径，同时对应要渲染的组件。

## 引用

从上面的代码观察发现，使用 React-Router 时我们要引入(import)才可以使用。

**react-router-dom 与 react-router 的区别**

在 React-router 的使用中，我们一般会引入 react-router-dom,在有的地方你可能会看到 react-router,react-router-dom 是 react-router 的升级版本。

## 基本使用

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

const Home = () => (
  <div>
    <h2>首页</h2>
  </div>
);

const About = () => (
  <div>
    <h2>关于</h2>
  </div>
);

const RouteConfigExample = () => (
  <Router>
    <div>
      <ul>
        <li>
          <Link to="/">首页</Link>
        </li>
        <li>
          <Link to="/about">关于</Link>
        </li>
        <li>
          <Link to="/topics">主题列表</Link>
        </li>
      </ul>
      <Route exact path="/" component={Home} />
      <Route path="/about" component={About} />
      <Route path="/topics" component={Topics} />
    </div>
  </Router>
```

```jsx
const Topics = ({ match }) => (
  // 通过`match`对象获取相对应的属性；`match`对象包含的属性有：
  // - params - (object)从与路径的动态段对应的URL解析的键/值对
  // - isExact - 如果整个URL匹配，则为true
  // - path -(string)用于匹配的路径模式。用于构建嵌套的<Route>
  // - url - (string)URL的匹配部分。用于构建嵌套的<Link>
  <div>
    <h2>主题列表</h2>
    <ul>
      <li>
        <Link to={`${match.url}/rendering`}>使用 React 渲染</Link>
      </li>

      <li>
        <Link to={`${match.url}/components`}>组件</Link>
      </li>

      <li>
        <Link to={`${match.url}/props-v-state`}>属性v.状态</Link>
      </li>
    </ul>
    <Route path={`${match.url}/:topicId`} component={Topic} />
    <Route exact path={match.url} render={() => <h3>请选择一个主题</h3>} />
  </div>
);
```

```jsx
const Topic = ({ match }) => (
  <div>
    <h3>{match.params.topicId}</h3>
  </div>
);

export default BasicExample;
```

## 路由配置

首先，定义几个组件函数

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

const Sandwiches = () => {
  return <h2>Sandwiches</h2>;
};

const Bus = () => {
  return <h3>Bus</h3>;
};
const Cart = () => {
  return <h3>Cart</h3>;
};

const Tacos = ({ routes }) => {
  return (
    <div>
      <h2>Tacos</h2>
      <ul>
        <li>
          <Link to="/tacos/bus">Bus</Link>
        </li>
        <li>
          <Link to="/tacos/cart">Cart</Link>
        </li>
      </ul>
      {routes.map((route, i) => <RouteWithSubRoutes key={i} {...route} />)}
    </div>
  );
};
```

然后对路由进行配置

```jsx
const routes = [
  {
    path: '/sandwiches',
    component: Sandwiches
  },
  {
    path: '/tacos',
    component: Tacos,
    routes: [
      {
        path: '/tacos/bus',
        component: Bus
      },
      {
        path: '/tacos/cart',
        component: Cart
      }
    ]
  }
];
```

路由配置后就可以愉快的使用

```jsx
const RouteWithSubRoutes = route => (
  //获取路由地址后就会渲染相应的组件
  <Route
    path={route.path}
    render={props => (
      // 渲染相应的组件
      <route.component {...props} routes={route.routes} />
    )}
  />
);

const RouteConfigExample = () => (
  <Router>
    <div>
      <ul>
        <li>
          <Link to="/tacos">Tacos</Link>
        </li>
        <li>
          <Link to="/sandwiches">Sandwiches</Link>
        </li>
      </ul>
      {routes.map((route, i) => <RouteWithSubRoutes key={i} {...route} />)}
    </div>
  </Router>
);

export default RouteConfigExample;
```

## 常用 API

### `<Route>`

`<Route>`用于`<Router>`中，使用方法是如下：

```jsx
<Router>
  <div>
    <Route exact path="/" component={Home} />
    <Route path="/news" component={NewsFeed} />
  </div>
</Router>
```

`Route`有一个`path`属性，是路径地址，还有一个组件属性`component`后面跟上对应的组件名(路径所对应的界面)。

### `<BrowserRouter>`

一个使用了 HTML5 history API 的高阶路由组件，保证你的 UI 界面和 URL 保持同步。

### `<Redirect>`

渲染一个`<Redirect>`重定向到一个新的位置。新的位置将覆盖历史堆栈的当前位置。

```jsx
import { Route,Redirect } from 'react-router-dom'
<Route exact path='/' render={()=>(
  loggedIn?(
    <Redirect to='/dashboard'/>
  ):(<PublicHomePage/>)
)
}/>
```

### `<Switch>`

渲染与该位置匹配的第一个子`<Route>`或者`<Redirect>`

```jsx
<Route path="/about" component={About}/>
<Route path="/:user" component={User}/>
<Route component={NoMatch}/>
```

上面代码，如果 URL 是/about，那么`<About>，<User>`和`<NoMatch>`将全部呈现，因为它们全部匹配路径，这是通过设计允许我们以许多方式将`<Route>`组合成我们的应用程序，例如侧边栏和面包屑，引导选项卡等。但是，偶尔我们只想选择一个`<Route>`进行渲染。

```jsx
import { Switch, Route } from 'react-router-dom'

<Switch>
  <Route exact path="/" component={Home}/>
  <Route path="/about" component={About}/>
  <Route path="/:user" component={User}/>
  <Route component={NoMatch}/>
</Switch>
```

上面代码，`<Switch>`将开始寻找匹配的`<Route>`;例如：我们在/about 寻找匹配的`<Route><Route path="/about"/>`将匹配，`<Switch>`将停止查找匹配项并呈现`<About>`

### `<Link>`

Link 是 react 路由中点击切换到哪一个`组件`的链接。Link 代表一个链接，在 html 界面中会解析成 a 标签。作为一个链接，必须有一个 to 属性，代表链接地址。这个链接地址是一个相对路径。

```jsx
import { Link } from 'react-router-dom'

<Link to="/about">关于</Link>
```

### `<NavLink>`

一个比较特殊的`<Link>`，它可以添加样式属性。

**activeClassName:string**

当元素被激活时，该 class 生效，给定的默认类是活动的，这将与 className 道具相连接。

```
<NavLink to="/faq" activeClassName="selected">
  FAQs
</NavLink>
```

**activeStyle:object**

当为 active(激活)状态时，样式被应用于元素上。

```jsx
<NavLink
  to="/faq"
  activeStyle={{
    fontWeight: 'bold',
    color: 'red'
  }}
>
  FAQs
</NavLink>
```

## 对象和方法

### `history`

`Router`组件的 history 属性，用来监听浏览地址的变化，并将 URL 解析成一个地址对象，供 React Router 匹配。

`history`属性，一共可以设置三种值。

* browserHistory
* hashHistory
* createMemoryHistory

**history 对象具有的属性和常用方法**

* length:number 浏览历史堆栈中的条目数
* action:string 路由跳转到当前页面执行的动作，分为 PUSH,REPLACE,POP
* location:object 当前访问地址信息组成的对象，具有如下属性：
  * pathname:string URL 路径
  * search:string URL 中的查询字符串
  * hash:string URL 的 hash 片段
  * state:string 例如执行 push(path,state)操作时，location 的 state 将被提供到堆栈信息里，state 只有在 browser 和 memory history 有效。
* push(path,\[state\]):（function）将新条目推入历史堆栈
* replace(path,\[state\]):（function）替换历史堆栈上的当前条目
* go(n):（function）将记录中的指针移动 n 个条目
* goBack(): (function) 返回上一页
* goForward(): (function) 前往下一页

history 对象是可变的，建议从`<Route>`的 props 里来获取 location,而不是从 history.location 直接获取。这样可以保证 React 在生命周期中的钩子函数正常执行。
