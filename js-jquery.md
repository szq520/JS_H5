
## jQuery 对象
---

> jquery对象转换原生DOM

```js
var box = $('.box')[0]
console.log( box )
```

> 原生DOM转换为jquery对象

```js
var box = document.querySelector('.box')
console.log( $(box) )
```

> 应用场景

在事件中, this指向原生DOM, 所以不能通过this直接调用jq方法

~~`this.css('width', '100px')`~~

而是要转换成jq对象

```js
$('.box').on('click', function () {
  $(this).css('background-color', 'red')
})
```

<br>
<br>
<br>

## jQuery 选择器
---

```js
// 获取类样式为box的元素
$('.box')

// 获取id等于top元素下面所有的span标签
$('#top span')

// 获取类样式为nav的ul下的li
$('ul.nav>li')

// 获取type等于button的input标签
$('input[type="button"]')
$('input:button')

// 获取所有包含'删除'两个字的a标签
$('a:contains("删除")')
// 获取所有input标签
$(':input')

// 获取单选/复选框已被选中的元素
$(':checked')

// 获取下拉表单被选中的元素
$(':selected')

// 获取表单中被禁用掉的元素
$(':disabled')
```

<br>
<br>
<br>

## jQuery 获取元素
---

```js
// 获取ul下第一个li标签
$('ul>li').first()

// 获取ul下最后一个li标签
$('ul>li').last()

// 获取第n个li标签(n从0开始)
$('ul>li').eq(n)

// 筛选类样式为active的li
$('ul>li').filter('.active')

// 剔除类样式为active的li
$('ul>li').not('.active')

// 获取.active的前一个li
$('.active').prev()

// 获取.active的后一个li
$('.active').next()

// 获取.active前面所有的li
$('.active').prevAll()

// 获取.active前面所有的li
$('.active').nextAll()

// 获取除了.active以外的的兄弟节点
$('.active').siblings()

// 获取ul下的的所有子元素
$('ul').children()

// 获取ul下指定的子元素
$('ul').find('.active')

// 获取ul的父级元素
$('ul').parent()

// 获取ul指定的父元素
$('ul').parents('.box')

// 获取所有的p标签和span标签
$('p').add('span')
```

<br>
<br>
<br>

## jQuery 操作css样式
---

> 单独设置css样式

```js
$('.box').css('background-color', 'pink')
```

> css属性连写方式

```js
$('.box').css({
  width: '100px',
  height: '100px'
})

// 或者通过链式操作
$('.box')
  .css('width', '100px')
  .css('height', '100px')
```

<br>
<br>
<br>

## jQuery 动画函数
---

> 基本动画函数

```js
/* 动画函数可以带两个参数
 * 第一个参数是时间, 单位为毫秒
 * 第二个参数为回调函数, this指向原生DOM
 */

$('#show').on('click', function () {
  $('.box').show(300)
})

$('#hide').on('click', function () {
  $('.box').hide(300)
})

$('#toggle').on('click', function () {
  $('.box').toggle(300)
})

$('#slideUp').on('click', function () {
  $('.box').slideUp(300)
})

$('#slideDown').on('click', function () {
  $('.box').slideDown(300)
})

$('#slideToggle').on('click', function () {
  $('.box').slideToggle(300)
})

$('#fadeIn').on('click', function () {
  $('.box').fadeIn(300)
})

$('#fadeOut').on('click', function () {
  $('.box').fadeOut(300)
})

$('#fadeToggle').on('click', function () {
  $('.box').fadeToggle(300)
})
```

> 自定义动画函数

```js
// 自定义动画
$('#animate').on('click', function () {
  $('.box').animate({
    width: '100px',
    height: '100px',
    // 自定义动画中的颜色不能使用单词!
    backgroundColor: 'red'
  }, 1000, function () {
    // 这里可以执行回调函数
  })
})
```

> 延迟动画

```js
$('#btn').on('click', function () {
  $('.box').show(300).delay(1000).hide(300)
})
```

<br>
<br>
<br>

## jQuery 操作DOM
---

> 增删改查

```js
// 把.bar后追加到.box中
$('.box').append($('.bar'))
$('.bar').appendTo('.box')

// 把.bar前追加到.box中
$('.box').prepend($('.bar'))
$('.bar').prependTo('.box')

// 把.bar追加为.active的前兄弟元素
$('.active').before($('.bar'))
$('.bar').insertBefore('.active')

// 把.bar追加为.active的后兄弟元素
$('.active').after($('.bar'))
$('.bar').insertAfter('.active')

// 清空.box中所有的子元素
$('.box').empty()

// 移除.box这个元素
$('.box').remove()
```

> 克隆元素

!> 克隆元素是可以传递参数的!

```js
// 如果不传递参数, 则表示只克隆DOM结构
$('li').clone()

// 如果传递参数true, 则连同事件一起克隆
$('li').clone(true)
添加内容
// 类似于innerHTML
$('li').html('<a>这是一个a链接</a>')

// 类似于innerText
$('li').text('<a>这是一个a链接</a>')

// 类似于value
$('input').val('请输入')
```

<br>
<br>
<br>

## jQuery 操作类名
---

```js
$('.nav li').on('click', function () {
  // 移除指定的类样式
  $('.active').removeClass('active')
  // 给当前元素添加类样式
  $(this).addClass('active')
})

// 切换类样式
$('li').toggleClass('active')

// 判断类样式 true | false
$('li').hasClass('active')
```

<br>
<br>
<br>

## jQuery 操作属性
---

> 可以获取属性的值、修改属性的值、添加自定义属性

```js
// 只有一个参数时,attr可以获取属性的值
console.log( $('input').attr('type') )

// 当有两个参数时,attr可以修改属性的值
$('input').attr('type', 'button')

// 如果该属性不存在,则可以添加自定义属性
$('input').attr('index', '1')

// 同时修改或设置多个属性
$('input').attr({
  'title': '输入框',
  'value': '请输入内容'
})
```

> 移除属性

```html
<input type="checkbox" checked="true">
```
```js
// 移除checked属性,使复选框取消选中
$('input').removeAttr('checked')
```

<br>
<br>
<br>

## jQuery 表单方法
---

> 获取表单数据

```js
/* 获取formData格式的数据
 * user=buuing&pass=1234
 */
$('form').serialize()

/* 获取数组格式的数据
 * [{name:"user",value:"buuing"},
 *  {name:"pass",value:"1234"}]
 */
$('form').serializeArray()
```
```js
// 获取焦点
$(':text').focus()

// 失去焦点
$(':text').blur()

// 选中内容
$(':text').select()
```

> 应用场景

```js
// 点击输入框时自动选中内容
$(':text').focus(function () {
  $(this).select()
})
```

<br>
<br>
<br>

## jQuery 获取坐标
---

```js
// 相对于文档html坐标
$('.box').offset().top
$('.box').offset().left

// 相对于拥有定位属性的元素
$('.box').position().top
$('.box').position().left

// 获取元素卷取出去的坐标
$('.box').scrollLeft()
$('.box').scrollTop()
```
```js
$('.box').on('click', function (e) {
  // 相对于屏幕的坐标
  e.screenX
  e.screenY
  // 相对于自身的坐标(不包括边框)
  e.offsetX
  e.offsetY
  // 相对于可视区域的坐标
  e.clientX
  e.clientY
  // 相对于文档html的坐标
  e.pageX
  e.pageY
})
```

<br>
<br>
<br>

## jQuery 注册事件
---

> 添加事件的三种方式

```js
// 通过on添加点击事件
$('.box').on('click', function () {
  console.log('我被点了')
})

// 通过bind添加点击事件
$('.box').bind('click', function() {
  console.log('我又被点了')
})

// 通过简洁方法添加点击事件
$('.box').click(function () {
  console.log('我再一次的被点了')
})
```

> 一次性事件

```js
$('.box').one('click', function() {
  alert('该事件只会触发一次')
})
```

> 添加多个事件

```js
$('.box')
  .on('mouseover', function () {
    console.log('鼠标进入事件')
  })
  .on('mouseout', function () {
    console.log('鼠标离开事件')
  })
```

> 移除事件

```js
// 移除所有事件
$('.box').off()

// 移除指定事件
$('.box').off('click')

// 移除多个事件
$('.box').off('click mouseout')
```

<br>
<br>
<br>

## jQuery 事件委托
---

> on通过传递第二个参数 (选择器) 可以实现事件委托

```js
// 给.box中的p标签委托事件
$('.box').bind('click', 'p', function () {
  console.log('触发了点击事件')
})

// 支持多个选择器
$('.box').on('click', 'p, span', function () {
  console.log('触发了点击事件')
})

// 除了on, 还有也支持事件委托
$('.box').delegate('p', 'click', function () {
  console.log(111)
})
```

<br>
<br>
<br>

## jQuery 事件触发
---

> 可以主动去触发相应的事件

```js
$('.box').on('click', function () {
 console.log('我被点了')
})
// 将会在1秒后自动触发点击事件
setTimeout(function () {
 $('.box').trigger('click')
}, 1000)
```

<br>
<br>
<br>

## jQuery 事件对象
---

> jquery对事件对象进行了简单处理

```js
// 在事件的回调函数中, 传递形参即可得到事件对象
$('.box').click(function (e) {
  // 分别为jq事件对象
  console.log(e)
  // 和原生对象
  console.log(e.originalEvent)
})
```

<br>
<br>
<br>

## jQuery 事件冒泡
---

> 因为IE低版本不支持捕获, 所以jq只支持冒泡阶段

```js
// 阻止冒泡
$('.box').on('click', function (e) {
  e.stopPropagetion()
})
// 阻止默认行为
$('.box').on('click', function (e) {
  e.preventDrfault()
})
```