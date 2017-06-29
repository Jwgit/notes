#### JavaScript对象的创建

1. ##### 工厂模式

   > ```javascript
   > function Person() {
   >   var o = new Object();
   >   o.name = 'Jing';
   >   o.say = function() {
   >     console.log(this.name);
   >   }
   >   return o;
   > }
   > var person1 = Person();
   > ```
   >
   > **优点** ：完成返回一个对象的要求
   >
   > **缺点**：
   >
   > 	1. 无法通过constructor识别对象，以为都是来自Object，无法得知来自Person
   > 	2. 每次通过Person创建对象的时候，所有的say方法都是一样的，但是却存储了多次，浪费资源

2. ##### 构造函数模式

   > ```javascript
   > function Person() {
   >   this.name = 'Jing';
   >   this.say = function() {
   >     console.log(this.name);
   >   }
   > }
   > var person1 = new Person();
   > ```
   >
   > **优点**：
   >
   > 1. 通过constructor或者instanceof可以识别对象实例的类别
   > 2. 可以通过new 关键字来创建对象实例，更像OO语言中创建对象实例
   >
   > **缺点**：
   >
   > 1. 多个实例的say方法都是一样的效果，但是却存储了多次（两个实例的say方法是不同的，因为存放的内存地址不一样）
   >
   > *注意*：
   >
   > 1. 构造函数模式隐式的在最后 return this， 在创建对象实例的时候，在非strict模式下，如果缺少了new，那么就会把属性和方法添加到全局对象上，strict模式下会this.name = name 将报错。
   > 2. 也可以根据return this 的特性调用call或者apply来指定this，在继承中有使用

3. ##### 原型模式

   > ```javascript
   > function Person() {};
   > Person.prototype.name = 'Jing';
   > Person.prototype.say = function() {
   >   console.log(this.name);
   > }
   > Person.prototype.friends = ['King'];
   > var person1 = new Person();
   > ```
   >
   > **优点**：
   >
   > 1. say方法是共享的，所有的实例的say方法指向同一个
   > 2. 可以动态的添加原型对象的方法和属性，并且直接反映在多有的对象实例上
   >
   > **缺点**：
   >
   > 1. 引用类型的变量，共享存储区域，所有的实例都共用同一个引用类型变量
   > 2. 第一次调用say方法或者name属性的时候会搜索两次，现在实例对象上找，没有就去原型对象（Person.prototype） 上找，*找到后再在实例上添加这些方法或属性*(????)
   > 3. 所有的方法都是共享的，没有办法创建实例自己的属性和方法，也没有办法像构造函数那样传递参数
   >
   > *注意*
   >
   > 1. 优点②中存在一个问题就是直接通过对象字面量给Person.prototype进行赋值的时候会导致constructor改变，所以需要手动设置，其次就是通过对象字面量给Person.prototype进行赋值，会无法作用在之前创建的对象实例上
   >
   >    ```javascript
   >    var person1 = new Person();
   >    Person.prototype = {
   >    	name: "King",
   >    	setName: function(name){
   >          this.name = name;
   >    	}
   >    }
   >    person1.setName(); // Uncaught TypeError: person1.setName is not a function(…)
   >
   >    Person.prototype.setName2 = function(name) {
   >      this.name = name;
   >    }
   >    person1.setName2('King');
   >    per1.say();  //King
   >    ```
   >
   >    这是因为对象实例和对象原型直接是通过一个指针链接的，这个指针是一个内部的属性`[[Prototype]]`，可以通过`__proto__`访问。我们通过对象字面修改了Person.prototype指向的地址，然而对象实例的`__proto__`并没有跟着一起更新，所以导，实例还是访问原来的Person.prototype，所以建议不要通过这种方法来改变Person.prototype对象的属性或方法。

4. ##### 构造函数和原型组合模式

   > ```javascript
   > function Person(name) {
   >   this.name = name;
   >   this.friends = ['Ling'];
   > }
   > Person.prototype.say = function() {
   >   console.log(this.name);
   > }
   > var person1 = new Person('Jing');
   > person1.say();  //Jing
   > ```
   >
   > **优点**: 
   >
   > 1. 解决了原型模式对于引用类型的确定
   > 2. 解决了原型模式没有办法传递参数的缺点
   > 3. 解决了构造函数模式不能共享方法的缺点

5. ##### 动态原型模式

   > ```javascript
   > function Person(name) {
   >   this.name = name;
   >   if(typeof this.say != 'function') {
   >     Person.prototype.say = function() {
   >       console.log(this.name);
   >     }
   >   }
   > }
   > ```
   >
   > **优点**：
   >
   > 1. 可以在初次调用构造函数的时候就完成原型对象的修改
   > 2. 修改能体现在所有的实例中
   >
   > *注意*
   >
   > 1. 只用检查一个在执行后应该存在的方法或者属性就行了
   > 2. 不能用对象字面量修改原型对象

6. ##### 寄生构造函数模式

   > ```
   > function Person(name) {
   >   var o = new Object();
   >   o.name = name;
   >   o.say = function() {
   >     console.log(this.name);
   >   }
   >   return o;
   > }
   > var person1 = new Person('Jing');
   > ```
   >
   > *注意*
   >
   > 1. 和工厂模式的区别，调用时使用new
   > 2. 为了不污染原生对象

7. ##### 稳妥构造模式

   > ```javascript
   > function Person(name) {
   >   var o = new Object();
   >   o.say = function() {
   >     console.log(name);
   >   }
   > }
   > var person1 = new Person('Jing');
   > person1.name; // undefined
   > person.say(); // Jing
   > ```
   >
   > **优点**：
   >
   > 1. 安全，name成为私有变量，只能通过say方法访问
   >
   > **缺点**：
   >
   > 1. 不能区分实例类型

   ​