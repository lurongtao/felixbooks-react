# 组件的数据挂载方式

## 属性(props)

`props`是正常是外部传入的，组件内部也可以通过一些方式来初始化的设置，属性不能被组件自己更改，但是你可以通过父组件主动重新渲染的方式来传入新的 `props`

属性是描述性质、特点的，组件自己不能随意更改。

之前的组件代码里面有`props`的简单使用，总的来说，在使用一个组件的时候，可以把参数放在标签的属性当中，所有的属性都会作为组件 `props` 对象的键值。通过箭头函数创建的组件，需要通过函数的参数来接收`props`:

```jsx
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  render () {
    return (
  		<h1>欢迎进入{this.props.name}的世界</h1>
  	)
  }
}

const Content = (props) => {
  return (
    <p>{props.name}是一个构建UI的库</p>
  )
}

class App extends Component {
  render () {
    return (
  		<Fragment>
      	<Title name="React" />
        <Content name="React.js" />
      </Fragment>
  	)
  }
}

ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```

### 设置组件的默认props

```jsx
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  // 使用类创建的组件，直接在这里写static方法，创建defaultProps
  static defaultProps = {
    name: 'React'
  }
  render () {
    return (
  		<h1>欢迎进入{this.props.name}的世界</h1>
  	)
  }
}

const Content = (props) => {
  return (
    <p>{props.name}是一个构建UI的库</p>
  )
}

// 使用箭头函数创建的组件，需要在这个组件上直接写defaultProps属性
Content.defaultProps = {
  name: 'React.js'
}

class App extends Component {
  render () {
    return (
  		<Fragment>
        {/* 由于设置了defaultProps， 不传props也能正常运行，如果传递了就会覆盖defaultProps的值 */}
      	<Title />
        <Content />
      </Fragment>
  	)
  }
}

ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```

### props.children

我们知道使用组件的时候，可以嵌套。要在自定义组件的使用嵌套结构，就需要使用 `props.children` 。在实际的工作当中，我们几乎每天都需要用这种方式来编写组件。

```jsx
import React, { Component, Fragment } from 'react'
import ReactDOM from 'react-dom'

class Title extends Component {
  render () {
    return (
  		<h1>欢迎进入{this.props.children}的世界</h1>
  	)
  }
}

const Content = (props) => {
  return (
    <p>{props.children}</p>
  )
}

class App extends Component {
  render () {
    return (
  		<Fragment>
      	<Title>React</Title>
        <Content><i>React.js</i>是一个构建UI的库</Content>
      </Fragment>
  	)
  }
}

ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```

### 使用prop-types检查props

React其实是为了构建大型应用程序而生, 在一个大型应用中，根本不知道别人使用你写的组件的时候会传入什么样的参数，有可能会造成应用程序运行不了，但是不报错。为了解决这个问题，React提供了一种机制，让写组件的人可以给组件的```props```设定参数检查，需要安装和使用[prop-types](<https://www.npmjs.com/package/prop-types>):

```sh
$ npm i prop-types -S
```

## 状态(state)

状态就是组件描述某种显示情况的数据，由组件自己设置和更改，也就是说由组件自己维护，使用状态的目的就是为了在不同的状态下使组件的显示不同(自己管理)

### 定义state

第一种方式

```jsx
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  state = {
    name: 'React',
    isLiked: false
  }
  render () {
    return (
      <div>
        <h1>欢迎来到{this.state.name}的世界</h1>
        <button>
          {
            this.state.isLiked ? '❤️取消' : '🖤收藏'
          }
        </button>
      </div>
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```

另一种方式(推荐)

```jsx
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  constructor() {
    super()
    this.state = {
      name: 'React',
      isLiked: false
    }
  }
  render () {
    return (
  		<div>
        <h1>欢迎来到{this.state.name}的世界</h1>
        <button>
          {
            this.state.isLiked ? '❤️取消' : '🖤收藏'
          }
        </button>
      </div>
  	)
  }
}
ReactDOM.render(
  <App/>,
  document.getElementById('root')
)
```

`this.props`和`this.state`是纯js对象,在vue中，data属性是利用`Object.defineProperty`处理过的，更改​data的数据的时候会触发数据的`getter`和`setter`，但是React中没有做这样的处理，如果直接更改的话，react是无法得知的，所以，需要使用特殊的更改状态的方法`setState`。

### setState

`isLiked` 存放在实例的 `state` 对象当中，组件的 `render` 函数内，会根据组件的 `state` 的中的`isLiked`不同显示“取消”或“收藏”内容。下面给 `button` 加上了点击的事件监听。

```jsx
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  constructor() {
    super()
    this.state = {
      name: 'React',
      isLiked: false
    }
  }
  handleBtnClick = () => {
    this.setState({
      isLiked: !this.state.isLiked
    })
  }
  render () {
    return (
      <div>
        <h1>欢迎来到{this.state.name}的世界</h1>
        <button onClick={this.handleBtnClick}>
          {
            this.state.isLiked ? '❤️取消' : '🖤收藏'
          }
        </button>
      </div>
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```

`setState`有两个参数

第一个参数可以是对象，也可以是方法return一个对象，我们把这个参数叫做`updater`

- 参数是对象

  ```jsx
  this.setState({
    isLiked: !this.state.isLiked
  })
  ```

- 参数是方法

  ```jsx
  this.setState((prevState, props) => {
    return {
      isLiked: !prevState.isLiked
    }
  })
  ```

  注意的是这个方法接收两个参数，第一个是上一次的state, 第二个是props

`setState`是异步的，所以想要获取到最新的state，没有办法获取，就有了第二个参数，这是一个可选的回调函数

```jsx
this.setState((prevState, props) => {
  return {
    isLiked: !prevState.isLiked
  }
}, () => {
  console.log('回调里的',this.state.isLiked)
})
console.log('setState外部的',this.state.isLiked)
```

## 属性vs状态

相似点：都是纯js对象，都会触发render更新，都具有确定性（状态/属性相同，结果相同）

不同点： 

1. 属性能从父组件获取，状态不能
2. 属性可以由父组件修改，状态不能
3. 属性能在内部设置默认值，状态也可以
4. 属性不在组件内部修改，状态要改
5. 属性能设置子组件初始值，状态不可以
6. 属性可以修改子组件的值，状态不可以

`state` 的主要作用是用于组件保存、控制、修改自己的可变状态。`state` 在组件内部初始化，可以被组件自身修改，而外部不能访问也不能修改。你可以认为 `state` 是一个局部的、只能被组件自身控制的数据源。`state` 中状态可以通过 `this.setState`方法进行更新，`setState` 会导致组件的重新渲染。

`props` 的主要作用是让使用该组件的父组件可以传入参数来配置该组件。它是外部传进来的配置参数，组件内部无法控制也无法修改。除非外部组件主动传入新的 `props`，否则组件的 `props` 永远保持不变。

如果搞不清 `state` 和 `props` 的使用场景，记住一个简单的规则：**尽量少地用 `state`，多用 `props`**。

没有 `state` 的组件叫无状态组件（stateless component），设置了 state 的叫做有状态组件（stateful component）。因为状态会带来管理的复杂性，我们尽量多地写无状态组件，尽量少地写有状态的组件。这样会降低代码维护的难度，也会在一定程度上增强组件的可复用性。

## 状态提升

如果有多个组件共享一个数据，把这个数据放到共同的父级组件中来管理

## 受控组件与非受控组件 

React组件的数据渲染是否被调用者传递的`props`完全控制，控制则为受控组件，否则非受控组件。



## 渲染数据

- 条件渲染

  ```jsx
  {
    condition ? '❤️取消' : '🖤收藏'
  }
  ```

- 列表渲染

```jsx
// 数据
const people = [{
  id: 1,
  name: 'Leo',
  age: 35
}, {
  id: 2,
  name: 'XiaoMing',
  age: 16
}]
// 渲染列表
{
  people.map(person => {
    return (
      <dl key={person.id}>
        <dt>{person.name}</dt>
        <dd>age: {person.age}</dd>
      </dl>
    )
  })
}
```

React的高效依赖于所谓的 Virtual-DOM，尽量不碰 DOM。对于列表元素来说会有一个问题：元素可能会在一个列表中改变位置。要实现这个操作，只需要交换一下 DOM 位置就行了，但是React并不知道其实我们只是改变了元素的位置，所以它会重新渲染后面两个元素（再执行 Virtual-DOM ），这样会大大增加 DOM 操作。但如果给每个元素加上唯一的标识，React 就可以知道这两个元素只是交换了位置，这个标识就是```key```，这个 `key` 必须是每个元素唯一的标识

- dangerouslySetHTML

对于富文本创建的内容，后台拿到的数据是这样的：

```js
content = "<p>React.js是一个构建UI的库</p>"
```

处于安全的原因，React当中所有表达式的内容会被转义，如果直接输入，标签会被当成文本。这时候就需要使用`dangerouslySetHTML`属性，它允许我们动态设置`innerHTML`

```jsx
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  constructor() {
    super()
    this.state = {
      content : "<p>React.js是一个构建UI的库</p>"
    }
  }
  render () {
    return (
  		<div
        // 注意这里是两个下下划线 __html
        dangerouslySetInnerHTML={{__html: this.state.content}}
      />
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```