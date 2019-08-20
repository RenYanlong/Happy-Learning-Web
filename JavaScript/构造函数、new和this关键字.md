# 构造函数、new和this关键字

有过javascript开发经验的人都应该清楚一件事，js并非是基于类，而是基于构造函数和原型。

构造函数就是一个普通的函数，只是有独有的特性和用法。我们常见的this和new关键字正是构造函数最大的特点。

* 通过构造函数生成对象实例的时候必须使用new关键字；
* 构造函数内部this代表生成实例；

下面就详细的说一下这两个特性：

## new关键字

### new关键字的使用

new命令的作用，就是执行构造函数，返回一个实例对象。构造函数内部的this也会代表对象实例。

```js
function Person(name){
  this.name = name;
}
let Jeff = new Person(Jeff);
```

如果我们不使用new关键字，构造函数就和普通函数无异，也不会生成对象实例。这时候函数内部的this不会代表对象实例，而变为全局变量（window对象），这个后面会讲到。

⚠️如果在严格模式下，像普通函数一样使用构造函数，this并不会代表全局变量，而是变为undefined，再不实用new关键字调用构造函数会报错。

### new关键字内部做了什么

使用new关键字，这种方式调用构造函数会经历以下四个步骤：

* 创建一个新的对象
* 将构造函数的作用域给新对象，因此this指向了这个新对象
* 执行构造函数中的代码，也就是为新对象添加属性
* 返回新对象

## this关键字

对用this关键字，我们应该始终牢记一点，this始终返回的是一个对象，一个代表当前运行环境的对象。

所以说在不同的运行环境下，一个this可能有不同的值。

```js
function fun(){
  console.log(this.a)
}
var a = 1;
var b = {
  a:2,
  c:fun
}

fun();  //1

b.c();  //2
```

这个例子就很好的说明了，相同一个函数，内部的this对象在不同的运行环境下，this对象代表的是不同的对象，在全局作用域下直接调用fun函数，this指向的window对象，window对象的a就是1。而调用b对象的fun方法，则是在b对象的运行环境下，fun函数内部的this就指向b对象，b对像的a属性就是2。

接下来我们就看看this可以使用的场合。

### this使用场合

this可以在这几个场合使用：

#### 1. 全局环境

在全局环境下使用this，this对象代表的是window对象。

```js
console.log(this === window); // true
function fun(){
  console.log(this === window); 
}
fun();  // true
```

#### 2. 构造函数

在构造函数中使用this，this对象代表的是构造函数的实例对象。

```js
function Person(name){
  this.name = name;
}
var Jeff = new Person('Jeff');
console.log(Jeff.name); // Jeff

```

这里的this就表示的是实例对象Jeff,在构造函数内部this.name就在使用new关键字后就像相当于Jeff.name。

#### 3. 对象的方法

在对象的方法中使用this，this对象代表的就是这个对象。

```js
var Jeff = {
  name:'Jeff',
  age:'22',
  say(){
    console.log(this);
  }
}
Jeff.say(); //Jeff
```

在作为对象的方法使用时，this指向的就是这个对象。

### 4. 绑定后的this

上面不同的环境，this对象代表不同的值。js提供了3种方式让我们可以让this绑定指向。

1. call方法

函数实例的call方法，可以指定函数内部this的指向。然后在所指定的作用域中，调用该函数。

```js
function fun(){
  console.log(this);
}
var Jeff = {

}
fun();  // window
fun.call(Jeff); // Jeff
```

call方法也可以传入多个参数。第一个参数是一个对象，目的是将函数实例内部this绑定在上面。如果第一个参数为空、null、undefined，则默认传入全局对象。后面的参数是函数调用时所需的参数。

2. apply方法

apply方法的作用与call方法类似，也是改变this指向，然后再调用该函数。唯一的区别就是，它接收一个数组作为函数执行时的参数。

```js
function fun(a,b){
  console.log(a+b);
}
fun.call(null,1,2); // 3
fun.apply(null,[1,2]);  //3
```

上面写了一个方法，但是使用了call方法和apply方法去绑定this的指向，我们看call和apply只有参数传递上的区别。

3. bind方法

bind方法用于将函数体内的this绑定到某个对象，然后返回一个新函数。这个函数也可称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind() 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。

```js
var counter = {
  count: 0,
  inc: function () {
    this.count++;
  }
};

var func = counter.inc.bind(counter);
func();
cinsole.log(counter.count); // 1
```

当你希望改变上下文环境之后并非立即执行，而是回调执行的时候，使用bind方法。

## 总结

构造函数上的两个特性new关键字和this关键字。这都是我们在编写面向对象的javascript的基础。