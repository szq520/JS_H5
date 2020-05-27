
> 本页根据阮一峰老师的[ECMAScript 6 入门](http://es6.ruanyifeng.com)整理笔记

## 新增两种声明变量方式 let和const
---

- 在es6之前, var声明的变量存在两个缺点

  - 一是没有`块级作用域`
  - 二是`变量提升`到代码的最顶部

<br>

##### **示例1 对比`var`和`let`声明变量的区别**

```js
{
  let a = 1
  var b = 2
}

console.log(a) // a is not defined.
console.log(b) // 2
```

可以看到使用`let`定义的变量在花括号外面打印会报错

<br>

##### **示例2 `var`没有块级作用域**

```js
for (var i = 0; i < 5; i++) {
  // ...
}
console.log(i) // 5
```

缺点也十分明显`for循环`也属于块级作用域, 通过`var`定义的变量在外部依然能访问到

<br>

##### **示例3 没有块级作用域带来的种种问题**

```js
// 通过var声明变量

for (var i = 0; i < 5; i++) {
  // console.log('定时器外面', i) // 顺序打印 0 1 2 3 4

  setTimeout(() => {
    // console.log('定时器里面', i) // 每次都打印5
  })

  ;(function (i) {
    setTimeout(() => {
      console.log('闭包里面', i) // 顺序打印 0 1 2 3 4
    })
  })(i)
}
```

即使是在for循环的内部, `var`声明的变量也存在种种问题, 为此es5时期大家普遍使用闭包来解决这个问题

```js
// 通过let声明变量

for (let i = 0; i < 5; i++) {
  console.log('定时器外面', i) // 顺序打印 0 1 2 3 4

  setTimeout(() => {
    console.log('定时器里面', i) // 顺序打印 0 1 2 3 4
  })
}
```

可以看到`let`定义的变量, 无论是在定时器内部还是外部, 都可以正常打印输出

<br>

##### **示例4 变量在块级区域内可以免受外界干扰**

```js
var x = 1
{
  const x = 2
  console.log('作用域内', x) // 2
}
console.log('作用域外', x) // 1
```

优点是局部作用域可以避免变量污染, 缺点是如果作用域出现新的声明, 则会锁死该作用域, 导致无法使用到外部的变量

```js
let x = 1
{
  console.log(x) // x is not defined
  let x
}
```

<br>

##### **示例5 块级作用域与函数声明**

- 在es5中

  - 函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明, 但是浏览器为了兼容以前的代码, 没有遵守这个规定

- 在es6中

  - 引入了块级作用域的概念, 明确的允许在块级作用域之中声明函数, 声明方式类似于`let`, 在块级作用域之外不可引用

  - 同样是为了兼容, es6规定浏览器的实现可以有`自己的行为方式`

    - 允许在块级作用域内声明函数
    - 函数声明类似于var, 会提升到全局作用域或函数作用域的头部
    - 函数声明还会提升到所在的块级作用域的头部

<br>

!> 下面的代码如果在es5中运行, 会打印出`world`是因为在es5中, 函数的声明类似于var, 没有块级作用域, 第二次的函数声明提升到了外面

```js
// 声明一个函数
function f() {
  console.log('hello')
}

(function () {
  if (false) {
    // 重复声明
    function f() {
      console.log('world')
    }
  }
  // 执行函数
  f()
}())
```

!> 如果是在es6中运行, 按理说会打印出`hello`, 但实际上则会报错, 因为es6规定浏览器为了兼容可以有自己的行为方式, 这个行为方式指的就是, 函数声明类似于var, 会提升到全局作用域或函数作用域的头部, 函数声明还会提升到所在的块级作用域的头部, 所以最终会在函数作用域中出现一个`var f = undefined`, 在加上`if (false) {}`代码并没有被执行, 才会报错提示`f is not a function`

?> 总结: 为了避免不同的浏览器的行为差异过大, 应该避免在块级作用域中声明函数, 即使需要的话, 也应该写成`函数表达式`

```js
// 函数声明语句
function f() {}

// 函数表达式
let f = function () {}
```

<br>
<br>
<br>

## 新增一种变量的赋值方式 解构赋值
---

- 可以以特定的方式从数组或对象中对变量进行赋值, 只要等号两边的模式相同, 就可以赋值成功

```js
let [a, b, c] = [1, 2, 3]
console.log(a, b, c) // 1, 2, 3

let [a, [[b], c]] = [1, [[2], 3]]
console.log(a, b, c) // 1, 2, 3

let [ , , a] = [1, 2, 3]
console.log(a) // 3

let [a, ...obj] = [1, 2, 3, 4]
console.log(a, obj) // 1, [2, 3, 4]

let [x, y, ...z] = [1]
console.log(x, y, z) // 1 undefined []
```

- 如果等号的右边是`不可遍历结构`(没有 Iterator 接口), 将会报错

```js
let [a] = 1
let [a] = false
let [a] = NaN
let [a] = undefined
let [a] = null
let [a] = {}
```

<br>

<br>
<br>
<br>

## 新增一种原始数据类型 Symbol
---

在es6之前, javascript拥有5种原始数据类型

  - String
  - Number
  - Boolean
  - null
  - undefined

而现在, js新增了一个原始数据类型`Symbol`

  - Symbol属性不可重复声明, 具有唯一性, 可以用来解决命名冲突
  - Symbol值不能与其他数据进行计算, 也不可以同其他字符串拼接
  - 不会被`for of`或者`for in`遍历

<br>
<br>
<br>

## 新增两种遍历方式`(for in)`和`(for of)`
---

?> ES6 借鉴 C++、Java、C# 和 Python 语言，引入了for...of循环，作为遍历所有数据结构的统一的方法

<br>

##### **只要是有`Symbol.iterator`属性的数据结构, 就可以用`for...of`**

```js
var arr = ['a', 'b', 'c', 'd']

// for...in循环读取键名
for (let a in arr) {
  console.log(a) // 0 1 2 3
}

// for...of循环读取键值
for (let a of arr) {
  console.log(a) // a b c d
}
```

<br>

##### **`for...of`对于数组的遍历器接口只返回具有数字索引的属性**

```js
let arr = [3, 5, 7]
arr.foo = 'hello'

for (let i in arr) {
  console.log(i) // "0", "1", "2", "foo"
}

for (let i of arr) {
  console.log(i) //  "3", "5", "7"
}
```

<br>

##### **`Set`和`Map`结构可以直接使用`for...of`循环**

- `Map`结构

```js
const map = new Map()
map.set('x', 1)
map.set('y', 'hello')
map.set('z', [22, 33, 44])

for (let [key, val] of map) {
  console.log(key, val)
}
```

- `set`结构

```js
var set = new Set([10, 20, 30])

for (let val of set) {
  console.log(val)
}
```

<br>

##### **`for...in`循环有几个缺点**

- 数组的键名是数字，但是`for...in`循环是以字符串作为键名“0”、“1”、“2”等等。

- `for...in`循环不仅遍历数字键名，还会遍历手动添加的其他键，甚至包括原型链上的键。

- 某些情况下，`for...in`循环会以任意顺序遍历键名。

<br>

##### **`for...of`循环有一些显著的优点**

- 有着同`for...in`一样的简洁语法，但是没有`for...in`那些缺点。

- 不同于`forEach`方法，它可以与`break`、`continue`和`return`配合使用。

- 提供了遍历所有数据结构的统一操作接口。

```js
const arr = [1, 2, 3, 4, 5]
for (let n of arr) {
  if (n > 3) break
  console.log(n)
}
```

<br>
<br>
<br>

## 新增 Iterator (遍历器)
---

?> Iterator（遍历器）是一种接口机制, 为各种不同的数据结构提供统一的访问机制

!> 由于数组的遍历会调用遍历器接口，所以任何接受数组作为参数的场合，其实都调用了`Iterator 接口`（即`Symbol.iterator`方法）

<br>

##### **解构赋值**

对`数组`和`Set 结构`进行解构赋值时，会默认调用`Symbol.iterator`方法

```js
// set结构
const [a, b, c] = new Set([1, 2, 3])
console.log(a, b, c)

// 数组
const [x, y, z] = [1, 2, 3]
console.log(x, y, z)
```

<br>

##### **扩展运算符**

扩展运算符`...`也会调用默认的 Iterator 接口

```js
const arr = [1,2,3]
console.log(Math.max(...arr))
```

!> 任何部署了`Iterator`接口的数据结构都可以转换成数组

<br>

##### **yield***

`yield*`后面跟的是一个可遍历的结构，它会调用该结构的遍历器接口

```js
const generator = function* () {
  yield 1
  yield* [2,3,4]
  yield 5
}

const iterator = generator()

iterator.next() // { value: 1, done: false }
iterator.next() // { value: 2, done: false }
iterator.next() // { value: 3, done: false }
iterator.next() // { value: 4, done: false }
iterator.next() // { value: 5, done: false }
iterator.next() // { value: undefined, done: true }
```

<br>

##### **字符串的 Iterator 接口**

字符串是一个类似数组的对象，也原生具有 Iterator 接口

```js
var str = "hi"

var iterator = str[Symbol.iterator]()

iterator.next() // { value: "h", done: false }
iterator.next() // { value: "i", done: false }
iterator.next() // { value: undefined, done: true }
```

##### **24 个 ES6 方法，用来解决实际开发的 JS 问题**
```js
1.如何隐藏所有指定的元素
const hide = (el) => Array.from(el).forEach(e => (e.style.display = 'none'));
// 事例:隐藏页面上所有`<img>`元素?
hide(document.querySelectorAll('img'))

2.如何检查元素是否具有指定的类？
页面DOM里的每个节点上都有一个classList对象，程序员可以使用里面的方法新增、删除、修改节点上的CSS类。使用classList，程序员还可以用它来判断某个节点是否被赋予了某个CSS类。
const hasClass = (el, className) => el.classList.contains(className)
// 事例
hasClass(document.querySelector('p.special'), 'special') // true

3.如何切换一个元素的类?
const toggleClass = (el, className) => el.classList.toggle(className)
// 事例 移除 p 具有类`special`的 special 类
toggleClass(document.querySelector('p.special'), 'special')

4.如何获取当前页面的滚动位置？
const getScrollPosition = (el = window) => ({
  x: el.pageXOffset !== undefined ? el.pageXOffset : el.scrollLeft,
  y: el.pageYOffset !== undefined ? el.pageYOffset : el.scrollTop
});
// 事例
getScrollPosition(); // {x: 0, y: 200}

5.如何平滑滚动到页面顶部
const scrollToTop = () => {
  const c = document.documentElement.scrollTop || document.body.scrollTop;
  if (c > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, c - c / 8);
  }
}
// 事例
scrollToTop()
window.requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。
requestAnimationFrame：优势：由系统决定回调函数的执行时机。60Hz的刷新频率，那么每次刷新的间隔中会执行一次回调函数，不会引起丢帧，不会卡顿。

6.如何检查父元素是否包含子元素？
const elementContains = (parent, child) => parent !== child && parent.contains(child);
// 事例
elementContains(document.querySelector('head'), document.querySelector('title')); 
// true
elementContains(document.querySelector('body'), document.querySelector('body')); 
// false

7.如何检查指定的元素在视口中是否可见？
const elementIsVisibleInViewport = (el, partiallyVisible = false) => {
  const { top, left, bottom, right } = el.getBoundingClientRect();
  const { innerHeight, innerWidth } = window;
  return partiallyVisible
    ? ((top > 0 && top < innerHeight) || (bottom > 0 && bottom < innerHeight)) &&
        ((left > 0 && left < innerWidth) || (right > 0 && right < innerWidth))
    : top >= 0 && left >= 0 && bottom <= innerHeight && right <= innerWidth;
};
// 事例
elementIsVisibleInViewport(el); // 需要左右可见
elementIsVisibleInViewport(el, true); // 需要全屏(上下左右)可以见

8.如何获取元素中的所有图像？
const getImages = (el, includeDuplicates = false) => {
  const images = [...el.getElementsByTagName('img')].map(img => img.getAttribute('src'));
  return includeDuplicates ? images : [...new Set(images)];
};
// 事例：includeDuplicates 为 true 表示需要排除重复元素
getImages(document, true); // ['image1.jpg', 'image2.png', 'image1.png', '...']
getImages(document, false); // ['image1.jpg', 'image2.png', '...']

9.如何确定设备是移动设备还是台式机/笔记本电脑？
const detectDeviceType = () =>
  /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)
    ? 'Mobile'
    : 'Desktop';

// 事例
detectDeviceType(); // "Mobile" or "Desktop"

10.How to get the current URL?
const currentURL = () => window.location.href
// 事例
currentURL() // 'https://google.com'
11.如何创建一个包含当前URL参数的对象？
const getURLParameters = url =>
  (url.match(/([^?=&]+)(=([^&]*))/g) || []).reduce(
    (a, v) => ((a[v.slice(0, v.indexOf('='))] = v.slice(v.indexOf('=') + 1)), a),
    {}
  );
// 事例
getURLParameters('http://url.com/page?n=Adam&s=Smith'); // {n: 'Adam', s: 'Smith'}
getURLParameters('google.com'); // {}

12.如何将一组表单元素转化为对象？
const formToObject = form =>
  Array.from(new FormData(form)).reduce(
    (acc, [key, value]) => ({
      ...acc,
      [key]: value
    }),
    {}
  );
// 事例
formToObject(document.querySelector('#form')); 
// { email: 'test@email.com', name: 'Test Name' }

13.如何从对象检索给定选择器指示的一组属性？
const get = (from, ...selectors) =>
  [...selectors].map(s =>
    s
      .replace(/\[([^\[\]]*)\]/g, '.$1.')
      .split('.')
      .filter(t => t !== '')
      .reduce((prev, cur) => prev && prev[cur], from)
  );
const obj = { selector: { to: { val: 'val to select' } }, target: [1, 2, { a: 'test' }] };

// Example
get(obj, 'selector.to.val', 'target[0]', 'target[2].a'); 
// ['val to select', 1, 'test']

14.如何在等待指定时间后调用提供的函数？
const delay = (fn, wait, ...args) => setTimeout(fn, wait, ...args);
delay(
  function(text) {
    console.log(text);
  },
  1000,
  'later'
); 

// 1秒后打印 'later'
15.如何在给定元素上触发特定事件且能选择地传递自定义数据？
const triggerEvent = (el, eventType, detail) =>
  el.dispatchEvent(new CustomEvent(eventType, { detail }));

// 事例
triggerEvent(document.getElementById('myId'), 'click');
triggerEvent(document.getElementById('myId'), 'click', { username: 'bob' });
自定义事件的函数有 Event、CustomEvent 和 dispatchEvent
// 向 window派发一个resize内置事件
window.dispatchEvent(new Event('resize'))
 

// 直接自定义事件，使用 Event 构造函数：
var event = new Event('build');
var elem = document.querySelector('#id')
// 监听事件
elem.addEventListener('build', function (e) { ... }, false);
// 触发事件.
elem.dispatchEvent(event);
CustomEvent 可以创建一个更高度自定义事件，还可以附带一些数据，具体用法如下：
var myEvent = new CustomEvent(eventname, options);
其中 options 可以是：
{
  detail: {
    ...
  },
  bubbles: true,    //是否冒泡
  cancelable: false //是否取消默认事件
}
其中 detail 可以存放一些初始化的信息，可以在触发的时候调用。其他属性就是定义该事件是否具有冒泡等等功能。
内置的事件会由浏览器根据某些操作进行触发，自定义的事件就需要人工触发。
dispatchEvent 函数就是用来触发某个事件：
element.dispatchEvent(customEvent);
上面代码表示，在 element 上面触发 customEvent 这个事件。
// add an appropriate event listener
obj.addEventListener("cat", function(e) { process(e.detail) });
 
// create and dispatch the event
var event = new CustomEvent("cat", {"detail":{"hazcheeseburger":true}});
obj.dispatchEvent(event);
使用自定义事件需要注意兼容性问题，而使用 jQuery 就简单多了：

// 绑定自定义事件
$(element).on('myCustomEvent', function(){});
 
// 触发事件
$(element).trigger('myCustomEvent');
// 此外，你还可以在触发自定义事件时传递更多参数信息：
 
$( "p" ).on( "myCustomEvent", function( event, myName ) {
  $( this ).text( myName + ", hi there!" );
});
$( "button" ).click(function () {
  $( "p" ).trigger( "myCustomEvent", [ "John" ] );
});

16.如何从元素中移除事件监听器?
const off = (el, evt, fn, opts = false) => el.removeEventListener(evt, fn, opts);
const fn = () => console.log('!');
document.body.addEventListener('click', fn);
off(document.body, 'click', fn); 

17.如何获得给定毫秒数的可读格式？
const formatDuration = ms => {
  if (ms < 0) ms = -ms;
  const time = {
    day: Math.floor(ms / 86400000),
    hour: Math.floor(ms / 3600000) % 24,
    minute: Math.floor(ms / 60000) % 60,
    second: Math.floor(ms / 1000) % 60,
    millisecond: Math.floor(ms) % 1000
  };
  return Object.entries(time)
    .filter(val => val[1] !== 0)
    .map(([key, val]) => `${val} ${key}${val !== 1 ? 's' : ''}`)
    .join(', ');
};
// 事例
formatDuration(1001); // '1 second, 1 millisecond'
formatDuration(34325055574); 
// '397 days, 6 hours, 44 minutes, 15 seconds, 574 milliseconds'

18.如何获得两个日期之间的差异（以天为单位）？
const getDaysDiffBetweenDates = (dateInitial, dateFinal) =>
  (dateFinal - dateInitial) / (1000 * 3600 * 24);
// 事例
getDaysDiffBetweenDates(new Date('2017-12-13'), new Date('2017-12-22')); // 9

19.如何向传递的URL发出GET请求？
const httpGet = (url, callback, err = console.error) => {
  const request = new XMLHttpRequest();
  request.open('GET', url, true);
  request.onload = () => callback(request.responseText);
  request.onerror = () => err(request);
  request.send();
};

httpGet(
  'https://jsonplaceholder.typicode.com/posts/1',
  console.log
); 
// {"userId": 1, "id": 1, "title": "sample title", "body": "my text"}

20.如何对传递的URL发出POST请求？
const httpPost = (url, data, callback, err = console.error) => {
  const request = new XMLHttpRequest();
  request.open('POST', url, true);
  request.setRequestHeader('Content-type', 'application/json; charset=utf-8');
  request.onload = () => callback(request.responseText);
  request.onerror = () => err(request);
  request.send(data);
};

const newPost = {
  userId: 1,
  id: 1337,
  title: 'Foo',
  body: 'bar bar bar'
};
const data = JSON.stringify(newPost);
httpPost(
  'https://jsonplaceholder.typicode.com/posts',
  data,
  console.log
); 
// {"userId": 1, "id": 1337, "title": "Foo", "body": "bar bar bar"}

21.如何为指定选择器创建具有指定范围，步长和持续时间的计数器？
const counter = (selector, start, end, step = 1, duration = 2000) => {
  let current = start,
    _step = (end - start) * step < 0 ? -step : step,
    timer = setInterval(() => {
      current += _step;
      document.querySelector(selector).innerHTML = current;
      if (current >= end) document.querySelector(selector).innerHTML = end;
      if (current >= end) clearInterval(timer);
    }, Math.abs(Math.floor(duration / (end - start))));
  return timer;
};

// 事例
counter('#my-id', 1, 1000, 5, 2000); 
// 让 `id=“my-id”`的元素创建一个2秒计时器

22.如何将字符串复制到剪贴板？
  const el = document.createElement('textarea');
  el.value = str;
  el.setAttribute('readonly', '');
  el.style.position = 'absolute';
  el.style.left = '-9999px';
  document.body.appendChild(el);
  const selected =
    document.getSelection().rangeCount > 0 ? document.getSelection().getRangeAt(0) : false;
  el.select();
  document.execCommand('copy');
  document.body.removeChild(el);
  if (selected) {
    document.getSelection().removeAllRanges();
    document.getSelection().addRange(selected);
  }
};
// 事例
copyToClipboard('Lorem ipsum'); 
// 'Lorem ipsum' copied to clipboard

23.如何确定页面的浏览器选项卡是否聚焦？
const isBrowserTabFocused = () => !document.hidden;
// 事例
isBrowserTabFocused(); // true

24.如何创建目录（如果不存在）？
const fs = require('fs');
const createDirIfNotExists = dir => (!fs.existsSync(dir) ? fs.mkdirSync(dir) : undefined);
// 事例
createDirIfNotExists('test'); 

```