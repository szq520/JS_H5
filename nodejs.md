
?> 用来方便地搭建快速的易于扩展的网络应用。Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效，非常适合运行在分布式设备的数据密集型的实时应用。

> Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境

- 实时应用：如在线聊天，实时通知推送等等（如socket.io）
- 分布式应用：通过高效的并行I/O使用已有的数据
- 工具类应用：海量的工具，小到前端压缩部署（如grunt），大到桌面图形界面应用程序
- 游戏类应用：游戏领域对实时和并发有很高的要求（如网易的pomelo框架）
- 利用稳定接口提升Web渲染能力
- 前后端编程语言环境统一：前端开发人员可以非常快速地切入到服务器端的开发（如著名的纯Javascript全栈式MEAN架构）

<br><br><br>

## 安装多版本 Node.js
---

NVM（Node version manager）是Node.js的版本管理软件，使用户可以轻松在Node.js各个版本间进行切换。适用于长期做 node 开发的人员或有快速更新node版本、快速切换node版本这一需求的用户

<br>

- 第一步, 使用git将源码克隆到本地的~/.nvm目录下，并检查最新版本

  - `yum install git -y`

```shell
git clone https://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```

<br>

- 第二步, 激活 NVM

  - `echo ". ~/.nvm/nvm.sh" >> /etc/profile`

  - `source /etc/profile`

<br>

- 第三步, 列出 Node.js 的所有版本(可选)

  - `nvm list-remote`

<br>

- 安装多个 Node.js 版本

  - 我选择了我本机环境和当前稳定版本

  - `nvm install v8.9.4`

  - `nvm install v8.11.4`

<br>

- 切换 Node.js 版本

  - 运行`nvm ls`可以查看已安装Node.js版本

  - 运行`nvm use v8.9.4`切换Node.js版本

!> 补充:`nvm help`可以查看帮助文档

<br>

- 部署项目

  - 运行`cd ~`回到家目录

  - `vim test.js`创建文件并打开
    - 如果没有vim, 则需要安装`yum install vim -y`

  - 接下来输入`i`进入编辑模式, 将如下代码粘贴进去

```javascript
// 加载http模块
const http = require('http')

// 创建服务器
const server = http.createServer()
// 监听客户端请求
server.on('request', (request, response) => {
  // 结束响应并返回结果
  response.end('hello node.js')
})

// 监听3000端口
server.listen(3000, () => {
  console.log('Server is running...')
})
```

- 接下来按`Esc`按钮，退出编辑模式，输入`:wq`保存并退出

- 最后输入`node ~/example.js &`运行项目并置于后台运行

当看到 `Server is running...` 的文字后，代表服务器已经运行成功了, 然后访问`IP:3000`即可

<br><br><br>

## 使用 pm2 启动项目
---

?> PM2是node进程管理工具，可以利用它来简化很多node应用管理的繁琐任务，如性能监控、自动重启、负载均衡等，而且使用非常简单

<br>

- 全局安装`npm i -g pm2`

  - 查看版本`pm2 -v`

- 启动项目`pm2 start server/bin/www`

  - 查看当前项目`pm2 list`

  - 查看日志`pm2 log`

  - 停止项目`pm2 stop server/bin/www`

<br><br><br>

## 配置 nginx 反向代理
---

> nginx的优势在负载均衡和静态文件处理

<br>

- 首先, 安装nginx

  - `yum install nginx -y`

<br>

- 安装完毕后, 找到nginx的配置文件

  - `find / -name nginx.conf`

    - 我这里显示是`/etc/nginx/nginx.conf`

<br>

- 接下来使用vim打开配置文件

  - `vim /etc/nginx/nginx.conf`

  - 按`i`进入编辑模式后, 配置虚拟主机

```shell
    server {
        listen       80 default_server;
        server_name  buuing.com;

        location / {
             #node.js应用的端口
             proxy_pass http://127.0.0.1:3000;
             root blog;
        }
    }
```

<br>

- 完成后按`Esc`键, 输入`:wq`保存并退出

- 最后重启nginx即可

  - `service nginx restart`


<br><br><br>

## Node.js 路由设计
---

这台服务器还略有些不足，于是我们加入了fs模块，让我们的node服务器可以拥有读取文件的能力。即在 `localhost:3000/` 的路由下，会把index.html这个页面展示出来

```javascript
// 加载http模块
const http = require('http')
// 加载fs模块(可以对文件进行操作)
const fs = require('fs')

// 创建服务器
const server = http.createServer()
// 监听客户端请求
server.on('request', (request, response) => {
  // 获取地址栏的路径
  const url = request.url
  // 请求 127.0.0.1:3000/ 时
  if (url === '/') {
    // 读取同一目录下的index.html文件
    fs.readFile('./index.html', (err, data) => {
      // 如果有错误先抛出
      if (err) { throw err }
      // 把读取到的数据响应给页面
      response.end(data)
    })
  } else {
    // 否则则返回404页面
    response.end('404 Not Found')
  }
})

// 监听端口
server.listen(3000, () => {
  console.log('Server is running...')
})
```

但此时还是有一些缺陷的，那就是读取一些静态文件时无法加载，比如请求 `./public/img/banner.jpg` 时会提示404 Not Found

<br><br><br>

## 开放静态资源目录
---

我们假设静态资源都放在public目录下，接下来我们再次进行改进代码，使这个服务器能识别这个公共目录

```javascript
// 加载http模块
const http = require('http')
// 加载fs模块(可以对文件进行操作)
const fs = require('fs')

// 创建服务器
const server = http.createServer()
// 监听客户端请求
server.on('request', (request, response) => {
  // 获取地址栏的路径
  const url = request.url
  // 请求 127.0.0.1:3000/ 时
  if (url === '/') {
    // 读取同一目录下的index.html文件
    fs.readFile('./index.html', (err, data) => {
      // 如果有错误先抛出
      if (err) { throw err }
      // 把读取到的数据响应给页面
      response.end(data)
    })
  } else if (url.indexOf('/public/') !== -1) {
    // 把public开放成静态资源目录
    fs.readFile('.' + url, (err, data) => {
      // 抛出错误
      if (err) { throw err }
      // 返回静态资源
      response.end(data)
    })
  } else {
    // 否则则返回404页面
    response.end('404 Not Found')
  }
})

// 监听端口
server.listen(3000, () => {
  console.log('Server is running...')
})
```
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <link rel="stylesheet" href="/public/css/main.css">
</head>
<body>
  <img src="/public/img/banner.jpg" alt="">
</body>
</html>
```

现在算是基本的完善了这个node服务器，并且我们认识到 node.js 的不同模块具有不同的能力，想要实现什么功能只需要加载相应的模块即可

