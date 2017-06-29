#####Promise


##### 语法

```
new Promise(/* executor */ ,function(resolve, reject){...});
```

##### 参数

> `executor`:
>
> Promise构造器的参数，Function类型，该方法有两个参数：resolve 和 reject， 这两个参数均为方法类型。
>
> executor方法在调用Promise构造器时立即被调用（甚至在构造器方法返回新创建的Promise对象之前执行）。
>
> 在executor内部，如果resolve被调用，代表该Promise被成功解析（resolve），而当reject被调用时，代表该Promise的值不能用于后续的处理了，也就是被拒绝（reject）了。
>
> executor主要用于初始化异步代码，一旦一步代码调用完成，要么调用resolve方法来表示Promise被成功解析，或者调用reject方法，表示初始化的异步代码调用失败，整个Promise被拒绝了。
>
> 如果在executor方法执行过程中抛出异常，那么Promise立即被拒绝，返回值也被忽略。

##### 状态

Promise有一下几种状态：

1. `pending`：初始状态，既不是fulfilled,也不是rejected
2. `fulfilled`: 表示异步代码成功执行（没有错误抛出），且返回返回值已填充（filled）
3. `rejected`: 表示executor执行失败，Promise被拒绝

pending状态的Promise对象可能被填充了（fulfilled）值，也可能被某种理由（异常信息）拒绝（reject）了。当其中任一种情况出现时，Promise对象的**then方法**绑定的**处理方法**（handlers ）就会被调用(then方法包含两个参数：onfulfilled和onrejected，它们都是Function类型。当值被填充时，调用then的onfulfilled方法，当Promise被拒绝时，调用then的onrejected方法， 所以在异步操作的完成和绑定处理方法之间不存在竞争)

因为[`Promise.prototype.then`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)和 `Promise.prototype.catch`方法返回 promises对象自身， 所以它们可以被链式调用

![状态流转图](https://mdn.mozillademos.org/files/8633/promises.png)

##### 方法

> 1. `Promise.all(iterable)`:这个方法返回一个新的promise对象，该promise对象在iterable里**所有的promise对象都成功**的时候才会触发成功，一旦有**任何一个iterable里面的promise对象失败**则立即触发该promise对象的失败。这个新的promise对象在触发成功状态以后，会把一个包含iterable里**所有**promise返回值的数组作为成功回调的返回值，顺序跟iterable的顺序保持一致；如果这个新的promise对象触发了失败状态，它会把iterable里**第一个**触发失败的promise对象的错误信息作为它的失败错误信息。Promise.all方法常被用于处理多个promise对象的状态集合。（可以参考jQuery.when方法---译者注）
> 2. `Promise.race(iterable)`:当iterable参数里的**任意一个**子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象。
> 3. `Promise.reject(reason)`:调用Promise的rejected句柄，并且返回这个Promise对象。
> 4. `Promise.resolve(value)`:用成功值value完成一个Promise对象。如果该value为可继续的（thenable，即带有then方法），返回的Promise对象会“跟随”这个value，采用这个value的最终状态；否则的话返回值会用这个value满足（fullfil）返回的Promise对象。

##### Promise原型方法

> 1. `Promise.prototype.catch(onRejected)`:添加一个否定(rejection) 回调到当前 promise, 返回一个新的promise。如果这个回调被调用，新 promise 将以它的返回值来resolve，否则如果当前promise 进入fulfilled状态，则以当前promise的肯定结果作为新promise的肯定结果.
> 2. `Promise.prototype.then(onFullfilled,onRejected)`: 添加肯定和否定回调到当前promise，返回新的promise，将回调的返回值来resolve。

##### 注意事项

> 1. 当你使用 `then(resolveHandler, rejectHandler)` 这种形式时，`rejectHandler` *并不会捕获由 resolveHandler 引发的异常*。
>
>    鉴于此，我个人的习惯是不适用 `then()` 的第二个参数，而是总是使用 `catch()`
>
> 2. `Promise.all()`执行一系列的Promise时，依照 promises 规范，一旦一个 promise 被创建，它就被执行了。因此你实际上需要的是一个 `promise factories` 数组。promises factory 是一个可以返回 promise 的函数。

```javascript
var dos = function(){console.log("1");return Promise.resolve("11")};
var dosm = function() {console.log("2");return Promise.resolve("22")};
dos().then(dosm).then(function(re){console.log(re)});
// 1
// 2
// 22
var dos = function(){console.log("1");return Promise.resolve("11")};
var dosm = function() {console.log("2");return Promise.resolve("22")};
dos().then(dosm()).then(function(re){console.log(re)});
// 1
// 2
// 11
```

