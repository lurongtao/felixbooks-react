## PureComponent

`PureComponnet`里如果接收到的新属性或者是更改后的状态和原属性、原状态相同的话，就不会去重新render了
在里面也可以使用`shouldComponentUpdate`，而且。是否重新渲染以`shouldComponentUpdate`的返回值为最终的决定因素。

```jsx
import React, { PureComponent } from 'react'

class YourComponent extends PureComponent {
  ……
}
```

## ref

React提供的这个`ref`属性，表示为对组件真正实例的引用，其实就是`ReactDOM.render()`返回的组件实例,`ref`可以挂载到组件上也可以是dom元素上。

- 挂到组件(`class`声明的组件)上的ref表示对组件实例的引用。**不能**在函数式组件上使用 ref 属性，因为它们没有实例：
- 挂载到dom元素上时表示具体的dom元素节点。

在React 最新的版本中，要使用`ref`, 需要使用`React.createRef`方法先生成一个`ref`。

```jsx
import React, { Component, createRef } from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  constructor() {
    super()
    // 创建inputRef
    this.inputRef=createRef()
  }
  componentDidMount () {
    console.log(this.inputRef.current) // <input type="text">
  }
  render () {
    return (
  		<div>
        {/* 关联ref和dom */}
        <input type="text" ref={this.inputRef} />
      </div>
  	)
  }
}
ReactDOM.render(
	<App/>,
  document.getElementById('root')
)
```