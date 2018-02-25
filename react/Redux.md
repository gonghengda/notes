
2014年 Facebook 为了解决大型复杂的 `代码结构` 和 `组件之间的通信` 问题，提出了 [<img alt="flux" height="10" src="./assets/flux-logo.svg"/> Flux](https://facebook.github.io/flux/) 架构的概念，引发了很多([至少15种](https://github.com/voronianski/flux-comparison))的实现，2015年，[<img alt="redux" height="12" src="./assets/redux-logo.svg"/> Redux](http://redux.js.org) 出现，将 Flux 与函数式编程结合一起，很短时间内就成为了最热门的前端架构，。

<a href="http://redux.js.org">
  <img alt="redux" height="64" src="./assets/redux-logo.svg"/>
</a>

<ruby>React 早期贡献者之一 Pete Hunt 说：<rt>As Pete Hunt, one of the early contributors to React, says:</rt></ruby>

> <ruby>"你应当清楚何时需要 Flux。如果你不确定是否需要它，那么其实你并不需要它。"<rt>You'll know when you need Flux. If you aren't sure if you need it, you don't need it.</rt></ruby>

<ruby>同样，Redux的创始人之一Dan Abramov说：<rt>Similarly, Dan Abramov, one of the creators of Redux, says:</rt></ruby>

> <ruby>"我想修正一个观点：当你在使用 React 遇到问题时，才使用 Redux。"<rt>I would like to amend this: don't use Redux until you have problems with vanilla React.</rt></ruby>

上面对话出自官网：[When should I use Redux?](https://redux.js.org/docs/faq/General.html#when-should-i-use-redux)

<img height="180px" src="./assets/redux-New.png" />

大概需要使用 Redux 的场景：

- 用户的使用方式复杂
- 不同身份的用户有不同的使用方式（比如普通用户和管理员）
- 多个用户之间可以协作
- 与服务器大量交互，或者使用了WebSocket
- View要从多个来源获取数据

## 4张动图解释 Redux

<img alt="node" width="360" src="./assets/redux1.gif"/>

React 使用单向数据流，这意味着父组件把自身的状态作为属性传递给子组件。

<img alt="node" width="360" src="./assets/redux2.gif"/>

随着添加更多的功能，非父子组件之间需要共享一些状态，这意味着我们将状态（和改变这个状态的函数）提升到最接近的祖先（Container Component）。我们将这些函数绑定到容器组件，并将它们作为属性向下传递。这意味着子组件可以触发其父组件中的状态更改，这将更新树中的所有其他组件。

<img alt="node" width="380" src="./assets/redux3.gif"/>

随着添加了更多的功能和组件，我们的应用程序状态流程开始看起来像这样..

<img alt="node" width="380" src="./assets/redux4.gif"/>

当我们使用 Redux 后，状态变成了这样。

## React & Redux 模型对比

Redux 模型  

<img alt="node" width="320" src="./assets/redux5.jpg"/>

React 的模型  

<img alt="node" width="320" src="./assets/redux6.jpg"/>


## 传统MVC

```shell
BROWSER             SERVER                    DATABASE
╭──────╮  request   ╭────────────╮  request   ╭───────╮
┆      ┆ ┈┈┈┈┈┈┈┈┈▶ ┆            ┆ ┈┈┈┈┈┈┈┈┈▶ ┆       ┆
┆ VIEW ┆  response  ┆ CONTROLLER ┆  response  ┆ MODEL ┆
┆      ┆ ◀┈┈┈┈┈┈┈┈┈ ┆            ┆ ◀┈┈┈┈┈┈┈┈┈ ┆       ┆
╰──────╯            ╰────────────╯            ╰───────╯
```

## FLUX

```shell
                                         ┌──────────╮                   
                          ╭──────────╮   │          │       ╭──────────╮
                          │ Actions  ├──▶│Dispatcher│───────│Callbacks │
                          ╰─────┬────╯   │          │       ╰─────┬────╯
                                │        ╰──────────╯             │     
                                │                                 ▼     
╭─────╮    ╭─────────╮    ╭─────┴────╮                         ╭───────╮
│ Web │◀───┤Web      │◀───┤  Action  │                         │ Store │
│ API ├───▶│API Utils├───▶│ Creators │                         ╰──┬────╯
╰─────╯    ╰─────────╯    ╰─────┬────╯                            │     
                                │                      ╭──────────┴────╮
                                │                      │               │
                          ╭─────┴─────╮   ╭────────╮   │ Change Events │
                          │   User    ├───┤ React  ┆◀──┤ Store Queries │
                          │Interactios│   │ views  │   │               │
                          ╰───────────╯   ╰────────╯   ╰───────────────╯
```

FLUX 理解

```shell
 COMPONENTS          ACTION CREATORS           STORES
   ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈<<<<┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
   ┆                                              ┆
╭──┴───╮            ╭────────────╮            ╭───┴───╮
┆      ┆  request   ┆            ┆  request   ┆       ┆
┆ VIEW ┆ ┈┈┈┈┈┈┈┈┈▶ ┆            ┆ ┈┈┈┈┈┈┈┈┈▶ ┆ MODEL ├┈┈┈╮
┆      ┆            ┆            ┆            ┆       ┆   ┆
╰──────╯            ┆            ┆            ╰───────╯   ┆
                    ┆ CONTROLLER ┆                        ┆
╭──────╮            ┆            ┆            ╭───────╮   ┆
┆      ┆  request   ┆            ┆  request   ┆       ┆   ┆
┆ VIEW ┆ ┈┈┈┈┈┈┈┈┈▶ ┆            ┆ ┈┈┈┈┈┈┈┈┈▶ ┆ MODEL ┆   ┆
┆      ┆            ┆            ┆            ┆       ┆   ┆
╰──┬─┬─╯            ╰────────────╯            ╰───┬───╯   ┆
   ┆ ┆                                            ┆       ┆
   ┆ ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈<<<<┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯       ┆
   ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈<<<<┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯
```



```shell
╭──────╮   signal   ╭────────────╮  set   ╭───────╮
┆      ┆ ─────────▶ ┆            ┆ ─────▶ ┆       ┆
┆ VIEW ┆   event    ┆ CONTROLLER ┆  get   ┆ MODEL ┆
┆      ┆ ◀━━━━━━━━  ┆            ┆ ◀┈┈┈┈┈ ┆       ┆
╰──────╯            ╰────────────╯        ╰───────╯
```


```shell
╭────────╮   signal   ╭────────────╮  set   ╭───────╮
┆        ┆ ─────────▶ ┆            ┆ ─────▶ ┆       ┆
┆ ROUTER ┆   event    ┆            ┆  get   ┆       ┆
┆        ┆ ◀━━━━━━━━  ┆            ┆ ◀┈┈┈┈┈ ┆       ┆
╰┈┈┈┈┈┈┈┈╯            ┆            ┆        ┆       ┆
                      ┆ CONTROLLER ┆        ┆ MODEL ┆
╭──────╮   signal     ┆            ┆  set   ┆       ┆
┆      ┆ ───────────▶ ┆            ┆ ─────▶ ┆       ┆
┆ VIEW ┆   event      ┆            ┆  get   ┆       ┆
┆      ┆ ◀━━━━━━━━━━  ┆            ┆ ◀┈┈┈┈┈ ┆       ┆
╰──────╯              ╰────────────╯        ╰───────╯
```

## Redux

### 安装

```bash
$ npm install --save react-redux
```

### Store

`Store` 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 `Store`。 Redux 提供createStore这个函数，用来生成 `Store`。

```jsx
import { createStore } from 'redux';
const store = createStore(fn);
```

上面代码中，`createStore` 函数接收另一个函数作为参数，返回新生成的 `Store` 对象。

### State

`Store` 对象包含所有数据，通过 `store.getState()` 可以拿到当前时刻的 `State`。

```jsx
import { createStore } from 'redux';
const store = createStore(fn);
const state = store.getState();
```

### Action

Action 是纯JavaScript对象。Action必须具有 `type` 指示正在执行的操作的类型的属性。类型通常应该定义为字符串常量  
下面代码中，Action 的名称是 `ADD_TODO`，它携带的信息是字符串 `Learn Redux`。  

```jsx
const action = {
  type: 'ADD_TODO',
  payload: 'Learn Redux'
};
```

### store.dispatch()

改变 `State` 的唯一办法 ,就是通过 `store.dispatch()` 发出 Action 。

```jsx
import { createStore } from 'redux';
const store = createStore(fn);

store.dispatch({
  type: 'ADD_TODO',
  payload: 'Learn Redux'
});
```

### Reducer

`Store` 收到 `Action` 以后，必须给出一个新的 `State`，这样 View 才会发生变化。这种 `State` 的计算过程就叫做 `Reducer`。  
下面代码中，每当 View 发送一个新的 `Action`，就会自动调用 `Reducer`，得到新的 `State`。

```jsx
import { createStore } from 'redux';

const reducer = (state = 0, action) => {
  switch (action.type) {
    case 'ADD':
      return state + action.payload; 
    default: 
      return state;
  }
};

const store = createStore(reducer);
const state = reducer(1, {
  type: 'ADD',
  payload: 2
}); //3
```

`reducer` 函数收到名为 `ADD` 的 `Action` 以后，就返回一个新的 State，

### store.subscribe()

监听函数，一旦 State 发生变化，就自动执行这个函数。然后您可以调用 `getState()` 读取回调中的当前 `state`。

```jsx
import { createStore } from 'redux';
const store = createStore(reducer);
store.subscribe(listener);
```

显然，只要把 View 的更新函数（对于 React 项目，就是组件的 `render` 方法或 `setState` 方法）放入 `listen`，就会实现 View 的自动渲染。

### Provider

`React-Redux` 提供 `Provider` 组件，可以让容器组件拿到 `state`。

```jsx
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import todoApp from './reducers'
import App from './components/App'

let store = createStore(todoApp);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

上面代码中，`Provider` 在根组件外面包了一层，这样一来，App 的所有子组件就默认都可以拿到 `state` 了。

## 组件概念

React-Redux 将所有组件分成两大类：UI组件和容器组件。  
> UI 组件特征:
- 只负责 UI 的呈现，不带有任何业务逻辑
- 没有状态（即不使用this.state这个变量）
- 所有数据都由参数（this.props）提供
- 不使用任何 Redux 的 API

> 容器 组件特征:
- 负责管理数据和业务逻辑，不负责 UI 的呈现
- 带有内部状态
- 使用 Redux 的 API
> React-Redux 规定，所有的 UI 组件都由用户提供，容器组件则是由 React-Redux 自动生成。也就是说，用户负责视觉层，状态管理则是全部交给它。

## connect()

`connect` 方法用于从 UI 组件生成容器组件。`TodoList` 是 UI 组件，`VisibleTodoList` 就是由 React-Redux 自动生成的容器组件。

```jsx
import { connect } from 'react-redux'
const VisibleTodoList = connect( mapStateToProps, mapDispatchToProps)(TodoList)
```

`connect` 方法接收了两个参数，前者负责将 `state` 作为组件的参数（props），后者将用户的操作映射成 Action。

## mapStateToProps()

下面代码中，`mapStateToProps` 接收 `state` ，`state` 有一个 `filter` 属性，它的值就是 `Store` 返回的 `state`   
`mapStateToProps` 会订阅 `Store`，每当 `Store` 更新的时候，就会自动执行，重新计算 UI 组件的参数，从而触发 UI 组件的重新渲染。

```jsx
const mapStateToProps = (state) => {
  return {
    todos: state.filter
  }
}
```

## mapDispatchToProps()

`mapDispatchToProps` 是用来建立 UI 组件的参数到 `store.dispatch` 方法的映射。也就是说，它定义用户的某些操作应该当作 `Action` 传给 `Store`。  

```jsx
// `dispatch` 是将要发送的 Action ， `ownProps` 是容器组件的props对象
const mapDispatchToProps = ( dispatch, ownProps) => {
  return {
    onClick: () => {
      dispatch({
        type: 'SET_VISIBILITY_FILTER',
        filter: ownProps.filter
      });
    }
  };
}
```

## 例子

下图简单概述了 `redux` 的工作流程，每次发起一个 `Action` 的时候，`Dispatcher` 就会执行更新 `Store` 的方法，并得到一个新的 `Store` ，View 会根据拿到的 `Store` 做出相应的变化!

```bash
                                 ╭───────╮              
                      ╭──────────│Action │─────────╮    
                      │          ╰───────╯         │    
                      │                            │    
                      ▼                            │    
╭──────────╮    ╭──────────╮     ╭───────╮     ╭───┴───╮
│  Action  ├───▶│Dispatcher├────▶│ Store ├────▶│ View  │
╰──────────╯    ╰──────────╯     ╰───────╯     ╰───────╯
```

下面代码中，`createStore` 接收到了 `reducer` ，只要 View 发送 Action 就会生成一个新的 `Store`, `Provider` 组件接收到的 `store` 作为props传给`App`。

```jsx
import { createStore } from 'redux'
import { Provider } from 'react-redux'
import App from './App'

const reducer = (state = 0, action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return action.text;
    default: 
      return state;
  }
};

let store = createStore(reducer)
render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

下面代码中，`connect` 函数收到 `Provider` 传出的 `store`，然后接受三个参数 `mapStateToProps`，`mapDispatchToProps` 和组件。   
`mapDispatchToProps` 当用户执行 `onClick` 时，会通过 `store.dispatch` 方法发送 `Action`，重新更新 `Store`  

```jsx
import { connect } from 'react-redux'

class App exteds Component {
  const mapStateToProps = (state) => {
    console.log(state) // 发送 Action 之间  = 0 ；发送 Action 之后  = 'Read the docs' 
  }
  const mapDispatchToProps = ( dispatch, ownProps) => {
    return {
      onClick: () => {
        dispatch({ type: 'ADD_TODO', text: 'Read the docs'})
      }
    };
  }
}
export default connect(mapStateToProps,  mapDispatchToProps)(App)
``` 

## 参考资料

- [Redux官网](https://redux.js.org/)
