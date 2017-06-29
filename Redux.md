##### Redux

1. Redux的设计思想： 

   > 1. Web 应用是一个状态机，视图与状态是一一对应的。
   > 2. 所有状态都保存在一个对象里面

2. 基本概念和API

   1. Store

      Store 是保存数据的容器，整个应用只能有一个Store。

      Redux提供createStore方法，来生成Store,该方法接受一个函数作为参数，还可接受第二个参数表示出事状态，返回Store对象。

   2. State

      State是Store的数据快照，是在某个时间点的Store中的数据集合，当前时刻的State 通过 store.getState()拿到。

      3. Action	

   ​         Action是View发出的通知，告知State应该要变化了.

   ​	Action是一个对象，**type**属性是必须的，表示Action的名称。可以携带信息传递给Store.

   ​	ActionCreator 就是创建Action 的函数。

   4. store.dispatch()

      store.dispatch() 是View发出Action的唯一方法。

   5. store.subscribe()

      Store.subscribe() 方法监听State的变化，一旦State变化，就自动执行。

3. Reducer

   Store 接受Action后，计算给出一个新的State,来更新View，这个计算过程就叫Reducer.

   Reducer 是一个函数，接受Action和当前的State作为参数，返回一个新的State.

   Srore.dispatch()方法触发Reducer的自动执行，为此需要将Reducer 传给createStore方法。这样生成的store，每当store.dispatch() 发送一个新的额Action 就会自动调用Reducer 得到新的State.

    Reducer 是一个纯函数：	

   ​	(1)不能改写参数

   ​	(2).不能调用系统IO的API

   ​	(3).不能调用Date.now()或者Mathc.random()等不纯的方法。


4. combineReducers

​        Redux 提供了一个`combineReducers`方法，用于 Reducer 的拆分。你只要定义各个子 Reducer 函数，然后用这个方法，将它们合成一个大的 Reducer。

5. 中间件

   中间件是一个函数，对store.dispatch方法进行改造，在发出Action和执行Reducer 两部之间，添加其他功能。

   createStore方法可以接受 applyMiddleware(…) 参数，applyMiddleware()  传入要使用的中间件名，有的中间件有次序要求，使用前要查一下文档，否则输出结果会不正确。

6. redux-thunk 中间件

   异步操作，在操作结束时候，需要系统自动发送出第二个Action。Action 是由`store.dispatch`方法发送的。而`store.dispatch`方法正常情况下，参数只能是对象，不能是函数。`redux-thunk`中间件，改造`store.dispatch`，使得后者可以接受函数作为参数。

   ```
   export function asyncActionCreator(data) {
     return (dispatch, getState){
   		// getState can get now state 
   		axios.get(url).then((res) => {
             dispatch(res);  // do something after network  ,then dispatch action
   		})
   	}
   }
   ```

   ​
