- 把json对象转换成字符串`JSON.stringify()`
- 把字符串转换成json对象`JSON.parse()`

<br>

## Math 数字
---

##### **`Math.abs()`获取绝对值**

- **参数**

  - *{ Number }* `n` 任意数字

- **返回值**

  - 返回参数的绝对值

- **示例**

```js
Math.abs(-1) // 1
```

<br>

##### **`Math.ceil()`向上取整**

- **参数**

  - *{ Number }* `n` 任意数字

- **返回值**

  - 返回一个整数

- **示例**

```js
Math.abs(1.33) // 2
```

<br>

##### **`Math.floor()`向下取整**

- **参数**

  - *{ Number }* `n` 任意数字

- **返回值**

  - 返回一个整数

- **示例**

```js
Math.abs(1.66) // 1
```

<br>

##### **`Math.max()`获取最大值**

- **参数**

  - *{ Number }* `...n` 多个数字类型的参数

- **返回值**

  - 返回多个数字的最大值

- **示例**

```js
Math.abs(1, 2, 3) // 3
```

<br>

##### **`Math.min()`获取最小值**

- **参数**

  - *{ Number }* `...n` 多个数字类型的参数

- **返回值**

  - 返回多个数字的最小值

- **示例**

```js
Math.min(1, 2, 3) // 1
```

<br>

##### **`Math.random()`获取一个随机数**

- **参数**

  - 无

- **返回值**

  - 返回一个0-1的随机数

- **示例**

```js
Math.random() // 随机数字
```

<br>

##### **`Math.trunc()`获取整数部分**

- **参数**

  - *{ Number }* `n` 任意数字

- **返回值**

  - 返回一个数字的整数部分

- **示例**

```js
Math.trunc(3.15) // 3
```

<br>
<br>
<br>

## Date 时间
---

- Date对象基于1970年1月1日(世界标准时间)起的毫秒数

<br>

##### **`new Date()`获取当前时间**

- **参数**

  - *{ Date }* `date` 时间对象

- **返回值**

  - 返回一个时间对象

- **示例**

```js
const date = new Date() // 时间对象
```

<br>

##### **`getFullYear()`获取年份**

- **参数**

  - *{ Date }* `date` 时间对象

- **返回值**

  - 返回当前时间对象的年份

- **示例**

```js
date.getFullYear() // 2018(年)
```

<br>

##### **`getMonth()`获取月份**

- **参数**

  - *{ Date }* `date` 时间对象

- **返回值**

  - 返回当前时间对象的月份

- **示例**

```js
date.getMonth()+1 // 12(月)
```

<br>

##### **`getDate()`获取日期**

- **参数**

  - *{ Date }* `date` 时间对象

- **返回值**

  - 返回当前时间对象的日期

- **示例**

```js
date.getDate() // 1(日)
```

<br>

##### **`getHours()`获取小时**

- **参数**

  - *{ Date }* `date` 时间对象

- **返回值**

  - 返回当前时间对象的小时数

- **示例**

```js
date.getHours() // 10(时)
```

<br>

##### **`getMinutes()`获取分钟数**

- **参数**

  - *{ Date }* `date` 时间对象

- **返回值**

  - 返回当前时间对象的分钟数

- **示例**

```js
date.getMinutes() // 58(分)
```

<br>

##### **`getSeconds()`获取秒数**

- **参数**

  - *{ Date }* `date` 时间对象

- **返回值**

  - 返回当前时间对象的秒数

- **示例**

```js
date.getSeconds() // 13(秒)
```

<br>
<br>
<br>

## Array 数组
---

?> Array对象是用于构造数组的全局对象

##### **基本方法**

```javascript
//返回数组的长度
arr.length

//返回一个截取的数组
arr.slice(2,4)

//对数组进行排序
arr.sort()
```

##### **反转数组**

```javascript
arr.reverse()
数组的判断
//判断数组类型
Array.isArray(arr)
//等效于arr instanceof Array

//判断数组中是否包含这个值
arr.includes(5)

//如果存在,则返回第一个元素的下标,否则返回-1
arr.indexOf(5)

//如果存在,则返回最后一个元素的下标,否则返回-1
lastIndexOf(5)
```

##### **数组的遍历**

```javascript
//循环遍历
arr.forEach( x => console.log(x) )

//对数组进行遍历测试,通过返回true,否则false
arr.every( x => x>0 )

//对数组进行遍历测试,通过返回false,否则true
arr.some( x => x>0 )

//过滤数组,通过则返回当前元素
arr.filter( x => x>5 )

//找到数组中满足条件,的第一个元素的值
arr.find( x => x>5 )

//满足条件,则返回第一个元素的下标,否则返回0
arr.findIndex( x => x>5 )

//对每一个元素调用函数并返回新数组
arr.map( x => x+1 )

//对所有元素求和
arr.reduce( (x,y) => x+y )
//也可以拼接字符串
arr.reduce( (x,y) => x+","+y )
```

##### **对数组进行添加或删除**

```javascript
//删除数组中最后一个元素,并返回该元素
arr.pop()

//删除数组中第一个元素,并返回该元素
arr.shift()

//将指定元素添加到数组的开头
arr.unshift()

//将元素追加到数组的最后
arr.push()
```

##### **添加或删除指定元素**

```javascript
// 从索引为2的位置删除一项
arr.splice(2, 1)

// 在索引为2的位置插入10
arr.splice(2, 0, 10)

// 从索引为2的位置删除一项再插入10
arr.splice(2, 1, 10)
```

##### **数组的合并**

```javascript
//把若干参数合并为数组
Array.of(1,2,3)

//合并两个数组并返回
arr1.concat(arr2)
```

##### **数组的转换**

```javascript
//把字符串拆分成伪数组
Array.from("string")

//让数组以指定字符拼接
arr.join("-")

//把数组转换成字符串
arr.toString()

//可以转换时间,数字,字符串
arr.toLocaleString()
```

<br>
<br>
<br>

## String 字符串
---

?> String 全局对象是一个用于字符串或一个字符序列的构造函数

##### **查找/获取**

```javascript
// 获取字符串的长度
'hello'.length

// 获取指定索引的字符
'hello'.charAt(3)

// 获取指定字符首次出现的索引
'hello'.indexOf('l')

// 获取指定字符最后出现的索引
'hello'.lastIndexOf('l')

// 查找指定字符出现的位置
'hello'.search('l')
```

##### **截取字符串**

```javascript
// 截取指定索引字符串
'hello'.slice(0, -3)

// 截取指定长度的字符串
'hello'.substr(1, 3)

// 截取指定索引字符串
'hello'.substring(1, 3)
```

##### **替换/转换**

```javascript
// 对指定字符串进行替换
'hello'.replace('l', 'o')

// 把字符串分割成数组
'hello word'.split(' ')

// 大写转换小写
'HELLO'.toLowerCase()

// 小写转换大写
'hello'.toUpperCase()

// 大写转换小写(根据地区)
'HELLO'.toLocaleLowerCase()

// 小写转换大写(根据地区)
'hello'.toLocaleUpperCase()

// 把指定索引的字母转换成编码
'hello'.codePointAt(0)

// 把编码转换成字母
String.fromCodePoint(65)
```

##### **拼接/填充**

```javascript
// 拼接字符串
'hello'.concat('wo', 'rd')

// 以指定长度在后面进行重复填充
'hello'.padEnd(10, '-')

// 以指定长度在前面进行重复填充
'hello'.padStart(10, '-')

// 将字符串重复整数次
'hello'.repeat(2)
```

##### **判断**

```javascript
// 判断是否包含指定字符
'hello'.includes('ll')

// 判断是否已指定字符开头
'hello'.startsWith('he')

// 判断是否以指定字符结尾
'hello'.endsWith('lo')
```

##### **去除**

```javascript
// 去除两边空格
' hello '.trim()

// 去除左边空格
' hello '.trimLeft()

// 去除右边空格
' hello '.trimRight()
```

<br>
<br>
<br>

## Object 对象
---

- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object

### Object 构造函数
---

##### **`Object.create()`创建一个新对象并为其指定__proto__原型指向**

- **参数**

  - *{ Object }* `proto` 新创建对象的原型对象
  - *{ Object }* `propertiesObject` 新的可枚举属性(自身定义的属性，而不是其原型链上的枚举属性)

    - *{ String | Number | Object | Function }* `value` 指定属性的值
    - *{ Boolean }* `writable` 当前属性`是否可以修改`, 默认为false
    - *{ Boolean }* `configurable` 当前属性`是否可以被删除`, 默认为false
    - *{ Boolean }* `enumerable` 当前属性`是否能用 (for in) 枚举`, 默认为false

- **返回值**

  - 返回一个新的对象

- **示例**

创建一个新的对象, 并改变其原型指向

```js
const obj1 = { title: '资料' }

// 在控制台查看会发现obj2的proto指向了obj1
const obj2 = Object.create(obj1, {
  name: {
    // 属性的值
    value: '张三',
    // 当前属性是否可以修改, 默认为false
    writable: true,
    // 当前属性是否可以被删除, 默认为false
    configurable: true,
    // 当前属性是否能用for in枚举, 默认为false
    enumerable: true
  }
})
```

使用`Object.create()`实现类式继承

```js
// Parent 父类构造函数
function Parent() {
  this.x = 1
}

// 父类的原型方法
Parent.prototype.move = function (x) {
  this.x += x
  console.log(this.x)
}

// Child 子类的构造函数
function Child() {
  Parent.call(this)
}

// 子类续承父类
Child.prototype = Object.create(Parent.prototype)
Child.prototype.constructor = Child

new Child().move(1)
```

<br>

##### **`Object.assign()`通过复制一个或多个对象来创建一个新的对象**

将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象

> ES2015新增

- **参数**

  - *{ Object }* `target` 目标对象
  - *{ Object }* `...sources` 源对象(可以是多个, 如果具有相同的属性, 则会覆盖掉前面的)

- **返回值**

  - 返回目标对象

- **示例**

拷贝一个新的对象并返回

```js
const obj1 = {
  a: 1
}

const obj2 = Object.assign({}, obj1)

console.log(obj2) // { a: 1 }
```

在react中有更巧妙的用法, 可以很便利的只更改state中某一个对象的某一个属性

```jsx
class App extends React.Component {
  state = {
    obj: {
      a: 1,
      b: 2,
      c: 3
    }
  }

  async changeObj () {
    await this.setState({
      obj: Object.assign({}, this.state.obj, {c: 100})
    })
    console.log(this.state.obj)
  }
}
```

<br>
  
##### **`Object.defineProperty()`给对象添加一个属性并指定该属性的配置。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.defineProperties()`给对象添加多个属性并分别指定它们的配置。**

- **参数**

  - *{ Object }* `target` 目标对象
  - *{ Object }* `props` 定义新的可枚举属性或修改的属性

    - *{ String | Number | Object | Function }* `value` 定义属性的值
    -  *{ Boolean }* `configurable` 定义当前属性`是否可以被删除`, 默认为false
    - *{ Boolean }* `enumerable` 定义当前属性`是否可被枚举`, 默认为false
    - *{ Boolean }* `writable` 定义当前属性`是否可以修改`, 默认为false
    - *{ Function }* `get` 当前属性被使用时, 函数返回值将被用作属性的值
    - *{ Function }* `set` 函数将仅接受参数赋值给该属性的新值

- **返回值**

  - 返回目标对象

- **示例**

```js
const obj = {
  firstName: 'hello',
  lastName: 'world'
}

Object.defineProperties(obj, {
  fullName: {
    get: function () {
      return `${this.firstName} ${this.lastName}`
    },
    set: function (value) {
      this.firstName = value.split(' ')[0]
      this.lastName = value.split(' ')[1]
    }
  }
})

console.log(obj)
```

<br>
  
##### **`Object.entries()`返回给定对象自身可枚举属性的[key, value]数组。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.freeze()`冻结对象：其他代码不能删除或更改任何属性。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.getOwnPropertyDescriptor()`返回对象指定的属性配置。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.getOwnPropertyNames()`返回一个数组，它包含了指定对象所有的可枚举或不可枚举的属性名。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.getOwnPropertySymbols()`返回一个数组，它包含了指定对象自身所有的符号属性。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.getPrototypeOf()`返回指定对象的原型对象。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.is()`比较两个值是否相同。所有 NaN 值都相等（这与==和===不同）。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.isExtensible()`判断对象是否可扩展。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.isFrozen()`判断对象是否已经冻结。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.isSealed()`判断对象是否已经密封。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.keys()`返回一个包含所有给定对象自身可枚举属性名称的数组。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.preventExtensions()`防止对象的任何扩展。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.seal()`防止其他代码删除对象的属性。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.setPrototypeOf()`设置对象的原型（即内部[[Prototype]]属性）。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>
  
##### **`Object.values()`返回给定对象自身可枚举值的数组。**

- **参数**

- **返回值**

- **示例**

```js
// ...
```

<br>

<br>
<br>
<br>

## RegExp 正则表达式
---

?> 在js中通过内置对象`RegExp`来支持正则表达式

<br>

#### 实例化`RegExp`对象的两种方式
---

> 第一种 new`构造函数`来实例化

```js
/*
* 第一个参数为`正则表达式`
* 第二个参数为`修饰符`
*/

// 正则表达式写在注释符号中
var reg = new RegExp(/\bis\b/, 'g')

// 也可以写在字符串中
var reg = new RegExp('\\bis\\b', 'g')
```

<br>

> 第二种 通过`字面量`的方式定义正则表达式

```js
// 也同样写在注释符号中
var reg = /\bis\b/

// 修饰符直接写在最后即可
var reg = /\bis\b/g
```

<br>
<br>
<br>

#### 如何使用`正则表达式`
---

> `test`方法

```js
var reg = /\bis\b/
// 返回类型为 boolean 值, true表示通过验证
reg.test('she is a girl, he is a boy')
```

<br>

> `exec`方法

```js
var reg = /([1]+)([2]+)([3]+)/
// 返回值是一个数组
var res = reg.exec('112233')
// 可以得到匹配出来的结果
console.log(res)
```

<br>

> 字符串方法`replace`

- `replace`方法会对所有的匹配项进行替换操作

```js
// 只匹配一次
var reg = /\bis\b/
'she is a girl, he is a boy'.replace(reg, 'IS')

// 加上g表示匹配全文
var reg = /\bis\b/g
'she is a girl, he is a boy'.replace(reg, 'IS')

var str = '112233'
var reg = /([1]+)([2]+)([3]+)/
// 回调函数中可以得到分组每一项
str.replace(reg, (res, $1, $2, $3) => {
  console.log(res)
  console.log($1)
  console.log($2)
  console.log($3)
})
```

<br>
<br>
<br>

#### 修饰符
---

- `g` 全文搜索, 不添加

```js
var reg = /\bis\b/g
reg.test('she is a girl, he is a boy')
```

- `i` 忽略大小写, 默认是不忽略

- `m` 多行搜索

<br>

#### 元字符
---

- `.` 表示除了\n以外的任意单个字符

- `\d` 表示任意一个数字 *等同于[0-9]*

- `\D` 表示任意一个非数字

- `\s` 表示任意一个空白符号 *空格或tab键*

- `\S` 表示任意一个非空白符

- `\w` 表示任意一个非特殊符号 *等同于[0-9a-zA-Z_]* **`_`属于非特殊符号**

- `\W` 表示任意一个特殊符号

- `\b` 代表单词边界 *(空格)*

```js
// 匹配单词 hello
/\bhello\b/
```

- `[]` 表示的是范围之内中的一个 *也可以去掉元字符的意义*

```js
// 匹配任意一个数字
/[0-9]/

// 匹配任意一个字母
/[a-zA-Z]]/

// 匹配.jpg
/[.]jpg/
```

- `|` 表示或者的意思

```js
// 匹配任意数字或字母中的一个
/[0-9]|[a-zA-Z]/
```

- `()` 提升优先级或分组

```js
// 匹配 10-20 之间的数字
/(1[0-9])|[2][0]/
```

- `^` 表示以什么开始 或者 取反

```js
// 匹配以数字开头
/^[0-9]/

// 匹配非数字
/[^0-9]/
```

- `$` 表示以什么结尾

```js
// 匹配以数字结尾
/[0-9]$/
```

!> `/^[0-9]$/` 为严格模式

<br>

#### 限定符
---

- `*` 表示前面表达式出现0到多次

```js
// 出现0或多个数字
/[0-9]*/
```

- `+` 表示前面表达式出现1到多次

```js
// 出现1到多个数字
/[0-9]+/
```

- `?` 表示前面表达式出现0到1次

```js
// 出现0或者1个数字
/[0-9]?/
```

- `{}` 表示前面表达式出现的次数 *可以是指定次数, 也可以是范围*

```js
// 出现11次数字 (手机号)
/[0-9]{11}/

// 出现0或多个数字
/[0-9]{0,}/

// 出现6-10次数字
/[0-9]{6,11}/
```

!> 这里有个错误写法~~`/[0-9]{,5}/`~~ 因为逗号前面不能为空

<br>
<br>
<br>

## Function 全局对象
---

?> 全局对象只是一个对象，而不是类，既没有构造函数，也无法实例化一个新的全局对象

```js
// 把对象的值转换为数字
Number()

// 解析一个字符串并返回一个浮点数
parseFloat()

// 解析一个字符串并返回一个整数
parseInt()

// 把对象的值转换为字符串
String()
```
