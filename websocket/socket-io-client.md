[参考socket.io-client 官网](https://github.com/socketio/socket.io-client/blob/master/docs/API.md#socketemiteventname-args-ack)
### 实测web前端代码 

```js
import React from 'react';
import socketio from 'socket.io-client';
import axios from "axios"

export default class Example extends React.Component {
  constructor(props) {
    super(props)
    this.state = {}
  }

  componentDidMount() {
    const io = socketio(`http://localhost:8090`, {
      query: {
        token: "123123"
      },
      reconnectionAttempts: 100, // 重连次数，默认无限次
      reconnectionDelay: 2000, // 重连延迟，默认1000，
    })
    io.on('connection', (msg) => {
      console.log('connection: ', msg)
    });

    io.on('disconnect', function (msg) {
      console.log('disconnect: ', msg);
    });

    io.on('newMsg', function (nickname, msg) {
      //显示这条新消息
      console.log("显示这条新消息", nickname, msg)
    });
  }

  onClickS = () => {
    console.log(this.input.value);
    axios.post("http://localhost:3113/api/admin_account/webSocket", {
      name: "gonghengda",
      text: this.input.value
    });
  }

  render() {
    return (
      <div>
        <input type="text" ref={el => this.input = el} />
        <button onClick={this.onClickS}>
          输入完成哦
          </button>
      </div>
    );
  }
}
```
