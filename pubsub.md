
## 兄弟组件之间进行通讯
---

- `npm i pubsub-js`

> pubsub.js为我们提供了很好的解决方式

通过事件的订阅和发布就可以实现我们想要的功能

<br>

> 演示

```jsx
import PubSub from 'pubsub-js'

// 发布消息
PubSub.publish('消息名称', '数据')

// 订阅消息
PubSub.subscribe('消息名称', (msg, data) => {
  console.log(msg, data)
})
```

<br>

> 案例

```jsx
import React from 'react'
// 引入pubsub.js用于兄弟组件之间的传值
import PubSub from 'pubsub-js'

// Header组件负责数据的发布
class Header extends React.Component {
  render () {
    return (
      <div>
        <button onClick={() => {
          PubSub.publish('addNumber', Math.ceil(Math.random() * 100))
        }}>
        添加
        </button>
      </div>
    )
  }
}

// Content组件负责数据的展示和渲染
class Content extends React.Component {
  state = {
    todo: [1, 2, 3]
  }
  componentDidMount () {
    PubSub.subscribe('addNumber', (msg, data) => {
      this.state.todo.push(data)
      this.setState({
        todo: this.state.todo
      })
    })
  }
  render () {
    return (
      <div>
        {
          this.state.todo.map((item, index) => {
            return <li key={index}>{item}</li>
          })
        }
      </div>
    )
  }
}

// 在父组件中进行调用
class App extends React.Component {
  render () {
    return (
      <div>
        <Header />
        <Content />
      </div>
    )
  }
}

export default App
```

### NavLink
---

- https://reacttraining.com/react-router/web/api/NavLink

- `<NavLink />`

    - `activeClassName` *{ String }* 指定当前active类名
    - `activeStyle` *{ Object }* 指定当前active类样式
    - `exact` *{ Boolean }* 当前路由是否严格匹配
    - `strict` *{ Boolean }* When true, the trailing slash on a location’s pathname will be taken into consideration when determining if the location matches the current URL. See the <Route strict> documentation for more information.
    - `isActive` *{ Function }* A function to add extra logic for determining whether the link is active. This should be used if you want to do more than verify that the link’s pathname matches the current URL’s pathname.
    - `location` *{ Object }* The isActive compares the current history location (usually the current browser URL). To compare to a different location, a location can be passed.
    - `ariaCurrent` *{ String }* The value of the aria-current attribute used on an active link. Available values are:

        - "page" - used to indicate a link within a set of pagination links
        - "step" - used to indicate a link within a step indicator for a step-based process
        - "location" - used to indicate the image that is visually highlighted as the current component of a flow chart
        - "date" - used to indicate the current date within a calendar
        - "time" - used to indicate the current time within a timetable
        - "true" - used to indicate if the NavLink is active


### 路由的跳转方式
---

> 通过`history.push`跳转

- `push`跳转的会保留历史记录

```jsx
{/* 跳转登录页面 */}
this.props.history.push('/login')
```

<br>

> 通过`history.replace`跳转

- `replace`跳转的不会保留历史记录

```jsx
{/* 跳转登录页面 */}
this.props.history.replace('/login')
```

<br>

> 通过`history.goBack`回退

```jsx
this.props.history.goBack()
```

<br>

> 通过`history.goForward`前进

```jsx
this.props.history.goForward()
```

<br>