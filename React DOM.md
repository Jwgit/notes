#### React DOM术语

##### 1. React Element

> React里的首要类型就是 `ReactElement`.它有4个属性：`type`,`props`,`key`,`ref`.没有方法，在prototype上什么也没有。
>
> 创建方法：
>
> ```javascript
> var reactElement = React.createElement('div');
> ```
>
> `ReactElement`是一个轻的，有状态的不可变的虚拟DOM Element。
>
> 渲染到DOM上
>
> ```javascript
> ReactDOM.render(reactElement, document.getElementById('example'));
> ```

##### 2. Factory

> `ReactElement Factory`产生一个特定type属性的`ReactElement`函数。
>
> ```javascript
> var div = React.createFactory('div');
> var root = div({ className: 'my-div' });
> ReactDOM.render(root, document.getElementById('example'));
> ```

##### 3. React Nodes

> 一个`ReactNode`可以是：
>
> - `ReactElement`
> - `string`(又名`ReactText`)
> - `number`(又名`ReactText`)
> - `Array of ReactNodes`(又名`ReactFragment`)
>
> `ReactNodes`被当做`ReactElement`的属性来表示子级，创建一个`ReactElements  `树。

##### 4.React Components

> 一个`ReactComponent`类就是一个JavaScript类
>
> ```javascript
> var MyComponent = React.createClass({
>   render: function() {
>     ...
>   }
> });
> ```
>
> 当这个构造函数被调用,期望返回一个至少有一个 `render` 方法的对象.这个对象被称为一个 `ReactComponent`.
>
> `ReactComponent` 的 `render` 方法被期望返回另一个 `ReactElement`.