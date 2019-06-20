### 实测代码

```js 
var config = require('./config.js')
var io = require('socket.io')(8090);
var HALF_HOUR_IN_SEC = 1800;

let users = []
// 使用中间件
io.use((socket, next) => {
  let token = socket.handshake.query.token;
  if (!token) return next(new Error('token 不存在，请先登录后再连接socket'));
  return next();
});

// 连接
io.sockets.on('connection', function (socket) {
  let token = socket.handshake.query.token;
  let value = socket.id;
  socket.emit('connection', socket.id)

  // learning
  // socket.emit('request', /* */); // 向套接字发出事件
  // io.emit('broadcast', /* */); // 向所有已连接的套接字发出事件
  // socket.on('reply', function(){ /* */ }); // listen to the event
});

io.sockets.on('disconnect', function (socket) {
  var index = users.indexOf(socket.nickname);
  users.splice(index, 1);//将断开用户的昵称从全局数组users中删除
  io.sockets.emit('system', socket.nickname, users.length, 'logout');
  io.sockets.emit('disconnect');
});



/**
 * 发送消息
 * 
 * @param {*} token 
 * @param {*} data 
 * @param {*} event 
 * @param {*} callback 
 */
function emit(token, data, callback) {
  if (!token || !data) {
    callback && callback(new Error('token 或 发送内容不存在'));
    return;
  }
  users.push(data.data)
  io.sockets.emit('newMsg', users)
}

exports.io = io;
exports.emit = emit;
```
