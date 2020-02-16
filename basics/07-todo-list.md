# TodoList

组件化开发React todolist， 项目开发中的组件的基本目录结构基本上是这样的：

> /your-project
>
> - src
>   - …
>   - components
>     - YourComponentOne
>       - index.js/YourComponentOne.js
>     - YourComponentTwo
>       - index.js/YourComponentTwo.js
>     - index.js 用于导出组件

注意：一个组件只干一件事情 ，所以TodoList和TodoItem要做成两个组件，这样也方便于后期理解shouldComponentUpdate