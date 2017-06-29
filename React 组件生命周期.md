##### React 组件生命周期

1. 挂载期

   ​	组件挂载主要做组件状态的初始化，读取state和props以及组件生命周期函数componentWillMount和componentDidMount。

   ​	componentWillMount 只渲染一次，此时即使在组件中设置setState也只会渲染一次，所以基本初始化的stated都可以放在this.state的。

   ​	componentDidMount 表示组件已经挂载到真实DOM。

2. 存在期

   ​	组件存在期间，父组件传递props或者自身执行setState，或者执行forceUpdate时，发生一系列的更新动作。

   1. props变化时，触发componentWillReceiveProps方法，参数为新的props。

   ​	接下来执行shouldComponentUpdate, 参数为需要更新的props和state，开发者根据必要判断，是否需要更新。当方法返回false，组件不在向下执行生命周期方法,默认返回true.

   ​	 接下来调用componentWillUpdate，参数为需要更新的state和props.

   ​	 然后调用render 更新组件，

   ​	componentDidUpdate在更新完毕后调用，参数为更新前的props和state。

   2. state变化时，与props变化相比，没有调用componentWillReceiveProps 方法，直接调用shouldComponetUpdate之后的流程。
   3.  forceUpdate执行后直接进入componentWillUpdate 流程

3. 卸载期

    组件卸载方法componentWillUnmount,主要用于清理方法，时间回收清除定时器等作用。

在componentWillMount，componentDidMount，componentWillReceiveProps，componentDidUpdate生命周期方法中可以调用this.setState。



this.setState() 是一个异步操作的过程，并不保证state立即更新。可以接受一个对象Object,也可以接受一个函数，为确保获取到更新后的state，可以接受一个回调函数，该回调在state更新后调用，确保state是更新后的值。

React 可能会出于性能考虑将多个 setState() 调用合并成一个批处理更新操作。

https://www.oschina.net/translate/functional-setstate-is-the-future-of-react

![ component-lifecycle](/Users/jing/notes/component-lifecycle.jpg)

