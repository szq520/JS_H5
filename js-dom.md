
## Document 文档
---

?> Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问

##### **属性**

```js
// 返回<body>标签
window.document.body

// 设置或返回与当前文档有关的所有 cookie
window.document.cookie

// 返回当前文档的域名
window.document.domain

// 返回文档被最后修改的日期和时间
window.document.lastModified

// 返回载入当前文档的文档的 URL
window.document.referrer

// 返回当前文档的标题
window.document.title

// 返回当前文档的 URL
window.document.URL
```

##### **方法**

```js
// 通过id获取元素
window.document.getElementById('Id值')

// 通过元素名称获取元素(伪数组)
window.document.getElementsByTagName('元素名称')

// 通过name属性的值获取元素
window.document.getElementsByName('name属性的值')

// 通过类样式名获取元素
window.document.getElementsByClassName('类样式名称')

// 通过选择器获取元素
window.document.querySelector('选择器')

// 通过选择器获取元素(伪数组)
window.document.querySelectorAll('选择器')
```

<br>
<br>
<br>

## Element 元素
---

?> Element 对象可以拥有类型为元素节点、文本节点、注释节点的子节点

##### **节点**

| 相对应的值 | nodeType | nodeName | nodeValue
| --- | --- | --- | ---
| 标签 | 1 | 大写的标签名 | null
| 属性 | 2 | 小写的属性名 | 属性的值
| 文本 | 3 | #text | 文本内容

```js
// 返回元素的名称
element.nodeName

// 返回元素的节点类型
element.nodeType

// 设置或返回元素值
element.nodeValue
```

##### **属性**

**`操作元素或节点`**

```js
// 父级节点
element.parentNode

// 父级元素
element.parentElement

// 子级节点
element.childNodes

// 子级元素
element.children

// 第一个子级节点
element.firstChild

// 第一个子级元素
element.firstElementChild

// 最后一个子级节点
element.lastChild

// 最后一个子级元素
element.lastElementChild

// 前一个兄弟节点
element.previousSibling

// 前一个兄弟元素
element.previousElementSibling

// 后一个兄弟节点
element.nextSibling

// 后一个兄弟元素
element.nextElementSibling
```

**`操作标签属性`**

```js
// 设置或返回元素的id
element.id

// 设置或返回元素的title属性
element.title

// 设置或返回元素的class属性
element.className

// 返回元素的标签名
element.tagName

// 设置或返回元素的style属性
element.style

// 设置或返回元素的内容
element.innerHTML
```

**`元素的位置`**

```js
// 返回元素的可见高度
element.clientHeight

// 返回元素的可见宽度
element.clientWidth

// 返回元素的高度
element.offsetHeight

// 返回元素的宽度
element.offsetWidth

// 返回元素的水平偏移位置
element.offsetLeft

// 返回元素的偏移容器
element.offsetParent

// 返回元素的垂直偏移位置
element.offsetTop

// 返回元素的整体高度
element.scrollHeight

// 返回元素左边缘与视图之间的距离
element.scrollLeft

// 返回元素上边缘与视图之间的距离
element.scrollTop

// 返回元素的整体宽度
element.scrollWidth
```

##### **方法**

```
// 把元素转换为字符串
element.toString()
```
```js
// 返回元素节点的指定属性值
element.getAttribute()
// 返回指定的属性节点
element.getAttributeNode()
// 返回拥有指定标签名的所有子元素的集合
element.getElementsByTagName()
// 把指定属性设置或更改为指定值
element.setAttribute()
// 设置或更改指定属性节点
element.setAttributeNode()
```
```js
// 如果元素拥有指定属性，则返回true，否则返回 false
element.hasAttribute()
// 如果元素拥有属性，则返回 true，否则返回 false
element.hasAttributes()
// 如果元素拥有子节点，则返回 true，否则 false
element.hasChildNodes()
```

?> 创建元素 `document.createElement('标签名称')`

```js
// 把新元素插在某个子元素前面
element.insertBefore(新元素,插在谁前面)
// 向元素添加新的子节点，作为最后一个子节点
element.appendChild()
// 从元素中移除指定属性
element.removeAttribute()
// 移除指定的属性节点，并返回被移除的节点
element.removeAttributeNode()
// 从元素中移除子节点
element.removeChild()
// 替换元素中的子节点
element.replaceChild(新元素,替换元素)
// 克隆元素
element.cloneNode()
```

<br>
<br>
<br>

## Event 事件
---

?> Event 对象代表事件的状态，比如事件在其中发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态

##### **事件名称**

| 名称 | 描述 | 名称 | 描述
| --- | --- | --- | ---
| onclick     | 当用户点击某个对象  | onmouseout  | 鼠标移出
| ondblclick  | 当用户双击某个对象  | onmousedown | 鼠标按下
| onfocus     | 元素获得焦点       | onmouseup   | 鼠标抬起
| onblur      | 元素失去焦点       | onreset     | 重置按钮被点击
| onchange    | 内容被改变         | onselect    | 文本被选中
| onkeydown   | 某个按键被按下     | onsubmit    | 确认按钮被点击
| onkeyup     | 某个按键被抬起     | onload      | 一张页面或一幅图像完成
| onkeypress  | 某个按键按下并抬起  | onunload    | 用户退出页面
| onmousemove | 鼠标被移动         | onresize    | 窗口或框架被重新调整大小
| onmouseover | 鼠标进入          | onerror     | 在加载文档或图像时发生

##### **事件参数**

| 属性 | 描述
| --- | ---
| altKey        | 返回当事件被触发时，"ALT" 是否被按下。
| button        | 返回当事件被触发时，哪个鼠标按钮被点击。
| clientX       | 返回当事件被触发时，鼠标指针的水平坐标。
| clientY       | 返回当事件被触发时，鼠标指针的垂直坐标。
| ctrlKey       | 返回当事件被触发时，"CTRL" 键是否被按下。
| metaKey       | 返回当事件被触发时，"meta" 键是否被按下。
| relatedTarget | 返回与事件的目标节点相关的节点。
| screenX       | 返回当某个事件被触发时，鼠标指针的水平坐标。
| screenY       | 返回当某个事件被触发时，鼠标指针的垂直坐标。
| shiftKey      | 返回当事件被触发时，"SHIFT" 键是否被按下。

<br>
<br>
<br>

## addEvent 事件绑定
---

?> 在实际开发中普通的事件注册会把前面的覆盖掉，而事件绑定则不会，无论绑定多少个都会根据条件进行触发


#### 为元素绑定多个事件

`addEventListener('事件类型', '事件处理函数', '事件是否捕获')`

> 事件类型不带on，this指向当前对象

```js
btn.addEventListener('click', function () {
  console.log('事件1')
}, false)

btn.addEventListener('click', function () {
  console.log('事件2')
}, false)
```

!> 只兼容谷歌和火狐, IE8不兼容

<br>

`attachEvent('事件类型', '事件处理函数')`

> 事件类型带on，this指向window

```js
attachEnent('onclick', function () {
  console.log('事件1')
})

attachEnent('onclick', function () {
  console.log('事件2')
})
```

!> 不兼容谷歌和火狐, IE8可以使用

<br>

#### 为元素解绑事件

> 移除所有事件

```js
Obj.onclick = null
```

> 移除指定的事件

```js
Obj.removeEventListener(事件类型, 方法名, false)
Obj.detachEnent(事件类型, 方法名)
```
