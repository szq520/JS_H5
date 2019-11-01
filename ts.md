
## 类型
---

##### **基本类型`string`|`number`|`boolean`|`undefined`|`null`**

```ts
let str: string = 'hello' // 字符串
let num: number = 100 // 数字
let login: boolean = true // 布尔

let u: undefined = undefined // undefined
let n: null = null // null
```

<br>

##### **数组类型`array`**

```ts
// 两种声明方式
let arr: number[] = [1, 2, 3, null, undefined]
let list: Array<number> = [4, 5, 6]
```

<br>

##### **元组类型**

```ts
let x: [string, number] = ['99', 99]
let y: [string, number] = [null, undefined]
```

<br>

##### **枚举类型`enum`**

```ts
enum Color {Red = 1, Green = 2, Blue = 3}
let c: Color = Color.Red // 1
let colorName: string = Color[2] // 'Green'
```

<br>

##### **Any类型`any`**

```ts
let any1: any = 'world' // 变量类型可以随意切换
let any2: any[] = [1, 'str', true] // 或者声明一个类型不确定的数组
```

<br>

##### **Void类型`void`**

```ts
function fn(): void { // 当函数没有返回值的时候, 其类型是void
  console.log('hello world')
}
let foo: void = undefined // void类型只能赋undefined和null
```

<br>

##### **Never类型`never`**

```ts
function err (msg: string): never { // 抛出异常
  throw new Error(msg)
}
function loop (): never { // 死循环
  while (true) {}
}
```

<br>

##### **Objeck类型`object`**

```ts
let obj1: object = {a: 1}
let obj2: object = null
```

<br>

##### **类型断言`< >`|`as`**

```ts
let bar: any = 'hello 404'
let barLength1 = (<string>bar).length // 第一种方式
let barLength2 = (bar as string).length // 第二种方式(jsx语法只能使用该种方式)
```

<br>
<br>
<br>

## 接口
---

##### **接口的使用**

```ts
function fn (params: {id: number}) {
  console.log(params.id)
}
const obj = { id: 1, name: '404' }
fn({id: 1})
```

```ts
interface PropsType {
  id: number
  name: string
}
function fn (params: PropsType) {
  console.log(params.id)
}
const obj = { id: 1, name: '404' }
fn(obj)
```

<br>

##### **可选属性`?`**

```ts
interface Style {
  color?: string
  width?: number
}
function fn (style: Style): {color: string, area: number} {
  return {
    color: style.color ? style.color : '#fff',
    area: style.width ? style.width * style.width : 100
  }
}
const obj = { width: 20 } // 传参时并没有传color
fn(obj)
```

<br>

##### **只读属性`readonly`**

```ts
interface Point {
  readonly x: number
  readonly y: number
}
let p: Point = { x: 10, y: 5 }
p.x = 20 // 报错: 只读属性不能修改
```

<br>

##### **数组的只读`ReadonlyArray`**

```ts
let a: number[] = [1, 2, 3]
let b: ReadonlyArray<number> = a

b[0] = 10 // error
b.push(10) // error
b.length = 10 // error
a = b // error 只读的数组, 也不可以进行赋值
a = a as number[] // success 但是可以利用断言重写
```

<br>

##### **函数类型**

```ts
interface FuncType {
  (x: number, y: number): boolean
}

let fn: FuncType
fn = function (x: number, y: number) {
  return x > y
}
```
