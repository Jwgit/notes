##### React-Redux

React-Redux 将组件分为两类：UI组件，容器组件

UI组件：	

> 只负责UI的呈现，不带任何业务逻辑
>
> 没有状态，不使用this.state
>
> 所有数据都由参数（this.props） 提供
>
> 不使用任何Redux的API

容器组件

> 负责管理数据和业务逻辑，不负责UI的呈现
>
> 带有内部状态
>
> 使用Redux的ApI

connect

> React-Redux 提供connect() 方法，用于从UI组件生成容器组件。
>
> connect 方法接受两个参数，mapStateToProps 和mapDispatchToProps。
>
> **mapStateToProps**负责输入逻辑，将state 映射到UI组件的参数（props）上。接受第一个参数state，还可以接受第二个参数ownProps，返回一个对象。
>
> **mapDispatchToProps**负责输出逻辑，将UI组件的操作映射成Action。可以是函数也可以是一个对象。如果`mapDispatchToProps`是一个函数，会得到`dispatch`和`ownProps`（容器组件的`props`对象）两个参数。

Provider

> `connect`方法生成容器组件以后，需要让容器组件拿到`state`对象，才能生成 UI 组件的参数。
>
> React-Redux 提供`Provider`组件，可以让容器组件拿到`state`。