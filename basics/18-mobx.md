# Mobx

Mobx是一个功能强大，上手非常容易的状态管理工具。redux的作者也曾经向大家推荐过它，在不少情况下可以使用Mobx来替代掉redux。

![MobX unidirectional flow](./images/mobx-flow.png)

这张图来自于官网，把这张图理解清楚了。基本上对于mobx的理解就算入门了。

官网有明确的核心概念使用方法，并配有[egghead](<https://egghead.io/courses/manage-complex-state-in-react-apps-with-mobx>)的视频教程。这里就不一一赘述了。

要特别注意当使用 `mobx-react` 时可以定义一个新的生命周期钩子函数 `componentWillReact`。当组件因为它观察的数据发生了改变，它会安排重新渲染，这个时候 `componentWillReact` 会被触发。这使得它很容易追溯渲染并找到导致渲染的操作(action)。

- `componentWillReact` 不接收参数
- `componentWillReact` 初始化渲染前不会触发 (使用 `componentWillMount` 替代)
- `componentWillReact` 对于 mobx-react@4+, 当接收新的 props 时并在 `setState` 调用后会触发此钩子
- 要触发`componentWillReact`必须在render里面用到被观察的变量
- 使用Mobx之后不会触发`componentWillReceiveProps`

> Mobx 详细参见 《千锋大前端手册》Mobx 部分。