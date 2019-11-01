

## 安装脚手架
---

> 检查是否安装`node`和`npm`

可以分别使用`node -v`和`npm -v`命令查看版本

> 安装 vue-cli

```shell
npm i -g vue-cli
```

安装成功后同样也可以查看版本

```shell
vue -V
```

> 初始化 vue 项目

可以先进行查看可以使用的模板

```shell
vue list
```

然后选择其中一个进行初始化（其中webpack表示选择的模板名称，demo表示项目名称）

```shell
vue init webpack demo
```

稍微等待片刻会出现如下一堆选项

```shell
// 项目名称
? Project name demo
// 项目描述
? Project description demo
// 作者
? Author ldq
// 打包方式
? Vue build runtime
// 是否设置路由
? Install vue-router? Yes
// 是否使用eslint代码规范
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
// 单元测试
? Set up unit tests No
? Setup e2e tests with Nightwatch? No
// 使用npm 还是 yarn
? Should we run `npm install` for you after the project has been created? (recommended) npm
```

完成之后，会生成一个vue的基本框架，使用如下命令进入项目开始运行

```
cd demo
```
```
npm run dev
```

!> 我习惯在`package.json`中的`dev`命令里加上`--open`, 这样运行`dev`的时候会自动打开网页

现在vue脚手架就已经生成ok了

<br>
<br>
<br>

## 配置测试接口
---

- 第一步, 先在根目录下新建一个文件夹`db`

  - 把模拟的`data.json`数据放在该目录下面

  - 结构为`/db/data.json`

```js
{
  "code": "10000",
  "message": "success",
  "data": [
    {
      "goodsId": "1560",
      "goodsName": "oppo R17",
      "goodsPrice": 3499,
      "goodsImg": "/static/img/oppo.jpg"
    }, {
      "goodsId": "5781",
      "goodsName": "荣耀 10",
      "goodsPrice": 2299,
      "goodsImg": "/static/img/rongyao.jpg"
    }, {
      "goodsId": "8946",
      "goodsName": "魅族 16",
      "goodsPrice": 3378,
      "goodsImg": "/static/img/meizu.jpg"
    }, {
      "goodsId": "6845",
      "goodsName": "小米 MIX 2S",
      "goodsPrice": 2699,
      "goodsImg": "/static/img/xiaomi.jpg"
    }
  ]
}
```

<br>

- 第二步, 找到`/build/webpack.dev.conf.js`文件

> 在`const portfinder = require('portfinder')`后面添加如下代码

```js
const express = require('express')
const testData = require('../db/data.json')

const app = express()
const router = express.Router()
app.use('/api', router)
```

> 在`devServer: {`里面添加如下代码, 注意加逗号

```js
before(app) {
  app.get("/api/test", (req, res, next) => {
    res.json(testData)
  })
},
```

<br>

!> 现在代码变成如下样子

```js
'use strict'
const utils = require('./utils')
const webpack = require('webpack')
const config = require('../config')
const merge = require('webpack-merge')
const path = require('path')
const baseWebpackConfig = require('./webpack.base.conf')
const CopyWebpackPlugin = require('copy-webpack-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const FriendlyErrorsPlugin = require('friendly-errors-webpack-plugin')
const portfinder = require('portfinder')
const express = require('express')
const testData = require('../db/data.json')

const app = express()
const router = express.Router()
app.use('/api', router)

const HOST = process.env.HOST
const PORT = process.env.PORT && Number(process.env.PORT)

const devWebpackConfig = merge(baseWebpackConfig, {
  module: {
    rules: utils.styleLoaders({ sourceMap: config.dev.cssSourceMap, usePostCSS: true })
  },
  // cheap-module-eval-source-map is faster for development
  devtool: config.dev.devtool,

  // these devServer options should be customized in /config/index.js
  devServer: {
    before(app) {
      app.get("/api/test", (req, res, next) => {
        res.json(testData)
      })
    },
    clientLogLevel: 'warning',
    historyApiFallback: {
      rewrites: [
        { from: /.*/, to: path.posix.join(config.dev.assetsPublicPath, 'index.html') },
      ],
    },
    hot: true,
    // 后面省略一堆代码...
```

<br>

- 最后`npm run dev`重启即可尝试访问接口

```js
axios.get('/api/test')
  .then(res => {
    console.log(res)
  })
```

<br>