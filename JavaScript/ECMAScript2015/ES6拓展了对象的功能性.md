# ES6拓展了对象的功能性

ES6通过多种方式加强了对象了使用，提升了对象的功能性。通过简单的语法拓展，提供了更多操作以及对对象交互的方法。

#### 对象类别

ES6明确的定义了每一个类别的对象，对象的类别如下：

* 普通对象：具有JavaScript对象所有的默认内部行为。
* 特异对象：具有某些与默认行为不符的内部行为。
* 标准对象：ES6规范中定义的对象。如：Array、Date等。
* 内建对象：脚本开始执行是存在于JavaScript执行环境中的对象，所有的标准对象都是内部对象。

#### 对象字面量语法拓展

ES6通过新的语法，让对象字面量更加强大、更加简洁。

ES5中通过函数创建对象

```
function Person(name, age) {
  return {
    name: name,
    age: age
  }
}
```
ES6中可以通过简洁写法，消除这种属性和局部变量之间的重复写法。

```
function Person(name, age) {
  return {
    name,
    age
  }
}
```

#### 对象方法的简洁语法

ES5之我们需要通过制定名称并完整的定义函数来实现。

```
let person = {
  name:'xiaoming',
  say:function(){
    console.log(`I am ${this.name}`);
  }
}
```
ES6中同样通过更加简洁的语法在对象中定义函数。

```
let person = {
  name:'xiaoming',
  say(){
    console.log(`I am ${this.name}`);
  }
}
```

#### 可计算属性名

在ES6中对象字面量中可以使用可**计算属性名称**.

```
let name = `name`;
let person = {
  [`last${name}`]: `liu`,
  [`first${name}`]:`xiaoming`
}
console.log(person[`lastname`]);    //liu
```

#### 重复的对象字面量属性

ES6之前定义重复的对象属性，在严格模式下会产生语法错误。

```
'use strict'
let person = {
  name:'xiaoming',
  name:'huahua'     //报错
}
```

在ES6中重复属性查询被移除，无论是否在严格模式下，对于重复定义的属性，都会选取最后一个定义值。

```
'use strict'
let person = {
  name:'xiaoming',
  name:'huahua'     //无错误
}
console.log(person.name);   //huahua
```

#### 新增方法

ES6中不希望创建新的全局函数，也不希望在Object.prototype上创建新的方法。

为了让一些任务更容易完成，所以在全局Object对象上加入新的方法。

###### Object.is()

Object.is()用于比较两个值是否相等。

这让我们想起了"=="和"==="，但是全等运算符和Object.is()也有区别。

```
console.log(NaN === NaN);   //false
console.log(Object.is(NaN,NaN));    //true

console.log(5 == '5');  //true
console.log(5 === '5'); //false
console.log(Object.is(5,'5'));  //false

console.log(-0 == +0);  //true
console.log(-0 == +0); //true
console.log(Object.is(-0,+0));  //false
```

上面都是之前javascript遗留下来的问题，我们可以通过Object.is()处理。全等运算符我们依旧可以在大部分情况下使用，其结果和Object.is()也大部分相同。


###### Object.assign()

Object.assign()用于实现对象组合的一种模式。使一个对象接收来自另外一个对象的属性和方法。此处的赋值是[浅拷贝](https://segmentfault.com/a/1190000011455690)

```
let xiaoming = { name: 'xiaoming' };
let huahua = { age: 15 }
console.log(Object.assign(xiaoming, huahua));   //{name: "xiaoming", age: 15}
```
    
Object.assign()方法可以接受任意数量的源数据，并按照顺序将属性赋值到接受对象中。如果有多个对象具有相同的属性名，则后面的覆盖前面的。

#### 枚举顺序

ES6中规定了对象属性枚举时的返回顺序，加入顺序后影响了Object.getOwnPropertyName()方法返回属性的方式，而上面提到的Object.assign()方法处理属性的顺序也会改变。

枚举顺序基本规则：
1. 所有数字键提前，升序排列
2. 所有字符串键按照加入对象的顺序排序

```
let person = {
  1:1,
  name:`xiaoming`,
  4:4,
  3:3,
  age:12
}
console.log(Object.getOwnPropertyNames(person));    //["1", "3", "4", "name", "age"]
```

#### 增强对象原型
    
##### Object.setPrototypeOf()

用于改变对象原型，两个参数：需要改变原型的对象和原型对象。

```
let boy = {
  say() {
    return `boy`
  }
}
let girl = {
  say() {
    return `girl`
  }
}
let xiaoming = Object.create(boy);
console.log(xiaoming.say());  //boy
console.log(Object.setPrototypeOf(xiaoming, girl));
console.log(xiaoming.say());    //girl
```


#### 总结

ES6中有关于对象功能的拓展大致有一下几点：

1. 语法的改进进行了一些改进。
2. 增加了新的方法处理对象，和枚举顺序的加入对原有对象方法的影响
3. 可以改变对象的原型



