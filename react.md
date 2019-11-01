
> todoMVC 小案例 `git clone https://github.com/tastejs/todomvc-app-template.git --depth=1 todomvc`

### 搭建简易的测试环境
---

?> 测试环境并不等同于生产环境! 以下的方式只限于写小demo时用到

- 先初始化`npm init -y`

- 再安装需要的包`npm i react@16.7.0 react-dom@16.7.0 @babel/standalone@7.0.0`

接下来依次引入刚刚安装的包

```html
<script src="./node_modules/@babel/standalone/babel.js"></script>
<script src="./node_modules/react/umd/react.development.js"></script>
<script src="./node_modules/react-dom/umd/react-dom.development.js"></script>
```

最后就可以在`<script type="text/babel"></script>`标签中进行书写`JSX`语法了

!> 但是需要注意的是, 必须以服务端的方式启动`index.html`, 本地直接打开会报错

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <div id="app"></div>
  <script src="./node_modules/@babel/standalone/babel.js"></script>
  <script src="./node_modules/react/umd/react.development.js"></script>
  <script src="./node_modules/react-dom/umd/react-dom.development.js"></script>
  <script type="text/babel">
    ReactDOM.render(<h1>JSX语法</h1>, document.getElementById('app'))
  </script>
</body>
</html>
```

- jsx语法里面需要注意的一些问题

  - 类样式`class`改为`className`
  - label标签中的`for`改为`htmlFor`
  - input标签中的`autofocus`改为`autoFocus`
  - input标签中的`checked`改为`defaultChecked`
  - input标签中的`value`改为`defaultValue`

<br>

### 使用JSX语法
---

> 渲染一个标签

```jsx
class App extends React.Component {
  render() {
    return (
      <h1>Hello</h1>
    )
  }
}
```

> 渲染变量

```jsx
let name = 'jack'
let age = 18
let sex = true

class App extends React.Component {
  render() {
    return (
      <div>
        <p>{name}</p>
        <p>{age + 2}</p>
        <p>{sex ? '男' : '女'}</p>
      </div>
    )
  }
}
```

!> 变量中既可以存普通字符串, 还可以存DOM元素

```jsx
const ul = <ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ul>

class App extends React.Component {
  render() {
    return (
      <div>
        {ul}
      </div>
    )
  }
}
```

> 渲染元素的属性

```jsx
let title = '这是一个p标签'

class App extends React.Component {
  render() {
    return (
      <div>
        <p title="这是一个p标签"></p>
        <p title={title}></p>
      </div>
    )
  }
}
```

!> 有两种特殊的属性需要注意

```jsx
class App extends React.Component {
  render() {
    return (
      <div>
        {/* class类样式需要改成className */}
        <p className="box"></p>
        {/* for属性需要改成htmlFor */}
        <label htmlFor="inp"></label>
      </div>
    )
  }
}
```

> 循环渲染一个数组

```jsx
let arr = [1,2,3,4]

class App extends React.Component {
  render() {
    return (
      <div>
        {arr.map(item => <h1 key={item}>{item}</h1>)}
      </div>
    )
  }
}
```

<br>

### 渲染style行内样式
---

```jsx
class App extends React.Component {
  render() {
    return (
      <div>
        <p style={{color: 'red', fontSize: '20px'}}>这是p标签</p>
      </div>
    )
  }
}
```

<br>

### 创建组件的方式
---

> 使用`es5`构造函数来创建组件

```jsx
function Hello (props) {
  return <div>hello</div>
}

class App extends React.Component {
  render() {
    return (
      <div>
        <Hello></Hello>
      </div>
    )
  }
}
```

> 使用`es6`的class来创建组件

- 如果使用`class`定义组件, 必须让组件继承自`React.Component`

```jsx
class Hello extends React.Component {
  render () {
    return <div>标签</div>
  }
}
```

<br>

### 在组件中传递数据
--- 

> 在组件中传递变量

```jsx
function Hello (props) {
  return (
    <div>
      <p>{props.name}今年{props.age}岁</p>
      <p>{props.children}</p>
    </div>
  )
}

class App extends React.Component {
  render() {
    return (
      <div>
        <Hello name="张三" age="18">标签</Hello>
      </div>
    )
  }
}
```

> 在组件中传递对象

```jsx
function Hello (props) {
  return <div>{props.name}今年{props.age}岁, 是{props.sex}孩</div>
}

const obj = {
  name: '张三',
  age: 18,
  sex: '男'
}

class App extends React.Component {
  render() {
    return (
      <div>
        <Hello {...obj}></Hello>
      </div>
    )
  }
}
```

> 给class定义的组件传递数据

```jsx
const obj = {
  name: '张三',
  age: 18,
  sex: '男'
}

// 在class创建的组件中, 直接通过this.props即可拿到传递的数据
class Hello extends React.Component {
  render () {
    return (
      <div>{this.props.name}今年{this.props.age}岁, 是{this.props.sex}孩</div>
    )
  }
}
```

<br>

## 有状态组件和无状态组件
---

?> 只有通过class定义的组件才能定义自己状态, 也就是说通过构造函数定义的组件就是无状态组件

> 有状态组件通过`state`来存储数据

```jsx
class App extends React.Component {
  constructor () {
    super()
    // this.state相当于vue中的data
    this.state = {
      msg: '私有的消息'
    }
  }

  render () {
    return (
      <div>{this.state.msg}</div>
    )
  }
}
```

<br>

## 在组件中注册点击事件
---

> 调用方法

```jsx
class App extends React.Component {
  render() {
    return (
      <div className="App">
        <button onClick={this.sayHi}>按钮</button>
      </div>
    )
  }
  // 定义一个方法
  sayHi () {
    console.log('hello')
  }
}
```

> 事件传参

```jsx
class App extends React.Component {
  render() {
    return (
      <div className="App">
        <button onClick={() => { this.sayHi('传参') }}>按钮</button>
      </div>
    )
  }

  sayHi (arg) {
    console.log(arg)
  }
}
```

<br>

## 子组件调用父组件的方法
---

```jsx
// 子组件 (无状态组件)
function MyBtn (props) {
  return (
    <button onClick={props.myclick}>按钮</button>
  )
}

// 父组件
class App extends React.Component {
  render () {
    return (
      <div className="App">
        <MyBtn myclick={() => this.sayHi()}></MyBtn>
      </div>
    )
  }
  sayHi () {
    console.log('父组件的方法被调用了')
  }
}
```

<br>

## 使用fetch发送ajax获取数据
---

```js
fetch(url, options).then(function(response) { 
// handle HTTP response
}, function(error) {
 // handle network error
})
```

<br>

## 生命周期函数
---

- `constructor()` 是ES6的class构造器, 并不属于`react`生命周期, 但是组件的状态和props会定义在构造器里

```js
class App extends React.Component {
  constructor (props) {

    super(props)
    // 可以得到父级传递来的数据
    console.log(props)

    // 定义该组件的状态
    this.state = {
      name: '张三',
      age: 18,
      sex: '男'
    }
  }
}
```

- [组件渲染](javascript:;)

  - `componentWillMount()` 当前组件即将渲染
  
    - 下面的是关于为什么不在该生命周期中进行ajax请求数据的一些说法

    - 获取数据肯定是以异步方式进行，不会阻碍组件渲染（只会耽误请求发送这个时间），然后接着渲染，等异步返回数据后，如果成功再进行setState操作，setState是将更新的状态放进了组件的__pendingStateQueue队列，react不会立即响应更新，会等到组件挂载完成后，统一的更新脏组件（需要更新的组件）。放在constructor或者componentWillMount里面反而会更加有效率。

    - 再说说React-Redux，要想让组件更新，必须要有用connect(...)(yourComponent)封装的容器（高阶）组件，这个组件会监听store变化，内部调用setState触发你的组件更新。数据处理都是通过dispatch(action)进行,自己并不会在组件的声明周期内直接ajax获取取数据。使用redux这个问题就成为了再组件声明周期的哪个节阶段dispatch(action)获取数据才合理？

    - 总结：
      - 跟服务器端渲染（同构）有关系，如果在componentWillMount里面获取数据，fetch data会执行两次，一次在服务器端一次在客户端。在componentDidMount中可以解决这个问题。
      - 在componentWillMount中fetch data，数据一定在render后才能到达，如果你忘记了设置初始状态，用户体验不好。
      - react16.0以后，componentWillMount可能会被执行多次。

  - `render()` 渲染并更新DOM元素以及子组件, 不能在该组件中发送ajax, 否则会陷入死循环

  - `componentDidMount()` 组件渲染完毕, 一般都是在该组件中发送ajax请求数据

- [组件更新](javascript:;)

  - `componentWillReceiveProps(nextProps)` 组件发生改变时触发, 参数里可以拿到更新之后的事件和数据

  - `shouldComponentUpdate(nextProps, nextState)` 控制组件是否被重新渲染, return true则更新组件, return false则阻止更新

  - `componentWillUpdate(nextProps, nextState)` 进入重新渲染流程, 会再次执行render函数

  - `componentDidUpdate(prevProps, prevState)` 组件渲染完毕, 参数中可以得到组件渲染之前的数据

- [组件销毁](javascript:;)

  - `componentWillUnmount()` 组件卸载

- [组件异常](javascript:;)

  - `componentDisCatch(error, info)` 在之前如果组件出错则会阻止整个应用的渲染, 所以在react@16中新增错误处理机制

<br>

### 生命周期使用场景
---

在react中, 父组件的render执行后, 子组件的render也会重新渲染, 但是数据没有发生变化的话, 有些损耗性能

我们可以借助`shouldComponentUpdate`这个生命周期, 来优化组件是否更新

```js
shouldComponentUpdate (nextProps, nextState) {
  // 只有当数据发生变化时, 组件才重新进行渲染
  return nextProps !== this.props
}
```

<br>

## React-Router 路由相关
---

- [页面Router](javascript:;)

  - 是最传统的一种路由跳转方式, 无论是前进还是后退都会重新加载页面

- [Hash Router](javascript:;)
  - 只有在页面的hash值发生改变时触发, 单页面应用的比较广泛
  - 通过监听`window.onhashchange`这个事件来控制页面的渲染

- [H5 Router](javascript:;)
  - js的history对象里提供了一种方法, 用来手动的在路由里存进一个新值, 点击浏览器后退按钮的时候, 还可以监听浏览器后退按钮所触发的事件
  - history中提供了一个方法`history.pushState('test', null, '/user/list')`, 其中第一个参数名称可以随便起, 第二个参数是个title字段, 可以为null, 第三个参数就是要跳转的地址
  - `window.onpopstate`, 监听浏览器后退按钮触发的事件
  - `history.replaceState()`与之前的方法参数一样, 都是三个, 该方法不会产生历史记录

<br>

### 路由组件
---

- 分为两种路由方式`<HashRouter>` `<BrowserRouter>`

  - 其中前者就是由hash路由来实现的, 后者则是使用了H5 Router来实现

- `<Route>` 用来定义路由规则

  - `exact`可以让路由进行严格匹配
  - `path`定义匹配的路由
  - `component`定义渲染哪个组件
  - `render`定义渲染哪些元素

- `<Link>`路由的跳转标签

  - `to`代表即将要跳转的路由地址

- `<NavLink>`是在`<Link>`的基础上增加了一些选中状态的处理, 比较适合做导航菜单

  - 
  - 

- `<Switch>` 解决路由多次匹配的问题

  - 如果在`<Router>`里面写了好几个`<Route>`, 那么这几个路由会一一匹配, 使用`<Switch>`包裹的话, 匹配到第一个就会停止
  - 还有一个用处就是搭配`<Route>`跳转404页面

```jsx
<HashRouter>
  <div>
    <Route path="/home" component={Home} />
    <Route path="/center" component={Center} />
    {/* 如果前面的都没有匹配到, 则会跳转到404组件 */}
    <Route component={Error404} />
  </div>
</HashRouter>
```

- `<Redirect>` 用来做自动跳转, 作用是当匹配到某些路径的时候, 自动跳转到该路由

<br>

### 嵌套路由
---

```jsx
<HashRouter>
  <div>
    <Route path="/home" component={Home} />
    <Route path="/center" component={Center} />
  </div>
</HashRouter>
```

```jsx
const Center = () => (
  <div>
    <h1>这是个人中心页面</h1>
    {/* 子路由的path必须加上父路由的path开头, 这样才能保证子路由匹配到时, 父路由也能匹配到 */}
    <Route path="/center/config" component={Config} />
    <Route path="/center/setting" component={Setting} />
  </div>
)
```

<br>

### 动态路由
---

```jsx
import UserDetails from '../components/User/UserDetails'

{/* ... */}

{/* 需要注意component属性不能接受一个字符串, 需要接受该组件的Function */}
<Route path="/user/:Id" component={UserDetails} />
```

!> 获取动态路由参数`props.match.params`

<br>

### 路由的统一配置和渲染
---

> 单层路由情况下

```jsx
const routes = [
  { path: '/home', component: Home },
  { path: '/user', component: User },
  { path: '/center', component: Center }
]

const Page = () => (
  <Router>
    <div>
      {
        {/* routes.map((route, key) => {
          return <Router key={key} path={route.path} component={route.component} />
        }) */}
        routes.map((route, key) => {
          return <Router key={key} {...route} />
        })
      }
    </div>
  </Router>
)
```

> 嵌套路由下

子路由的渲染需要到相对应的组件下去渲染, 而不是在当前位置, 所以需要把子路由当成参数传递过去

```jsx
const routes = [
  { path: '/home', component: Home },
  { path: '/user', component: User },
  { path: '/center', component: Center, routes: [
    { path: '/center/list', component: List },
    { path: '/center/setting', component: Setting }
  ]}
]
const Page = () => (
  <Router>
    <div>
      {
        routes.map((item, key) => (
          <Route
            path={item.path}
            render={(props) => {
              /* render的作用跟component属性一样, render需要返回的是一个组件的标签 */
              return <item.component {...props} routes={item.routes} />
            }}
          />
        ))
      }
    </div>
  </Router>
)
```

接下来在子组件中就可以通过`this.props.routes`获取到传递过来的数据, 从而可以渲染路由

<br>

### 封装路由
---

```jsx
import React from "react"
import { Route } from 'react-router-dom'

export default function routeIfy(routes) {
  if (!routes) return
  return routes.map((item, key) => {
    return <Route
      key={key}
      path={item.path}
      exact={!!item.exact}
      render={
        props => <item.component {...props} routes={item.routes} />
      }
    />
  })
}
```

<br>
<br>
<br>

## 使用ref来操作DOM元素
---

在`react`中我们使用ref来操作DOM元素

```js
class App extends React.Component {
  render () {
    return (
      <div>
        <input type="text" ref={(input) => this.input = input} />
      </div>
    )
  }
}
```

<br>