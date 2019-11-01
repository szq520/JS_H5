
## mpvue 是一个使用 Vue.js 开发小程序的前端框架 {docsify-ignore}
---

- `mpvue`全家桶

  - 搭建`mpvue`基础框架
  - `mpvue-entry`[自动生成构建入口，避免编写大量重复的 main.js 文件](#/mpvue?id=mpvue-entry-自动生成构建入口)
  - `mpvue-router-patch`[模拟vue-router的路由跳转方法]()

- 集成脚手架`vue init F-loat/mpvue-quickstart my-project`

<br>

### 搭建 mpvue 基础框架
---

使用`vue-cli`初始化一个`mpvue`项目

```
vue init mpvue/mpvue-quickstart my-project
```

可以自行封装`ajax`方法

```js
/**
 * ldq - 封装公共的ajax请求方法
 * @param { Object } options
 * @param { Function } callBack
 */
export function Ajax (options, callBack = function () {}) {
  wx.showLoading({title: '请求中...', mask: true})
  const {url, method = 'GET', data = {}} = options
  return new Promise((resolve, reject) => {
    wx.request({
      url,
      data,
      method,
      header: {
        'content-type': 'application/json'
      },
      success (res) { resolve(res) },
      fail (err) { reject(err) },
      complete (res) {
        setTimeout(() => {
          wx.hideLoading()
          callBack && callBack(res)
        }, 1000)
      }
    })
  })
}

export default {
  Ajax
}
```

<br>

### mpvue-entry 自动生成构建入口
---


- 安装`npm i mpvue-entry@next -D`

- 在`webpack.base.conf.js`文件中修改以下代码

```js
const MpvueEntry = require('mpvue-entry') // 新增

...

module.exports = {
  entry: MpvueEntry.getEntry('src/app.json'), // 替换
  ...
  plugins: [
    new MpvueEntry(), // 新增
    ...
  ]
}
```

- 如果是官网模板则需要在`webpack.base.conf.js`中去掉如下代码

```js
module.exports = {
  plugins: [
    new CopyWebpackPlugin([{
      from: '**/*.json',
      to: ''
    }], {
      context: 'src/'
    }),
    ...
  ]
}
```

- 还需要在`pages`下面加一个`pages.js`文件

```js
module.exports = [

]
```
