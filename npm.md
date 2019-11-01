

## 区分 --save 与 --save-dev

> 其中前两个效果一样, 无论加不加--save, 都是保存到dependencies依赖项中

```bash
npm i jquery

npm i jquery --save
```

> 后两个则是把一些辅助开发工具保存到devDependencies依赖项中

```bash
npm i jquery --save-dev

npm i jquery -D
```

!> 这样做的目的是为了对包进行分类, 当项目上线的时候可以使用`npm install --production`只安装dependencies依赖项中的包

<br><br><br>

## 保存自动重启 node 服务器

`npm i -g nodemon`

```shell
// 启动入口文件
nodemon ./app.js
```

<br><br><br>

## 从本地缓存中下载 npm 包

`npm i express --cache-min 999999`

<br><br><br>

## http-server 快速启动

> 快速启动一个node测试服务器, 并且同一个局域网下可以访问

`npm i -g http-server`

```shell
hs -o -p 8080
```

<br><br><br>

## browser-sync 同步测试

> 用于同步测试, 当编辑器保存时, 浏览器会自动刷新

`npm i -g browser-sync`

```js
{
  "scripts": {
    "demo": "browser-sync start --server --files 'css/*.css, js/*.js, *.html'"
  }
}
```

<br><br><br>

## 配置 npm run dev

在`package.json`中添加如下代码

```js
"scripts": {
  "start": "node ./app.js",
  "dev": "nodemon --exec npm start"
},
```

