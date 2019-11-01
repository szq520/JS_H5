
## Connection 连接数据库
---

<br>

> 连接数据库

```js
// 加载模块
const mongoose = require('mongoose')

// 连接数据库
mongoose.connect(
  "mongodb://账号:密码@127.0.0.1:27017/数据库?authSource=admin&authMechanism=SCRAM-SHA-1",
  { useNewUrlParser: true }, function (err) {
    if (err) {
      return console.log('error:' + err)
    }
    console.log('success!')
})
```

> 监听连接成功

```js
// 监听连接成功
mongoose.connection.on('connected', () => {
  console.log('连接成功')
})
```

> 监听连接失败

```js
// 监听连接失败
mongoose.connection.on('error', () => {
  console.log('连接失败')
})
```

> 监听断开连接

```js
// 监听断开连接
mongoose.connection.on('disconnected', () => {
  console.log('断开连接')
})
```

<br>
<br>
<br>

## Model & Schema 对象
---

- 其中的`Schema`对象还可以有更详细的参数

  - `type` 类型 *String | Number | Array | Date | Boolean*
  - `default` 默认值 *string*
  - `trim` 去除两边空格 *boolean*
  - `unique` 唯一索引 *boolean*
  - `index` 辅助索引 *boolean*
  - `set` 存储之前的逻辑 *function*
  - `get` 读取之前的逻辑 *function*
  - `userSchema.virtual` 虚拟属性

- 又或者可以通过 [Mongoose 验证器](/node-mongoose?id=mongoose-验证器) 定义数据的校验规则

> 示例

```js
// 加载模块
const mongoose = require('mongoose')

// 定义模型
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
  nickname: {
    // 类型
    type: String,
    // 默认值
    default: 'new user',
    // 去除两边空格
    trim: true,
    // 辅助索引可以增加查询速度
    index: true
  },
  phone: {
    type: Number,
    // 唯一索引可以保证是否唯一
    unique: true
  },
  age: {
    type: Number,
    // 存储之前的逻辑
    set: function (age) {
      // ...
      return age
    },
    // 读取之前的逻辑
    get: function (age) {
      // ...
      return age
    }
  },
  createdAt: {
    type: Date,
    // 默认值
    default: Date.now
  }
}, { collection: 'user' })

// 定义一个虚拟属性
userSchema.virtual('fullName').get(function () {
  // this表示当前对象
  return this.firstName + ' ' + this.lastName
})

// 设置当转换成json数据时, 把虚拟属性也添加进去
userSchema.set('toJSON', {
  getters: true,
  virtual: true
})

// 创建模型并导出
module.exports = mongoose.model('User', userSchema)
```

<br>
<br>
<br>

## Mongoose 验证器
---

- 在mongoose中如果要实现数据校验的功能, 那我们需要了解一下验证器

<br>

#### 预定义的验证器

- 所有类型

  - `required` 必须字段 *boolean*

- Number 类型

  - `min` 最小值 *number*
  - `max` 最大值 *number*

- String 类型

  - `enum` 枚举 *array*
  - `match` 包含的值 *正则表达式*

> 示例

```js
const userSchema = new mongoose.Schema({
  nickname: {
    type: String,
    require: true
  },
  sex: {
    type: String,
    enum: ['男', '女', '保密']
  }
  age: {
    type: Number,
    require: true,
    min: 1,
    max: 100
  }
})
```

<br>

#### 自定义的验证器

- 所有类型

  - `validate` 自定义逻辑 *function*

> 示例

```js
const userSchema = new mongoose.Schema({
  desc: {
    type: String,
    validate: function (desc) {
      if (desc.length != 0) {
        return true
      } else {
        return false
      }
    }
  }
})
```

<br>
<br>
<br>

## Mongoose 内置方法
---

> save 保存

```js
// 加载模型
const User = require('../models/user')

let user = new User({
  name: 'jack',
  sex: '男',
  age: 18
})

// 保存
user.save((err) => {
  if (err) {
    return console.log('save failed')
  }
  console.log('save success')
})
```

<br>

> find 查询

```js
// 加载模型
const User = require('../models/user')

// 第一个参数为查询条件
User.find({}, (err, data) => {
  if (err) {
    return console.log('error')
  }
  console.log(data)
})
```

<br>

> find 排序查询

```js
// 加载模型
const User = require('../models/user')

// 使用exec来处理回调
User.find().sort(age: -1).exec((err, data) => {
  if (err) {
    return console.log('error')
  }
  console.log(data)
})
```

<br>

> findOne 查询一条

返回满足条件的第一条数据

```js
// 加载模型
const User = require('../models/user')

// 第一个参数为查询条件
User.findOne({ name: 'jack' }, (err, data) => {
  if (err) {
    return console.log('error')
  }
  console.log(data)
})
```

<br>

> remove 删除

```js
// 加载模型
const User = require('../models/user')

User.findOne({ name: 'jack' }, (err, data) => {
  if (err) {
    return console.log('error')
  }
  // 如果存在就删除
  if (data) {
    data.remove()
  }
})
```

<br>
<br>
<br>

## Mongoose 自定义方法
---

### 静态方法

- 静态方法不依赖于具体的实例对象, 不需要new对象即可使用

> 示例

```js
const bookSchema = new mongoose.Schema({
  bookName: String,
  bookId: Number
})

// 根据bookid查询数据
bookSchema.statics.findByBookId = (bookId, callback) => {
  this.findOne({ bookId: bookId }, (err, res) => {
    callback(err, res)
  })
}

const Book = mongoose.model('Book', bookSchema)

Book.findByBookId(1234, (err, res) => {
  console.log(res)
})
```

<br>

### 实例方法

- 实例方法需要new一个具体的实例对象, 再通过实例对象进行调用

> 示例

```js
const bookSchema = new mongoose.Schema({
  bookName: String,
  bookId: Number
})

bookSchema.methods.print = () => {
  console.log('书名: '+this.bookName+'编号: '+this.bookId)
}

// 打印基本信息
const Book = mongoose.model('Book', bookSchema)

const book = new Book({
  bookName: '这是一本书',
  bookId: 1234
})

book.save((err) => {
  if (err) return console.log(err)
  book.print()
})
```

<br>
<br>
<br>

## Mongoose 中间件
---

- 文档中间件

  - `init `
  - `validate`
  - `save` 存储
  - `remove` 删除

- 查询中间件

  - `count` 统计
  - `find` 查询
  - `findOne` 查询一条
  - `update` 更新
  - `findOneAndRemove` 查询一条并删除
  - `findOneAndUpdate` 查询一条并更新

- 预处理中间件

  - `pre` 执行之前调用

- 后置处理中间件

  - `post` 执行之后调用

> 示例

```js
const userSchema = new mongoose.Schema({
  address: String
})

// 预处理中间件
userSchema.pre('save', (next) => {
  console.log('保存之后')
  next()
})

// 后置处理中间件, 如果多一个参数, 可以并列执行一个方法
userSchema.post('save', true (next, done) => {
  console.log('保存之后')
  next()
  // 执行第二个方法
  done()
})

const User = mongoose.model('User', userSchema)

const user = new User({
  address: '北京市 顺义区 99号'
})

user.save()
```

<br>
<br>
<br>

## DBRef 关联查询
---

在mongoose中, DERef可以实现不同集合之间的数据交叉引用, 相当于mysql中的联表查询

- `populate()` 方法

```js
const User = mongoose.model('User', {
  nickname: String
})

const News = mongoose.model('News', {
  title: String,
  author: {
    // 类型
    type: mongoose.Schema.ObjectId,
    // 指定关联哪一个集合
    ref: 'User'
  }
})

const user = new User({
  nickname: 'jack'
})

const news = new News({
  title: '这是一条新闻',
  author: user
})

user.save((error) => {
  if (error) return console.log(error)
  // 当user保存成功后
  news.save((err) => {
    if (err) return console.log(err)
    News.findOne().populate('author').exec((err, res) => {
      console.log(res)
    })
  })
})
```
