
## 安装 express-generator
---

?> 通过应用生成器工具 express 可以快速创建一个应用的骨架

<br>

- 第一步, 通过npm进行全局安装

  - `npm i -g express-generator`

  - 安装成功后可以通过`express --version`查看安装的版本

<br>

- 第二步, 快速生成项目

  - 在根目录下输入`express server`即可创建项目

  - 其目录结构为

```
├── app.js
├── bin 可执行文件
│   └── www
├── package.json
├── public 静态资源
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes 路由
│   ├── index.js
│   └── users.js
└── views 视图
    ├── error.jade
    ├── index.jade
    └── layout.jade
```

<br>

- 最后`cd server`进入目录, 通过`npm install`进行安装依赖

  - 可通过`node bin/www`命令启动项目

<br>
<br>
<br>

## 如何渲染html格式文件

!> 这里需要注意, 视图目录中的文件是`.jade`格式的文件, 这种语法虽然高效, 但是可读性比较差, 可以通过以下方式修改成`.html`格式的文件

- 先`npm i ejs`安装一个依赖

- 再从`app.js`文件中找到`app.set('views', path.join(__dirname, 'views'));`这行代码, 在其前后进行编辑

```js
var ejs = require('ejs')

...

app.set('views', path.join(__dirname, 'views'));
app.engine('.html', ejs.__express)
app.set('view engine', 'html');
```

<br>
<br>
<br>

## vue静态资源加载失败

- 把`public`改成`views`, 然后把打包后的文件全部放在`views`目录下

```js
// app.use(express.static(path.join(__dirname, 'public')));
app.use(express.static(path.join(__dirname, 'views')));
```

<br>
<br>
<br>

## 使用jwt实现登录态

- 安装`npm i jsonwebtoken`

  - 方法`jwt.sign('规则', '加密字符串', '过期时间', '回调函数')`

```js
const jwt = require('jsonwebtoken')

...

const rule = {
  id: doc._id,
  nickname: doc.nickname
}
jwt.sign(rule, 'ldq', { expiresIn: 43200 }, (err, token) => {
  if (err) return console.log(err.message)
  res.status(200).json({
    status: '10000',
    message: '登录成功',
    results: doc,
    token: 'Bearer ' + token
  })
})
```

- 安装`npm i passport-jwt passport`

  - 在`app.js`中进行初始化

```js
const mongoose = require('mongoose')
const passport = require('passport')
const JwtStrategy = require('passport-jwt').Strategy,
    ExtractJwt = require('passport-jwt').ExtractJwt
const Users = mongoose.model('users')

...

// 初始化passport
app.use(passport.initialize())



const opts = {}
opts.jwtFromRequest = ExtractJwt.fromAuthHeaderAsBearerToken();
opts.secretOrKey = '加密字符串';

passport => {
  passport.use(new JwtStrategy(opts, (jwt_payload, done) => {
    console.log(jwt_payload)
    // Users.findOne({id: jwt_payload.sub}, function(err, user) {
    //   if (err) {
    //     return done(err, false);
    //   }
    //   if (user) {
    //     return done(null, user);
    //   } else {
    //     return done(null, false);
    //     // or you could create a new account
    //   }
    // })
  }))
}
```