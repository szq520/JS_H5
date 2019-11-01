# 豆瓣测试接口
---

> 感谢豆瓣为我们提供的开放api, 在这里仅用于个人测试使用, 侵删

<br>

- [获取电影Top250](javascript:;)

  - 接口地址 `https://api.douban.com/v2/movie/top250`

  - 请求方式 `get`

  - 请求参数

    - `start` *数据的开始项*
    - `count` *单页条数*

  - 示例

    - 获取电影Top250第一页10条数据：`https://api.douban.com/v2/movie/top250?start=0&count=10`

<hr>

- [获取正在热映的电影](javascript:;)

  - 接口地址 `https://api.douban.com/v2/movie/in_theaters`

  - 请求方式 `get`

  - 请求参数

    - `start` *数据的开始项*
    - `count` *单页条数*
    - `city` *城市*

  - 示例

    - 获取广州热映电影第一页10条数据：`https://api.douban.com/v2/movie/in_theaters?city=广州&start=0&count=10`

<hr>

- [电影搜索](javascript:;)

  - 接口地址 `https://api.douban.com/v2/movie/search`

  - 请求方式 `get`

  - 请求参数

    - `start` *数据的开始项*
    - `count` *单页条数*
    - `q` *要搜索的电影关键字*
    - `tag` *要搜索的电影的标签*

  - 示例

    - 搜索电影《神秘巨星》：`https://api.douban.com/v2/movie/search?q=神秘巨星&start=0&count=10`

    - 搜索喜剧类型的电影：`https://api.douban.com/v2/movie/search?tag=喜剧&start=0&count=10`

<hr>

- [电影详情](javascript:;)

  - 接口地址 `https://api.douban.com/v2/movie/subject/:id`

  - 请求方式 `get`

  - 请求参数

    - `id` *电影id*

  - 示例

    - 《神秘巨星》的id为：26942674的详细信息：`https://api.douban.com/v2/movie/subject/26942674`

<br>
<br>
<br>

## 原生 ajax
---

```js
// get方式
const xhr = new XMLHttpRequest
xhr.open('get', '请求接口')
xhr.send()
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(xhr.responseText)
  }
}

// post方式
const xhr = new XMLHttpRequest
xhr.open('post', '请求接口')
xhr.setRequestHeader('application/x-www-form-urlencoded')
xhr.send('xx=xxx&xx=xxx')
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(xhr.responseText)
  }
}
```

<br>
<br>
<br>

## jQuery 中的 ajax
---

```js
$.ajax({
  url: '请求接口',
  type: '请求方式',
  // 请求参数
  data: {
    xx: 'xxx',
    xx: 'xxx'
  },
  // jsonp跨域 (可选)
  dataType: 'jsonp',
  // 成功回调
  success: function (res) {
    console.log(res)
  },
  // 失败回调
  error: function (err, msg) {
    console.log(msg)
  }
})
```

<br>
<br>
<br>

## jquery-form 封装 ajax
---

```html
<form id="form" action="请求接口" method="提交方式">
  <input type="text" name="message">
  <button type="submit">提交</button>
</form>
```

```js
$('#form').on('submit', function (e) {
  // 阻止默认提交事件
  e.preventDefault()
  // 自动获取表单信息并提交
  $(this).ajaxSubmit({
    // 成功回调
    success: function (res) {
      console.log(res)
    },
    // 失败回调
    error: function (err) {
      console.log(err)
    }
  })
})
```

<br><br><br>

## vue-resource
---

- 相关配置

```js
new Vue({
  el: '#app',

  data() {
    return {

    }
  },

  mounted() {
    // 全局拦截器
    Vue.http.interceptors.push((request, next) => {
      // ... 
      next(res => {
        return res
      })
    })
  },

  http: {
    root: 'http://localhost:3000'
  },

  methods: {
    // ...
  }
})
```

- 请求方式

```js
// get请求
get () {
  this.$http.get('/db.json', {
    // 参数
    params: {
      page: '1'
    },
    // 请求头
    headers: {
      token: 'k1r5th1er6hg1e'
    }
  }).then(res => {
      console.log(res)
    }, err => {
      console.log(err)
    })
},

post () {
  this.$http.post('/db.json', {
    page: '1'
  }, {
    headers: {
      token: 'k1r5th1er6hg1e'
    }
  }).then(res => {
      console.log(res)
    }, err => {
      console.log(err)
    })
},

jsonp () {
  this.$http.jsonp('/db.json').then(res => {
    console.log(res)
  })
},

http () {
  this.$http({
    url: 'db.json',
    params: {
      page: '1'
    },
    headers: {
      token: 'k1r5th1er6hg1e'
    },
    timeout: 30,
    before () {
      console.log('在发送请求之前执行')
    }
  }).then(res => {
    console.log(res)
  })
}
```

<br>
<br>
<br>

## axios
---

- 安装axios

```
npm i axios
```

> 简单使用

```js
mounted () {
  // 全局拦截器, 拦截请求
  axios.interceptors.request.use(config => {
    console.log('将要发送请求')
    return config
  })
  // 全局拦截器, 拦截响应
  axios.interceptors.response.use(response => {
    console.log('将要得到回应')
    return response
  })
},

methods: {
  // get请求
  get() {
    axios.get('./db.json', {
      // 参数
      params: {
        page: '1'
      },
      // 请求头
      headers: {
        token: 'k1r5th1er6hg1e'
      }
    }).then(res => {
        console.log(res)
      }).catch(err => {
        console.log(err)
      })
  },

  post() {
    axios.post('./db.json', {
      page: '1'
    }, {
      headers: {
        token: 'k1r5th1er6hg1e'
      }
    }).then(res => {
        console.log(res)
      }).catch(err => {
        console.log(err)
      })
  },

  http () {
    axios({
      url: './db.json',
      method: 'get',
      // 如果是post请求, 需要在data定义参数
      data: {
        page: '1'
      },
      // 如果是get请求, 需要在params里面定义
      params: {
        page: '1'
      },
      headers: {
        token: 'k1r5th1er6hg1e'
      },
    }).then(res => {
      console.log(res)
    })
  }
}
```

<br>
<br>
<br>

## 面试题: get 与 post 的区别
---

作为一道在北京面试题中已经问烂了的题目, 困扰了我很久, 我心生疑惑. get不就是get, post不就是post吗, 还能翻出花来? 对此我怨念颇深...

<br>

!> `答案一` 也就是我最初的回答, 但显然大部分的面试官都不满意

- 浏览器刷新或后退时, post表单会被重新提交

- get数据有2kb的长度限制, post没有限制

- get参数在url中可见, 而post则更加安全一些

<br>

!> `答案二` ajax中的get请求在IE浏览器下, 会出现缓存! 而post则不会

网页第一次加载时, 会从服务器下载img, css, js等静态资源. 当请求成功后会在本地临时存储起来, 以减少对服务器的耗损和用户的等待时间, 这也就是为什么第二次打开网页会快很多的原因

> 但是问题来了

在IE浏览器中, 当get请求的`url地址跟之前一模一样`的情况下, 则会去获取之前缓存好的数据

> 解决办法

- [1. 给每一次的get请求都添加一个随机值](javascript:;)
  - 可以是内置方法`Math.random()`随机数
  - 又或者使用`new Date().getTime()`时间戳

  - 当每一次的get请求的url都不一样时, 浏览器自然无法产生缓存

<br>

- [2. 设置 header 请求头](javascript:;)
  - `xhr.setRequestHeader('If-Modified-Since','0')`

  - 这样会自动在请求头中添加一个叫做`If-Modified-Since`的时间参数, 与服务端资源的最后修改时间进行对比, 如果不一致则会获取新的资源

<br>

- [3. 可以让后端在服务器设置禁用缓存](javascript:;)
  - 比如php可以`header("Cache-Control:no-cache,must-revalidate");`

  - ...

<br>

!> `答案三` GET产生一个TCP数据包, POST产生两个TCP数据包

- [HTTP的底层是TCP/IP, 也就是说get和post本质上来讲, 都是TCP链接](javascript:;)
  - 对于get请求: 浏览器会把`http header`和`data`一并发送出去, 然后服务器响应200(返回数据)

  - 而对于post来讲: 浏览器先发送`header`, 服务器响应`100 continue`, 浏览器再发送`data`, 服务器响应200(返回数据)

  - 虽然看似post比get多走一次TCP链接, 但是在网络不稳定的情况下, post在发送数据的完整性上来讲, 要可靠得多

  - 还有一个坑! `并不是所有浏览器的post都会发送两次包`, `Firefox`就只发送一次

<br><br><br>

## 还有重要的同源与跨域
---

#### 什么是同源策略

同源策略是一种约定,浏览器为了保证数据的安全,规定只有在域名,协议,端口三者一致的情况下,才能进行数据的访问

!> 所有支持js的浏览器都会使用同源策略

<br>

#### 什么是跨域

> 常用的跨域几种方式

- [jsonp跨域](javascript:;)

- [proxy代理跨域](javascript:;)

- [cors跨域](javascript:;)
