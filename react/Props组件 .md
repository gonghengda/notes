组件可以将UI切分成一些的独立的、可复用的部件，这样你就只需专注于构建每一个单独的部件。

> 组件名称，以 `大写字母` 开头 

## 函数组件

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// 使用 Welcome({name:"world"})
// 或者----
// <Welcome name="World!" />
```

## 类定义组件

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
//使用 <Welcome name="World!" />
```

## 组件渲染

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
ReactDOM.render(
  <div>
    <Welcome name="World!!" />
  </div>, 
  document.getElementById('root')
);
```

代码实例：https://codepen.io/jaywcjlove/pen/OzWyzp

## 组合组件

> 最外层必须有个节点包裹起来。  

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

ReactDOM.render(
  <div>
    <Welcome name="Welcome!" />
    <Welcome name="Cahal!" />
    <Welcome name="Edite!" />
  </div>,
  document.getElementById('root')
);
```

实例代码 https://codepen.io/jaywcjlove/pen/vpgNWL

## 提取组件

> 由于所有的嵌套会导致组件很难被改变，并且难以重用它的各个部分。我们需要从中提取一些组件。  

例如，考虑这个 Comment 组件：

```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
    </div>
  );
}
```
我们可以从 Comment 组件中提取 UserInfo 组件，以便于重用这段代码：
```jsx
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <img className="Avatar"
        src={props.user.avatarUrl}
        alt={props.user.name}
      />
      <div className="UserInfo-name">
      {props.user.name}
      </div>
    </div>
  );
}
```
提取出来的 Comment 组件进一步简化：
```jsx
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
    </div>
  );
}
```
如果你的用户界面的一部分被多次使用，或者是组件特别复杂，建议使用可重用组件。
