
## web页面使用支付宝-支付流程
---

首先是后端给一个接口, 调用之后拿到返回值是一个`form`标签和`script`标签, 然后把返回值插入到页面当中即可唤起`网页版支付宝`

```js
const div = document.createElement('div')
div.innerHTML = form // form就是后台返回的数据
document.body.appendChild(div)
document.forms[0].submit()
```
