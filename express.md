# Express
---

> 基于 Node.js 平台，快速、开放、极简的 web 开发框架。

```shell
npm install express --save
```

### Web 应用 {docsify-ignore}

- Express 是一个基于 Node.js 平台的极简、灵活的 web 应用开发框架，它提供一系列强大的特性，帮助你创建各种 Web 和移动设备应用。

### API {docsify-ignore}

- 丰富的 HTTP 快捷方法和任意排列组合的 Connect 中间件，让你创建健壮、友好的 API 变得既快速又简单。

### 性能 {docsify-ignore}

- Express 不对 Node.js 已有的特性进行二次抽象，我们只是在它之上扩展了 Web 应用所需的基本功能。

<br><br><br>

## 使用 Express
---

```javascript
// 加载express模块
const express = require('express')
// 创建服务器实例
const app = express()
// 创建路由实例
const router = express.Router()
// 路由方法
router.get('/', (req, res, next) => {
  res.send('hello express')
})
// 挂载路由
app.use(router)
// 监听3000端口
app.listen(3001, () => console.log(new Date()))
```

<br><br><br>

## 中间件
---

> 没有任何限制 `app.use(function)`

```javascript
// 只有后面的路由才会生效
app.use((req, res, next) => {
  // 执行你想要的逻辑
  console.log('hello')
  // 继续执行后面的代码
  next()
})
```

> 限制路由 `app.use(path, function)`

```javascript
// 只有以/admin开头的请求才会打印hello
app.use('/admin', (req, res, next) => {
  // 执行你想要的逻辑
  console.log('hello')
  // 继续执行后面的代码
  next()
})
```

> 限制路由和请求方法 `app.METHODS(path, function)`

```javascript
// 只有以get方式请求/article开头的路径时才会打印hello
app.get('/article/:ID', (req, res, next) => {
  // 执行你想要的逻辑
  console.log('hello')
  // 继续执行后面的代码
  next()
})
```

> 多个处理函数 `app.use(path, function, function)`

```javascript
app.use('/', (req, res, next) => {
  // 执行第一个函数的逻辑
  console.log('first')
  // 继续执行后面的代码
  next()
}, (req, res, next) => {
  // 执行第二个函数的逻辑
  console.log('second')
  // 继续执行后面的代码
  next()
})
```

<br><br><br>

## 中间件的基本使用
---

###### 使用内置中间件开放静态资源目录

```js
// 开放静态资源目录
app.use('/node_modules', express.static('./node_modules/'))
app.use('/public', express.static('./public/'))
```

---

###### 使用router进行路由管理

```js
// 创建路由实例
const router = express.Router()
// 挂载路由容器到app中,使路由生效
app.use(router)
```

---

###### 使用app.use中间件处理错误

```js
// 配置错误处理中间件
app.use((err, req, res, next) => {
  res.status(500).send({
    error: err.message
  })
})
```

只需要在后面的函数中`return next(err)`即可

---

###### 使用art-template模板引擎渲染页面和数据

`npm i art-template express-art-template`

```js
// 配置模板引擎
app.engine('html', require('express-art-template'))
```

---

###### 使用body-parser处理表单请求

`npm i body-parser`

```js
// 配置 body-parser
app.use(bodyParser.urlencoded({ extended: true }))
// app.use(bodyParser.json())
```

---

###### 使用mysql数据库模块来处理数据交互

`npm i mysql`

```js
// 加载mysql模块
const mysql = require('mysql')
// 创建连接池
const pool = mysql.createPool(dbConfig)
// 封装私有的执行sql方法
exports.query = (...args) => {
  const callback = args.pop()
  // 从连接池中获取连接
  pool.getConnection((err, connection) => {
    if (err) {
      return callback(err, undefined)
    }
    // 执行sql语句
    connection.query(...args, (err, results) => {
      // 释放连接
      connection.release()
      if (err) {
        return callback(err, undefined)
      }
      callback(null, results)
    })
  })
}
```

---

###### 使用MD5进行数据加密

`npm i blueimp-md5`

```js
// 加载MD5模块
const md5 = require('blueimp-md5')
// 数据加密
data.password = md5(data.password)
```

---

###### 使用session存储用户登录状态, 并使用express-mysql-session持久化存储登录状态

`npm i express-session express-mysql-session`

```js
// 加载session模块
const session = require('express-session')
const MySQLStore = require('express-mysql-session')(session)
// 配置信息
const options = {
  host: '127.0.0.1',
  port: 3306,
  user: 'root',
  password: '1234',
  database: 'test'
}
// 连接到数据库存储登录状态
const sessionStore = new MySQLStore(options)
// 配置session开启会话
app.use(session({
  // 自定义加密字符串
  secret: 'buuing.com',
  // 持久化存储
  store: sessionStore,
  // 配置cookie
  cookie: {
    // 过期时间(单位为毫秒)
    maxAge: 1000*60*60*12*1
  },
  resave: false,
  // 使用session才会配发秘钥
  saveUninitialized: false
}))
// 添加用户登录状态
req.session.user = user
```

---

###### 使用app.locals全局模板对象,来存储session中的用户信息

```js
app.use((req, res, next) => {
  app.locals.user = req.session.user
})
```

---

###### 使用jquery-form处理表单数据

`npm i jquery-form`

```js
$('#form').on('submit', function (e) {
  e.preventDefault()
  $(this).ajaxSubmit((res) => {
    console.log(res)
  })
})
```

---

###### 使用moment时间类库处理时间

`npm i moment`

```js
// 加载moment模块
const moment = require('moment')
// 调用
moment().format('YYYY-MM-DD HH:mm:ss')
```

---

###### 使用第三方中间件response-time记录响应时间

`npm i response-time`

```js
// 加载模块
const responseTime = require('response-time')
// 会自动在http响应头中加入响应时间相关信息
app.use(responseTime())
```

---

###### 使用esLint代码风格强校验工具

`npm i eslint nodemon --save-dev`

`./node_modules/.bin/eslint --init`

在package.json文件中加入如下代码, 使每次重启服务器都进进行一次代码校验

```json
"scripts": {
  "prestart": "eslint ./",
  "start": "node ./app.js",
  "dev": "nodemon --exec npm start"
},
```

<br><br><br>

## 第三方中间件
---

> 官方中间件资源：[http://expressjs.com/en/resources/middleware.html](http://expressjs.com/en/resources/middleware.html)

!> 为了保持 Express 本身极简灵活的特性，开发人员可以根据自己的需求去灵活的定制

<table>
<thead>
<tr>
<th style="width: 165px;">Middleware module</th>
<th>Description</th>
<th style="width: 200px;">Replaces built-in function (Express 3)</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/body-parser.html" target="_blank">body-parser</a></td>
<td>Parse HTTP request body. See also: <a href="https://github.com/raynos/body" target="_blank">body</a>, <a href="https://github.com/visionmedia/co-body" target="_blank">co-body</a>, and <a href="https://github.com/stream-utils/raw-body" target="_blank">raw-body</a>.</td>
<td>express.bodyParser</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/compression.html" target="_blank">compression</a></td>
<td>Compress HTTP responses.</td>
<td>express.compress</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/connect-rid.html" target="_blank">connect-rid</a></td>
<td>Generate unique request ID.</td>
<td>NA</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/cookie-parser.html" target="_blank">cookie-parser</a></td>
<td>Parse cookie header and populate <code>req.cookies</code>. See also <a href="https://github.com/jed/cookies" target="_blank">cookies</a> and <a href="https://github.com/jed/keygrip" target="_blank">keygrip</a>.</td>
<td>express.cookieParser</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/cookie-session.html" target="_blank">cookie-session</a></td>
<td>Establish cookie-based sessions.</td>
<td>express.cookieSession</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/cors.html" target="_blank">cors</a></td>
<td>Enable cross-origin resource sharing (CORS) with various options.</td>
<td>NA</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/csurf.html" target="_blank">csurf</a></td>
<td>Protect from CSRF exploits.</td>
<td>express.csrf</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/errorhandler.html" target="_blank">errorhandler</a></td>
<td>Development error-handling/debugging.</td>
<td>express.errorHandler</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/method-override.html" target="_blank">method-override</a></td>
<td>Override HTTP methods using header.</td>
<td>express.methodOverride</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/morgan.html" target="_blank">morgan</a></td>
<td>HTTP request logger.</td>
<td>express.logger</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/multer.html" target="_blank">multer</a></td>
<td>Handle multi-part form data.</td>
<td>express.bodyParser</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/response-time.html" target="_blank">response-time</a></td>
<td>Record HTTP response time.</td>
<td>express.responseTime</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/serve-favicon.html" target="_blank">serve-favicon</a></td>
<td>Serve a favicon.</td>
<td>express.favicon</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/serve-index.html" target="_blank">serve-index</a></td>
<td>Serve directory listing for a given path.</td>
<td>express.directory</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/serve-static.html" target="_blank">serve-static</a></td>
<td>Serve static files.</td>
<td>express.static</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/session.html" target="_blank">session</a></td>
<td>Establish server-based sessions (development only).</td>
<td>express.session</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/timeout.html" target="_blank">timeout</a></td>
<td>Set a timeout period for HTTP request processing.</td>
<td>express.timeout</td>
</tr>
<tr>
<td><a href="http://expressjs.com/en/resources/middleware/vhost.html" target="_blank">vhost</a></td>
<td>Create virtual domains.</td>
<td>express.vhost</td>
</tr>
</tbody>
</table>


<br><br><br>

## 获取数据的三种方式

> req.query 获取地址栏查询字符串数据

```
127.0.0.1/?s=string

console.log(req.query.s)
// 打印结果为string
```

> req.params  获取动态路径参数

```
// 假设路由为/active/:Id
127.0.0.1/active/3

// 打印结果为3
console.log(req.params.Id)
```

> req.body  获取表单请求体数据

主要用于接收前端post过来的数据

```js
// 现有前端这样一段代码
$.ajax({
  url: '/active/creat',
  type: 'post',
  data: {
    title: '标题',
    content: '内容'
  },
  success: function (res) {
    console.log(res)
  }
})
```

前端向/active/creat这个接口发送一个数据

```
console.log(req.body)
// 打印结果为{ title: '标题', content: '内容' }
```