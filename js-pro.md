
## 几种常见的排序算法
---

- [冒泡排序](javascript:;)

  - 在遍历的过程中每次只比较两个元素, 如果顺序错误就进行交换

```js
function bubbleSort (arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j+1]) {
        let temp = arr[j+1]
        arr[j+1] = arr[j]
        arr[j] = temp
      }
    }
  }
  return arr
}
```

<br>

- [选择排序](javascript:;)

  - 以某个值在遍历的过程中进行比较, 如果碰到比其小的值则记录其index, 最后才进行交换

```js
function selectionSort (arr) {
  for (let i = 0; i < arr.length; i++) {
    let index = i
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[index]) {
        index = j
      }
    }
    let temp = arr[i]
    arr[i] = arr[index]
    arr[index] = temp
  }
  return arr
}
```

<br>

- [插入排序](javascript:;)

  - 从第一个值开始, 如果后面的数大于前面的数则向前插入

```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let key = arr[i]
    let j = i - 1
    while (j >= 0 && arr[i] > key) {
      arr[j + 1] = arr[j]
      j--
    }
    arr[j + 1] = key
  }
  return arr
}
```

<br>

- [快速排序](javascript:;)

  - 每次都以最左边的为基准数, 左右两边同时检索, 左边比基准值大的和右边比基准值小的进行交换

```js
function quickSort (arr, left, right) {
  if (left > right) return false
  const base = arr[left]
  let i = left
  let j = right
  // 当左边索引不等于右边索引时
  while (i !== j) {
    // 从右往左检索, 遇到比基准数小的则停下
    while (arr[j] >= base && i < j) {
      j--
    }
    // 从左往右检索, 遇到比基准数大的则停下
    while (arr[i] <= base && i > j) {
      i++
    }
    // 最后当左右都停下时, 两个元素交换顺序
    let temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
  }
  // 如果两个索引相遇, 则把基准数和当前位置交换
  arr[left] = arr[i]
  arr[i] = base
  // 基准数归位之后, 先排左边在排右边
  quickSort(arr, left, i - 1)
  quickSort(arr, j + 1, right)
  return arr
}
```

<br>

## JS常用的几种继承方式
--- 

- [原型链继承](javascript:;)

  - 通过`改变原型`指向实现原型链的继承, 让子类的`prototype`等于父类的`实例对象`

  - 特点

    - 无法实现多继承
    - 无法实现传参
    - 能访问原型方法/原型属性
    - `实例属性和方法无法改变`

```js
// 人类的构造函数
function Person(name) {
  this.name = name || 'myName'
  this.say = () => console.log('我的名字叫' + this.name)
}

// 通过原型添加属性和方法
Person.prototype.food = '米饭'
Person.prototype.eat = () => console.log('我想吃' + this.food)

// 学生类构造函数
function Student() {}

// 改变原型指向实现原型链继承
Student.prototype = new Person('小明')

var stu1 = new Student()
var stu2 = new Student()
var stu3 = new Student()

// 不能改变实例方法和实例属性
stu1.say()
stu2.say()
stu3.say()

// 能访问原型方法和原型属性
stu1.eat()
```

<br>

- [构造继承](javascript:;)

  - 在子类型构造函数的内部调用超类型的构造函数

  - 特点

    - 可以实现多继承
    - 可以实现传参
    - 只能继承实例属性和方法
    - `不能继承原型方法/原型属性`

```js
// 人类的构造函数
function Person(name) {
  this.name = name || 'myName'
  this.say = () => console.log('我的名字叫' + this.name)
}

// 通过原型添加属性和方法
Person.prototype.food = '米饭'
Person.prototype.eat = () => console.log('我想吃' + this.food)

// 学生类构造函数
function Student(name, score) {
  // 借用构造函数实现构造继承
  Person.call(this, name)
  this.score = score
}

var stu1 = new Student('张三', 59)
var stu2 = new Student('李四', 88)
var stu3 = new Student('王五', 100)

// 可以继承实例方法和实例属性
stu1.say()
stu2.say()
stu3.say()

// 不能继承原型方法和原型属性
stu1.eat()
```

<br>

- [组合继承 (原型链+构造函数)](javascript:;)

  - 使用原型链实现对原型属性和方法的继承, 通过使用构造函数实现对实例属性的继承

  - 特点

    - 集原型链继承和构造函数继承优点于一身

```js
// 人类的构造函数
function Person(name) {
  this.name = name || 'myName'
  this.say = () => console.log('我的名字叫' + this.name)
}

// 通过原型添加属性和方法
Person.prototype.food = '米饭'
Person.prototype.eat = () => console.log('我想吃' + this.food)

// 学生类构造函数
function Student(name, score) {
  // 借用构造函数实现构造继承
  Person.call(this, name)
  this.score = score
}

// 改变原型指向实现原型链继承
Student.prototype = new Person()

var stu1 = new Student('张三', 59)
var stu2 = new Student('李四', 88)
var stu3 = new Student('王五', 100)

// 可以继承实例方法和实例属性
stu1.say()
stu2.say()
stu3.say()

// 可以继承原型方法和原型属性
stu1.eat()
```

<br>

- [拷贝继承](javascript:;)

  - 把一个对象的属性或方法, 复制到另一个对象当中

  - 但并不会把所有属性和方法全部拷贝下来, 比如构造器

```js
function Cat1() {}

Cat1.prototype.name = '小白'
Cat1.prototype.say = () => console.log('喵喵')

var Cat2 = {}

for (var key in Cat1.prototype) {
  Cat2[key] = Cat1.prototype[key]
}

console.dir(Cat1.prototype)
console.dir(Cat2)
```

<br>

- `实例继承` **(不常用)**

- `寄生组合` **(不常用)**

<br>
<br>
<br>

<!-- ## 高阶函数-函数作为参数或返回值使用 -->
<!-- --- -->

<!-- <br> -->
<!-- <br> -->
<!-- <br> -->

## apply和call方法的使用及区别
---

##### **简单理解**

- 最基本的使用, 改变其this指向

```js
function f1(a, b) {
  return console.log(a + b, this)
}

var obj = {
  num: 100
}

// 普通函数中的this指向window
f1(10, 20) // 30 window

// 使用apply或call的话, 则可以改变其中的this指向, 二者之间的区别就是传参方式的不同
f1.apply(obj, [10, 20]) // 30 {num: 100}
f1.call(obj, 10, 20) // 30 {num: 100}
```

<br>

##### **借用别的函数或对象的方法**

```js
// 比如Array的forEach方法
[1, 2, 3, 4, 5].forEach(item => {
  console.log(item)
})

// 会提示 'abcde'.forEach is not a function
'abcde'.forEach(item => {
  console.log(item)
})

// 此时则需要使用call
[].forEach.call('abcde', item => {
  console.log(item)
})
```

<br>

##### **实现继承**

- 在前面的`构造继承`就是使用call来实现的

```js
function Person(name, age, sex) {
  this.name = name
  this.age = age
  this.sex = sex
}

function Student(name, age, sex, score) {
  // 借用构造函数实现构造继承
  Person.call(this, name, age, sex)
  this.score = score
}

var stu = new Student('jack', 18, '男', 99)
console.log(stu)
```

<br>

##### **apply的一些巧妙用法**

  - `Math.max()`可以得到所有参数中的最大值, 但是他的参数不支持数组`Math.max([param1,param2])`, 也就是说得一个一个把要比较的数字放进去`Math.max(param1,param2...)`

  - 由此我们可以通过使用`apply`来使其参数可以传递一个数组

```js
// 假设有一个数组
var arr = [3, 5, 2, 4]

// 该方法规定我们必须把参数一个一个放进去
Math.max(3, 5, 2, 4) // 5

// 如果直接传入一个数组, 他会无法识别该参数
Math.max(arr) // NaN

// 此时我们使用apply轻松解决该难题
Math.max.apply(null, arr) // 5
```

<br>
<br>
<br>

## bind方法的使用及注意问题
---

##### **复制一个方法**

```js
function Person(age) {
  this.age = age
  this.say = function () {
    console.log(`今年${this.age}岁`)
  }
}

function Student(age) {
  this.age = age
}

var per = new Person(18)
var stu = new Student(6)

// 把per的方法复制一份给stu
stu.say = per.say.bind(stu)
stu.say()
```

<br>

##### **改变this指向**

```js
function Game() {
  this.num = Math.random()
}

Game.prototype.play = function () {
  // 定时器中的this指向window, 所以通过bind传递this
  setInterval(function () {
    console.log(this.num)
  }.bind(this), 1000)
}

var game = new Game()
game.play()
```

<br>
<br>
<br>

## 作用域、作用域链、预解析
---

- 相对于`es5`来讲js是没有块级作用域的

  - 比如: `if () {}`
  - 比如: `for () {}`
  - 比如: `while () {}`

```js
if (true) {
  var num = 10
}
// 可以看到在外部依然可以打印到num
console.log(num) // 10
```

- 但是js有全局作用域和局部作用域

  - 全局变量: 只要不是在函数中定义的变量
  - 局部变量: 定义在函数内部的变量

```js
function fn() {
  var num = 10
}
console.log(num) // 报错
```

- 预解析: `es5`在解析代码之前把变量和函数的声明提前

```js
console.log(num) // undefined
var num = 10
```

- 预解析分段

```html
<script>
  console.log(num) // 报错 num is not defined
</script>
<script>
  console.log(num) // undefined
  var num = 10
</script>
```

- 作用域链: 变量使用的时候, 层层搜索

```js
function f1() {
  var num = 10
  function f2() {
    // var num = 20
    function f3() {
      // var num = 30
      // 变量使用时会一层一层的往上找
      console.log(num) // 10
    }
  }
}
```

<br>
<br>
<br>

## 闭包的作用及案例
---

?> `什么是闭包?` 函数A中有个函数B, 函数B可以访问函数A中的数据

<br>

- [闭包的作用](javascript:;): 延长作用域链, 延长变量的适用范围和时间

  - 优点: `缓存数据`
  - 缺点: `不能及时的释放, 消耗内存空间`

<br>

##### **案例1: 模拟点赞功能**

```js
// 获取所有按钮
var btns = document.querySelectorAll('button')

function f1() {
  var num = 0
  return function () {
    this.innerHTML = ++num
  }
}

// 循环遍历注册点击事件
for (item of btns) {
  var fn = f1()
  item.onclick = fn
}
```

!> 这里只是模拟了点赞的功能, 实际开发中点赞的数据是要存在数据库中的

<br>

##### **案例2: 点击按钮显示他排在第几个**

- 同样还是假设有五个按钮

- 最简单的思路就是直接在for循环中打印变量i, 但实际上每次打印的值都是5

```js
// 获取所有按钮
var btns = document.querySelectorAll('button')

// 循环遍历注册点击事件
for (var i = 0; i < btns.length; i++) {
  btns[i].onclick = function () {
    console.log(i)
  }
}
```

- 这次我们来使用闭包

```js
// 获取所有按钮
var btns = document.querySelectorAll('button')

// 循环遍历注册点击事件
for (var i = 0; i < btns.length; i++) {
  // 自调用函数
  (function (n) {
      btns[n].onclick = function() {
      console.log(n)
    }
  })(i)
}
```

!> 第二种写法是利用`函数的作用域`来缓存数据

<br>
<br>
<br>

## 递归的作用和注意问题
---

?> 递归就是一个函数调用其本身, 当条件满足时则退出循环

##### **演示: 遍历 DOM 树结构**

```js
// 获取html根元素
var root = document.documentElement

// 递归打印元素名称
function forEachDOM (node) {
  console.log(node.nodeName)
  for (item of node.children) {
    item.children && forEachDOM(item)
  }
}
forEachDOM(root)
```

<br>
<br>
<br>

<!-- ## 浅拷贝与深拷贝及注意事项 -->
<!-- --- -->

<!-- <br> -->
<!-- <br> -->
<!-- <br> -->
