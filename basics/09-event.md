# 事件处理

## 绑定事件

采用on+事件名的方式来绑定一个事件，注意，这里和原生的事件是有区别的，原生的事件全是小写`onclick`, React里的事件是驼峰`onClick`，**React的事件并不是原生事件，而是合成事件**。

## 事件handler的写法

- 直接在render里写行内的箭头函数(不推荐)
- 在组件内使用箭头函数定义一个方法(推荐)
- 直接在组件内定义一个非箭头函数的方法，然后在render里直接使用`onClick={this.handleClick.bind(this)}`(不推荐)
- 直接在组件内定义一个非箭头函数的方法，然后在constructor里bind(this)(推荐)

## Event 对象

和普通浏览器一样，事件handler会被自动传入一个 `event` 对象，这个对象和普通的浏览器 `event` 对象所包含的方法和属性都基本一致。不同的是 React中的 `event` 对象并不是浏览器提供的，而是它自己内部所构建的。它同样具有`event.stopPropagation`、`event.preventDefault` 这种常用的方法

## 事件的参数传递

- 在`render`里调用方法的地方外面包一层箭头函数 
- 在`render`里通过`this.handleEvent.bind(this, 参数)`这样的方式来传递
- 通过`event`传递
- 比较推荐的是做一个子组件, 在父组件中定义方法，通过`props`传递到子组件中，然后在子组件件通过`this.props.method`来调用

## 处理用户输入

```jsx
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  constructor() {
    super()
    this.state = {
      xing: '',
      ming: ''
    }
  }
  handleInputChange = (e) => {
    this.setState({
      [e.target.name]: e.target.value
    })
  }
  render () {
    const {
      xing,
      ming
    } = this.state
    return (
  		<div>
        <label>
          <span>姓:</span>
          <input
            type="text"
            name="xing"
            value={xing}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          <span>名:</span>
          <input
            type="text"
            name="ming"
            value={ming}
            onChange={this.handleInputChange}
          />
        </label>
        <p>欢迎您: {xing}{ming}</p>
      </div>
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```