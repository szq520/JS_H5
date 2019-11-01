
## Window 对象
---

?> Window 对象表示浏览器中打开的窗口

##### **属性**

```js
// 返回窗口是否已被关闭
window.closed

// 返回窗口的文档显示区的高度
window.innerHeight
// 返回窗口的文档显示区的宽度
window.innerWidth

// 返回窗口的外部高度
window.outerHeight
// 返回窗口的外部宽度
window.outerWidth

// 设置或返回当前页面相对于窗口显示区左上角的 X 位置
window.pageXOffset
// 设置或返回当前页面相对于窗口显示区左上角的 Y 位置
window.pageYOffset
```

##### **方法**

```js
// 显示带有一段消息和一个确认按钮的警告框
alert()

// 显示带有一段消息以及确认按钮和取消按钮的对话框
confirm()

// 显示可提示用户输入的对话框
prompt()

// 关闭浏览器窗口
close()

// 打开一个新的浏览器窗口或查找一个已命名的窗口
open()

// 按照指定的像素值来滚动内容
scrollBy()

// 把内容滚动到指定的坐标
scrollTo()

// 按照指定的周期（以毫秒计）来调用函数或计算表达式
setInterval()

// 在指定的毫秒数后调用函数或计算表达式
setTimeout()
```

<br>
<br>
<br>

## Navigator 对象
---

?> Navigator 对象包含有关浏览器的信息

##### **属性**

```js
// 返回浏览器的代码名
window.navigator.appCodeName

// 返回浏览器的次级版本
window.navigator.appMinorVersion

// 返回浏览器的名称
window.navigator.appName

// 返回浏览器的平台和版本信息
window.navigator.appVersion

// 返回当前浏览器的语言
window.navigator.browserLanguage

// 返回指明浏览器中是否启用cookie的布尔值
window.navigator.cookieEnabled

// 返回浏览器系统的CPU等级
window.navigator.cpuClass

// 返回指明系统是否处于脱机模式的布尔值
window.navigator.onLine

// 返回运行浏览器的操作系统平台
window.navigator.platform
```

<br>
<br>
<br>

## History 对象
---

?> History 对象包含用户（在浏览器窗口中）访问过的 URL

##### **方法**

```js
// 后退
back()
// 前进
forward()
// 指定历史记录
go()
```

<br>
<br>
<br>

## Location 对象
---

```js
// 当页面地址(主要进行跳转操作)
location.href

// 下面两种也可以进行跳转
location.assign('baidu.com')
location.replace('baidu.com')

// 刷新当前页面
location.reload()

// 当前页面哈希值
location.hash

// 域名+端口号
location.host

// 域名
location.hostname

// 当前文件路径
location.pathname

// 端口
location.port

// 协议
location.protocol

// 问号后面搜索内容
location.search
```

<br><br><br>

## setInterval&ensp;定时器
---

#### 循环定时器

> setInterval(function, time) 需要两个参数

第一个参数是方法，第二个参数是时间，表示在每隔time毫秒就会执行一次function

```js
// 定时器会返回一个id值
var timeId = setInterval(function () {
  console.log(this)
}, 1000)
```

直到清除该定时器为止

```js
clearInterval(timeId)
```

<br>

#### 一次性定时器

> setTimeout(function, time) 使用方法同上

```js
// 定时器会返回一个id值
var timeId = setTimeout(function () {
  console.log(this)
}, 1000)
```

即使是一次性定时器也需要清除

```
clearTimeout(timeId)
```

<br>

#### 案例：单页面展示多个倒计时

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="first"></div>
  <div id="second"></div>
  <div id="third"></div>
  <script>

  function timeDown(id, time) {
    // 如果时间小于0, 则不执行该函数
    if (time <= 0) return
    // 获取指定id的对象
    var Obj = document.querySelector('#'+id)
    // 封装函数
    var fn = () => {
      // 定义天数时分秒
      var d = Math.floor( time / 86400 ),
        h = Math.floor( (time % 86400) / 3600 ),
        m = Math.floor( (time % 3600) / 60 ),
        s = Math.floor( time % 60 )
      // 如果时分秒小于10, 则拼接0
      h = h < 10 ? '0'+h : h
      m = m < 10 ? '0'+m : m
      s = s < 10 ? '0'+s : s
      Obj.innerHTML = d+'天'+h+'小时'+m+'分钟'+s+'秒'
      time--
      // 如果time归零, 则停止计时器
      if (time <= 0) {
        clearInterval(timeId)
        Obj.innerHTML = '开始抢购'
      }
    }
    // 先调用一次
    fn()
    // 然后开始定时器
    var timeId = setInterval(fn, 1000)
  }

  timeDown('first', 10)
  timeDown('second', 5000)
  timeDown('third', 90000)

  </script>
</body>
</html>
```

<br><br><br>

## cookie-session
---

#### 基于cookie-session的认证方式的缺陷

- session默认是内存存储, 一旦重启就会丢失数据
- 当内存中的session数据量过大时, 需要扩容服务器
- cookie-session的认证方式只针对浏览器生效
- 由于session是基于cookie的, 同源下的其他请求, 客户端也会把cookie带到服务器  

!> 如果资源在同一个域名下, 加载一张图片,也会把cookie信息带过去, 这样是没有意义的, 解决的办法是给静态资源一个子级域名

<br>

#### 基于json web token鉴权机制
https://www.jianshu.com/p/576dbf44b2ae
http://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html