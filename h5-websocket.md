# websocket
---

> 即时通讯技术

?> websocket也是一种协议, 建立连接之后可以主动发请求并任意响应数据

websocket与ajax十分相似, 但是ajax只能是客户端主动请求, 并且建立连接之后, 一次请求只对应一次响应

<br>

## 原生 websocket
---

先安装一个包 `npm i ws -S`

##### **服务端**

```js
// 加载ws模块
const ws = require('ws')

// 监听8080端口
app.listen(8080, () => console.log(new Date()))

// 创建websocket服务器并监听8081
const wss = new ws.Server({port: 8081})

// 连接事件
wss.on('connection', client => {

  // 当有人连接时, 发送消息
  client.send('你好')

  // 接受客户端发来的数据
  client.on('message', data => {
    console.log(data)
  })

})
```

##### **客户端**

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>websocket</title>
</head>
<body>
  <script>

    // 与服务器建立连接
    const server = new WebSocket('ws://127.0.0.1:8081')

    // 连接成功事件
    server.onopen = () => {
      alert('连接成功了')

      // 客户端向服务端发送消息
      server.send('我是客户端, 我连接成功了')
    }

    // 收到消息事件
    server.onmessage = (e) => {
      console.log(e.data)
    }

  </script>
</body>
</html>
```

!> 但是我们在实际开发中一般不使用原生的websocket, 而是使用socket.io

<br><br>

## 使用 socket.io
---

socket.io是基于websocket进行了二次封装, 使其语法更佳简介

`npm i socket.io -S`

<br>

##### **服务端**

```js
// 加载模块
const http = require('http')
const express = require('express')
// 创建服务器
const app = express()
const server = http.createServer(app)

app.use(express.static('./node_modules'))

server.listen(8080)

// 传递server对象的目的是为让http协议与websocket共用一个端口
const io = require('socket.io')(server)

// 监听连接事件
io.on('connection', client => {

  // 接受消息
  client.on('名称', data => {
    console.log(data)
  })

  // 发送消息
  client.emit('名称', '内容')

  // 把消息发送给所有人
  io.emit('名称', '内容')

})
```

<br>

##### **客户端**

```html
<script src="/socket.io-client/dist/socket.io.js"></script>
<script>

  // 连接服务器
  const server = io()

  // 连接成功事件
  server.on('connect', () => {
    // ...
  })

  // 接收消息
  server.on('名称', (data) => {
    console.log(data)
  })

  // 发送消息
  server.emit('名称', '内容')

</script>
```

!> 前端需要引入`/node_modules/socket.io-client/dist/socket.io.js`文件
