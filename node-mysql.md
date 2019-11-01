
> 如果想要在node中操作mysql，则需要先安装mysql模块

```js
npm i mysql
```

<br>

## 连接 MySQL
---

> 基本示例

```js
// 加载mysql模块
const mysql = require('mysql')
// 创建连接
const connection = mysql.createConnection({
  host: '127.0.0.1',
  user: 'root',
  password: '1234',
  database: 'demo'
})
// 开始连接(可以不写,query会自动连接)
connection.connect()
// 执行sql语句
let sql = 'SELECT 1+1 AS number'
connection.query(sql, (err, results) => {
  if (err) { throw err }
  console.log(results)
})
// 关闭连接
connection.end()
```

<br>

## 创建连接池
---

> 基本示例

```js
// 加载mysql模块
const mysql = require('mysql')
// 创建连接池
const pool = mysql.createPool({
  host: '127.0.0.1',
  user: 'root',
  password: '1234',
  database: 'demo',
  // 默认是10个
  connectionLimit: 10
})
// 获取可用的连接
pool.getConnection((err, connection) => {
  if (err) { throw err }
  // 执行sql语句
  let sql = 'SELECT * FROM `info`'
  connection.query(sql, (err, results) => {
    // 查询完毕后,释放回连接池
    connection.release()
    // 处理结果
    if (err) { throw err }
    console.log(results)
  })
})
```

<br>

## SELECT 查询数据
---

> 基本示例

```js
let sql = 'SELECT * FROM `info`'
// 执行sql语句
connection.query(sql, (err, results) => {
  if (err) { throw err }
  // 查询结果始终是数组
  console.log(results)
})
```

<br>

## INSERT INTO 插入数据
---

> 基本示例

```js
let obj = {
  nickname: 'ben',
  message: 'how are you'
}
let sql = 'INSERT INTO `info` (`nickname`,`message`) VALUES("'+obj.nickname+'","'+obj.message+'")'
// 执行sql语句
connection.query(sql, obj, (err, results) => {
  if (err) { throw err }
  console.log(results)
})
```

> 简洁语法

```js
let obj = {
  nickname: 'jack',
  message: 'i am fine'
}
let sql = 'INSERT INTO `info` SET ?'
// 执行sql语句
connection.query(sql, obj, (err, results) => {
  if (err) { throw err }
  console.log(results)
})
```
