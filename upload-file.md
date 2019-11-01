
### 获取文件对象
---

!> 需要注意的是, 文件对象只有在`onchange`的时候才能获取到

<br>

> 示例 普通html页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <div>
    <!-- 文件对象只有change事件可以获取到, 点击事件不行 -->
    <input type="file" onchange="uploadFiles(this)">
  </div>
  <script>
    // 在方法中把当前的标签传递过来
    function uploadFiles(input) {
      // 获得的将会是一个对象, 但是依然可以通过files[0]的方式获取第一个
      console.log(input.files)
    }
  </script>
</body>
</html>
```

> 示例 在vue中

```html
<template>
  <div>

  </div>
</template>
```

<br>

### 图片预览
---

- 预览图片需要先获取到文件对象的url地址, 再付给img标签显示

- 如果想要先预览再决定是否上传, 那么需要一个`公共变量存储`起来, 因为文件对象只有在`onchange`的时候才能获取到

```html
<input type="file" @change="doUpload($event)" accept="image/*" />
<img class="upImg" :src="imgUrl" />
```

```js
getObjectURL (file) {
  const url = null
  if (window.createObjectURL!=undefined) {
    // basic
    url = window.createObjectURL(file)
  } else if (window.URL!=undefined) {
    // mozilla(firefox)
    url = window.URL.createObjectURL(file)
  } else if (window.webkitURL!=undefined) {
    // webkit or chrome
    url = window.webkitURL.createObjectURL(file)
  }
  return url
},
doUpload (e) {
  // 获取要显示预览的img标签
  const img = document.querySelector(".upImg")
  this.currFile = e.target.files[0]
  this.imgUrl = this.getObjectURL(e.target.files[0])
}
```

<br>

### 上传图片
---

> 通过`FormData`上传

- 如果只上传一个图片, 那只需要`append`一个文件对象即可

- 如果要上传多个, 那需要循环`append`

```js
// 上传一个图片
uploadFile (files) {
  const formData = new FormData()
  formData.append('file', files[0])
  this.axios.post('接口地址', formData).then(res => {
    console.log(res)
  })
}

// 上传多个图片
uploadFiles (files) {
  const formData = new FormData()
  
  formData.append('file', files[0])
  this.axios.post('接口地址', formData).then(res => {
    console.log(res)
  })
}
```

<br>

### 下载二进制文件

```js
this.axios({
  method: "get",
  url: `/CORPMS/api/download/file/${item.FileId}`,
  responseType: "blob",
  headers: { "Content-Type": "application/x-www-form-urlencoded" }
}).then(res => {
  console.log(res)
  if (res.data) {
    var blob = new Blob([res.data], { type: res.type })
    var name = res.headers["content-disposition"]
    //var filename=decodeURI(res.headers['content-disposition'].indexOf('=') + 1)
    var filename = name.substr(name.indexOf("=") + 1)
    if (window.navigator.msSaveOrOpenBlob) {
      navigator.msSaveBlob(blob, filename)
    } else {
      var a = document.createElement("a")
      a.download = filename
      a.href = window.URL.createObjectURL(blob)
      a.click()
    }
  }
})
```
