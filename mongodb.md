


# MongoDB 与传统 MySQL 的区别
---

> 关系型数据库可以说是更严谨的, 可靠性更强的数据库

- ##### [关系型数据库](javascript:;)
  - 优点
    1. `结构稳定, 修改不易, 经常需要联表查询`
    1. `一致性高, 由于并发高, 在数据同步的时候一般采用锁来保证数据的可靠性`
    1. `查询能力高, 可以操作很复杂的查询`
    1. `表具有逻辑性, 易于理解`

  - 缺点
    2. `不适用高并发读写`
    2. `不适用海量数据高效读写`
    2. `层次多，扩展性低`
    2. `维护一致性开销大`
    2. `涉及联表查询，复杂，慢`

> 非关系型数据库胜在处理大数据的速度，但是对于数据的准确度没有那么高

- ##### [非关系型数据库](javascript:;)
  - 优点
    1. `数据之间没有关系，所以易扩展，也易于查询`
    1. `数据结构灵活，每个数据都可以有不同的结构`
    1. `由于降低了一致性的要求，所以查询速度更快`

  - 缺点
    2. `数据的准确度没有那么高`

<br>

## Win10 安装 MongoDB 相关配置
---

?> 官网下载安装包然后傻瓜式安装, 安装路径也使用默认目录安装在C盘

!> 需要注意`win7系统`环境下只能安装`mongodb 3.2`版本

<br>

- 在该目录下`c:\mongodb\`新建三个文件夹

```
├── data
├── etc
│   └── mongo.conf
└── logs
    └── mongodb.log
```

<br>

- 同时在`mongo.conf`文件中添加如下配置

```shell
# 数据库路径
dbpath=c:\mongodb\data\
# 日志输出文件路径
logpath=c:\mongodb\logs\mongodb.log
# 错误日志采用追加模式，配置这个选项后mongodb的日志会追加到现有的日志文件，而不是从新创建一个新文件
logappend=true
# 启用日志文件，默认启用
journal=true
# 这个选项可以过滤掉一些无用的日志信息，若需要调试使用请设置为false
quiet=true
# 端口号 默认为27017
port=27017
# 指定存储引擎（默认win10不加此引擎，如果是win7再加进去）
# storageEngine=mmapv1
```

<br>

- 然后把`C:\Program Files\MongoDB\Server\4.0\bin`添加到环境变量当中

  - 打开命令行输入`mongod --config c:\mongodb\etc\mongo.conf --install --serviceName "MongoDB"`

  - 在控制面板的服务设置当中`手动`开启服务后再次输入`mongo`进入数据库


<br><br><br>

## Linux 安装 MongoDB 并开启权限验证
---

?> mongodb是属于非关系型数据库, 与mysql之间是有区别的

<br>

> 开始安装

- 第一步, 添加mongodb的yum源

  - `vim /etc/yum.repos.d/mongodb-3.4.repo`

  - 进入文件后按`i`进入编辑模式, 将以下内容粘贴进去

```shell
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<br>

- 第二步, 使用yum进行安装

  - `yum install -y mongodb-org`

  - 当看到 Complete! 表示安装成功

    - 可以输入`mongo --version`查看版本

<br>

!> 最后还要给你的数据库`创建账号和密码`

  - 首先要创建一个超级管理员, 这个账户不仅可以读写任何数据库, 还可创建或删除用户
    
    - 进入admin数据库`use admin`

    - 创建超级管理员`db.createUser({ user: "用户名", pwd: "密码", roles: ["root"] })`

    - 退出mongo数据库`exit`, 并关闭mongo服务`systemctl stop mongod.service`

    - 开启授权`/usr/bin/mongod -f /etc/mongod.conf --auth`

    - 接下来进入数据库`mongo`, 输入`show dbs`发现没有任何权限读写权限了
    
    - 我们进入`use admin`然后授权登录`db.auth("用户名", "密码")`, 就可以随意操作了

<br>

权限名称 | 权限说明
:--: | :--:
Read                 | 允许用户读取指定数据库
readWrite            | 允许用户读写指定数据库
dbAdmin              | 允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问system.profile
userAdmin            | 允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
clusterAdmin         | 只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。
readAnyDatabase      | 只在admin数据库中可用，赋予用户所有数据库的读权限
readWriteAnyDatabase | 只在admin数据库中可用，赋予用户所有数据库的读写权限
userAdminAnyDatabase | 只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
dbAdminAnyDatabase   | 只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。
root                 | 只在admin数据库中可用。超级账号，超级权限

> 也可以单独创建一个只能读写`指定数据库`的用户

```shell
db.createUser({
  user: '用户名',
  pwd: '密码',
  roles:[
    { role: 'dbAdmin', db: '指定数据库' },
    { role: 'readWrite', db: '指定数据库' }
  ]
})
```

<br>

- mongodb 的相关操作

  - 启动服务:`systemctl start mongod.service`

  - 停止服务:`systemctl stop mongod.service`

  - 进入数据库:`mongo 127.0.0.1:27017`

  - 查看所有用户:`db.system.users.find()`

  - 删除指定用户:`db.dropUser("user")`

<br>
<br>
<br>


## 增、删、改、查
---

> 选择数据库

- 如果有该数据库会进入, 如果没有则`自动创建`

```
use 数据库名称
```

<br>

> 查看数据库

```
show databases
```
```
show dbs
```

<br>

> 查看集合(查看数据表)

```
show collections
```
```
show tables
```

<br>
<br>
<br>

### 增加
---

> 插入数据

- 如果没有该集合, 则依然会`自动创建`

```js
db.user.insert({ name: 'jack', age: 20 });
```

- 使用`js`插入数据

```js
var addData = function () {
  for (var i = 0; i < 5; i++) {
    db.user.insert({ name: 'ben', sex: 22+i });
  }
}
```

<br>
<br>
<br>

### 删除
---

> 删除所有

```js
db.user.remove({})
```

<br>

> 删除所有符合条件的

```js
db.user.remove({ age: 10 })
```

<br>

> 只删除第一个符合条件的

- 参数: `justOne`

```js
db.user.remove(
  { age: 99 },
  { justOne: true }
)
```

<br>

> 删除集合

```
db.user.drop()
```

> 删除数据库

- 删除时`必须进入该数据库`才能删除, 因为db表示的是当前数据库

```
db.dropDatabase()
```

<br>
<br>
<br>

### 修改
---

?> 前者是条件, 后者是要更新的数据

<br>

> 覆盖更新

- 其他非id字段消失, 只保存更新后的数据

```js
db.user.update(
  {name: 'ben'},
  {age: 100}
)
```

<br>

> 更新指定的字段

- 参数: `$set`

```js
db.user.update(
  { name: 'ben' },
  {
    '$set': { age: 100 }
  }
)
```

<br>

> 指定字段增加多少

- 参数: `$inc`

```js
db.user.update(
  { name: 'ben' },
  {
    '$inc': { age: -1 }
  }
)
```

<br>

> 更新所有符合条件的

- 参数: `multi`为true时更新所有符合条件的数据, 为false时只更新符合条件的第一条数据

```js
db.user.update(
  { name: 'ben' },
  { '$set': { age: '99' } },
  { multi: true }
)
```

<br>

> 如果没有符合条件, 就插入该条数据

- 参数: `upsert`

```js
db.user.update(
  { name: 'nike' },
  { age: 18 },
  { upsert: true }
)
```

<br>

> 也可以简写为

- 第三个参数为`upsert`的值, 第四个参数为`multi`的值

```js
db.user.update(
  { name: 'nike' },
  { age: 18 },
  false,
  true
)
```

<br>

!> id创建之后是不可以被修改的

<br>
<br>
<br>

### 查询
---

> 查询所有

```js
db.user.find()
```

<br>

> 查询年龄`等于`20岁的数据

- 参数:`$eq`（等于）

```js
db.user.find({
  age: { '$eq': 20 }
})
```

<br>

> 查询年龄`不等于`20岁的数据

- 参数:`$ne`（不等于）

```js
db.user.find({
  age: { '$ne': 20 }
})
```

<br>

> 查询年龄`小于`20岁的数据

- 参数:`$lt`（小余）

```js
db.user.find({
  age: { '$lt': 20 }
})
```

<br>

> 查询年龄`小余等于`20岁的数据

- 参数:`$lte`（小余等于）

```js
db.user.find({
  age: { '$lte': 20 }
})
```

<br>

> 查询年龄`大余`20岁的数据

- 参数:`$gt`（大余）

```js
db.user.find({
  age: { '$gt': 20 }
})
```

<br>

> 查询年龄`大余等于`20岁的数据

- 参数:`$gte`（大余等于）

```js
db.user.find({
  age: { '$gte': 20 }
})
```

<br>

> 查询年龄`包含`20, 21, 22岁的数据

- 参数:`$in`（包含）

```js
db.user.find({
  age: {
    '$in': [20, 21, 22]
  }
})
```

<br>

> 查询年龄`不包含`20, 21, 22岁的数据

- 参数:`$nin`（不包含）

```js
db.user.find({
  age: {
    '$nin': [20, 21, 22]
  }
})
```

<br>

> 查询姓名为jack`并且`年龄为20岁的数据

- 参数:`$and`（并且）

```js
db.user.find({
  '$and': [
    { name: 'jack' },
    { age: 20 }
  ]
})
```

<br>

> 查询姓名为jack`或者`年龄为20岁的数据

- 参数:`$or`（或者）

```js
db.user.find({
  '$or': [
    { name: 'jack' },
    { age: 20 }
  ]
})
```

<br>

> 查询`前5条`数据

- 方法:`limit()`

```js
db.user.find().limit(5)
```

<br>

> 查询`第6-10`条数据

- 方法:`skip()`

```js
db.user.find().skip(5).limit(5)
```

<br>

> `统计`查询到结果的数据

- 方法:`count()`

```js
db.user.find().count()

db.user.find().skip(5).limit(5).count(true)
```

- 方法:`size()`

```js
db.user.find().skip(5).limit(5).size()
```

<br>

> 对年龄进行`排序`显示

- 方法:`sort()`

  - 升序为`1`

  - 降序为`-1`

```js
db.user.find().sort({ age: -1 })
```

<br>

> 查询的结果中, `只返回`name字段

- 在第二个集合中

  - 设置`1`时, 返回

  - 设置`0`时, 不返回

```js
db.user.find({}, { name: 1 })

// 指定id不返回
db.user.find({}, { _id: 0 })
```

!> 除了_id可以随意设置, 其他字段的值必须统一

<br>
<br>
<br>

## aggregate 聚合
---

?> MongoDB中聚合(aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果

<br>

### 条件查询
---

- 参数:`$match`

  - 使用查询的条件与`find()`基本一致

```js
db.user.aggregate({
  '$match': { age: 25 }
})
```
<br>

> 查询20岁名叫jack的

```js
db.user.aggregate({
  '$match': {
    '$and': [
      { age: 20 },
      { name: 'jack' }
    ]
  }
})
```

<br>

> 查询25-30岁名叫ben的

```js
db.user.aggregate({
  '$match': {
    '$and': [
      {
        age: { '$lt': 30 }
      }, {
        age: { '$gt': 25 }
      }, {
        name: 'ben'
      }
    ]
  }
})
```

<br>
<br>
<br>

### 分组查询
---

> 对姓名进行`分组`

- 参数:`$group`

```js
db.user.aggregate({
  '$group': { _id: '$name' }
})
```

<br>

> 对姓名进行`分组`, 并对年龄进行`求和`

- 参数:`$sum`

```js
db.user.aggregate({
  '$group': {
    _id: '$name',
    ageSum: { '$sum': '$age' }
  }
})
```

<br>

> 对姓名进行`分组`, 并显示年龄的`最大值`

- 参数:`$max`

```js
db.user.aggregate({
  '$group': {
    _id: '$name',
    ageMax: { '$max': '$age' }
  }
})
```

<br>

> 对姓名进行`分组`, 并显示年龄的`最小值`

- 参数:`$min`

```js
db.user.aggregate({
  '$group': {
    _id: '$name',
    ageMin: { '$min': '$age' }
  }
})
```

<br>

> 对姓名进行`分组`, 并显示年龄的`平均值`

- 参数:`$avg`

```js
db.user.aggregate({
  '$group': {
    _id: '$name',
    ageAvg: { '$avg': '$age' }
  }
})
```

<br>
<br>
<br>

### 排序查询
---

> 对年龄进行`升序`排序

- 参数:`$sort`

  - 升序为`1`

```js
db.user.aggregate({
  '$sort': { age: 1 }
})
```

<br>

> 对年龄进行`降序`排序

- 参数:`$sort`

  - 降序为`-1`

```js
db.user.aggregate({
  '$sort': { age: -1 }
})
```

<br>
<br>
<br>

### 复杂查询
---

> 对年龄小于20的进行降序

```js
db.user.aggregate([
  {
    '$match': {
      age: { '$lt': 20 }
    }
  },{
    '$sort': { age: -1 }
  }
])
```

<br>

> 对25-30岁之间的人, 以姓名进行分组, 并显示平均年龄

```js
db.user.aggregate([
  {
    '$match': {
      '$and': [
        {
          age: { '$lt': 30 }
        }, {
          age: { '$gt': 25 }
        }
      ]
    }
  }, {
    '$group': {
      _id: '$name',
      ageAvg: {
        '$avg': '$age'
      }
    }
  }
])
```

<br>

> 对大于30岁的人, 以姓名进行分组, 并升序显示最大年龄

```js
db.user.aggregate([
  {
    '$match': {
      age: { '$gt': 30 }
    }
  }, {
    '$group': {
      _id: '$name',
      ageMax: {
        '$max': '$age'
      }
    }
  }, {
    '$sort': { ageMax: 1 }
  }
])
```

<br>
<br>
<br>

## mapReduce 批量操作
---

?> `db.user.mapReduce(map, reduce, {})`其中前两个参数`map`和`reduce`是方法, 第三个参数是对数据如何处理

> `map`的作用是遍历所有数据, 然后通过`emit(key, val)`把数据保存为一个二维数组传递下去
  
  - `this`表示当前数据

  - 其格式为`[key1: [val1, val2, val3]], [key2: [val1, val2, val3]]`

<br>

> `reduce`的作用是拿到`map`传递来的数据根据业务需求进行一系列复杂操作

  - `reduce`可以拿到两个参数(key, val), 对其中的二维数据进行操作

  - 示例: `function (key, val) { return Array.sum(val) }`

<br>

> 第三个参数

  - 把数据打印出来`{ out: { inline: 1 } }`

  - 保存到指定集合`{ out: { replace: 'temp_user'} }`