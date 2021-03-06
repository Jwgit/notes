#### 一、事件

##### 1. 事件流

> 事件流描述的是从页面中接受事件的顺序。“DOM2级事件”规定事件流包含三个阶段：事件捕获阶段，处于目标阶段和事件冒泡阶段。首先发生的是事件捕获，然后是目标节点接收到事件，最后是冒泡阶段。

##### 2. 事件冒泡

> IE的事件流叫做事件冒泡，即事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点。
>
> ![事件流转图](https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg)
>
> 所有的现代浏览器都支持事件冒泡。IE5.5及更早的浏览器冒泡会跳过`<html>`元素。IE9，Firefox，Chrome，Safari则将时间一直冒泡到window对象

##### 3. 事件捕获

> 事件捕获的思想是不太具体的节点应该更早的接收到事件，而具体的节点最后接收到事件。事件捕获的用意是在事件到达预定目标之前捕获它



#### 二、事件处理程序

##### 1. DOM0级事件处理程序

> 将一个函数赋值给一个事件处理程序的属性，该函数被认为是该元素的方法。
>
> ```javascript
> var btn = document.getElementById('myBtn');
> btn.onclick = function(){
>   console.log(this.id);
> }
>
> //程序中得this 指向是元素本身
>
> //移除事件处理
> btn.onclick = null;
> ```

##### 2. DOM2级事件处理程序

> 1. 指定事件处理程序：`addEventListener()`,所有的DOM节点都有该方法，接收三个参数：要处理的事件名，作为事件处理程序的函数，一个布尔值。最后这个布尔值参数如果为`true`,表示在捕获阶段调用事件处理函数，为`false` 在冒泡阶段调用事件处理函数。同一个节点可以指定多个事件处理程序，按照事件处理函数的**顺序执行**。
>
>    ```javascript
>    var btn = document.getElementById('myBtn');
>    btn.addEventListener('click',function(){
>      console.log(this.id);
>    },false)
>
>    //事件名称为click 非onclick
>    ```
>
> 2. 删除事件处理程序：`removeEventListener()`,所有的DOM节点都有该方法。同样接收三个参数：要删除的事件名，事件的处理函数名，一个布尔值。*匿名函数的事件处理程序将无法移除*
>
>    ```javascript
>    var btn = document.getElementById('myBtn');
>    var handler = function(){
>      console.log(this.id);
>    }
>    btn.addEventListener('click',handler,false);
>    btn.removeEventListener('click',handler,false)
>    ```

##### 3. IE事件处理程序

> 1. 指定事件处理程序：`attachEvent()`, 方法接收两个参数：事件处理程序名称，事件处理程序函数。IE8 下只支持冒泡，处理程序被添加到冒泡阶段。可为同一节点指定多个处理函数，多个事件处理程序不是以顺序执行，而是以**相反的顺序被执行**。
>
>    ```javascript
>    var btn document.getElementById('myBtn');
>    btn.attachEvent('onclick',function(){
>      console.log(this); // 这里的this 指向全局作用域 window
>    })
>
>    //事件程序名称是onclick ,非click
>    ```
>
> 2. 删除事件处理程序：`detachEvent()`,方法接收两个参数：事件处理程序名称，事件处理程序函数。*同样的匿名函数的事件处理程序将无法移除*
>
>    ```javascript
>    var btn document.getElementById('myBtn');
>    var handler = function(){
>      console.log("Jing"); 
>    })
>    btn.attachEvent('onclick',handler);
>    btn.detachEvent('onclick',handler);
>
>    //事件程序名称是onclick ,非click
>    ```

##### 4. 跨浏览器的事件处理程序

> ```javascript
> var EventUtil = {
>   addHandler: function(element, type, handler) {
>     if(element.addEventListener){
>       element.addEventListener(type, handler,false); // false: 冒泡
>     }else if(element.attachEvent){
>       element.attachEvent('on'+type, handler);
>     }else{
>       element['on' + type] = handler;
>     }
>   },
>   removeHandler: function(element, type, handler) {
>     if(element.removeEventListener){
>       element.removeEventListener(type, handler,false); // false: 冒泡
>     }else if(element.detachEvent){
>       element.detachEvent('on'+type, handler);
>     }else{
>       element['on' + type] = null;
>     }
>   }
> }
> ```
>
> 
