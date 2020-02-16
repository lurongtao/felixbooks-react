# HOC(高阶组件)

Higher-Order Components就是一个函数，传给它一个组件，它返回一个新的组件。

```jsx
const NewComponent = higherOrderComponent(YourComponent)
```

比如，我们想要我们的组件通过自动注入一个版权信息。

```jsx
// withCopyright.js 定义一个高阶组件
import React, { Component, Fragment } from 'react'

const withCopyright = (WrappedComponent) => {
  return class NewComponent extends Component {
    render() {
      return (
        <Fragment>
          <WrappedComponent />
          <div>&copy;版权所有 千锋教育 2019 </div>
        </Fragment>
      )
    }
  }
}
export default withCopyright
```

```jsx
// 使用方式
import withCopyright from './withCopyright'

class App extends Component {
  render () {
    return (
  		<div>
        <h1>Awesome React</h1>
        <p>React.js是一个构建用户界面的库</p>
      </div>
  	)
  }
}
const CopyrightApp = withCopyright(App)
```

这样只要我们有需要用到版权信息的组件，都可以直接使用withCopyright这个高阶组件包裹即可。

在这里要讲解在CRA 中配置装饰器模式的支持。