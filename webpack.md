
## 实时打包编译
---

- 安装最基础的webpack包`npm i webpack webpack-cli -D`
- 监听代码状态实时刷新`npm i webpack-dev-server -D`
- 将index.html托管到内存中`npm i html-webpack-plugin -D`

目录结构为

```
├── dist 打包后的代码
├── src 源代码
│   ├── index.js
│   └── index.html
├── package.json
└── webpack.config.js
```

> 在`package.json`文件中如下代码

```js
"scripts": {
  "dev": "webpack-dev-server --open"
},
"devDependencies": {
  "html-webpack-plugin": "^3.2.0",
  "webpack": "^4.27.1",
  "webpack-cli": "^3.1.2",
  "webpack-dev-server": "^3.1.10"
},
```

> 在`webpack.config.js`文件中加入如下配置

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  // 选择是开发环境还是身产环境 development | production
  mode: 'development',
  plugins: [
    // 在内存中生成index.html
    new HtmlWebpackPlugin({
      // 源文件
      template: path.join(__dirname, './src/index.html'),
      // 目标文件
      filename: 'index.html'
    })
  ]
}
```
