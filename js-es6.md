
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