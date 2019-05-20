# this

this的指向仅需牢记一点：this的指向基于函数调用的情况。和函数在哪定义无关，而和函数怎么调用有关。

简单的说就是**this指向谁是看谁调用的**。

这样我们在具体分析通常调用this的几种情况：

##### 全局环境

在全局环境，this指向全局对象window。

```javascript
console.log(this == window);    //true
```

##### 独立函数环境

独立函数调用，this必须指向对象，默认为window。

```javascript
function a (){
	return this
};
a() === window; //true
```

##### 对象方法环境

作为对象方法调用，this指向该对象

```javascript
let obj = {
    prop: 37,
    fun() {
        return this.prop;
    }
}
```

在构造函数中，通过new关键字，this指向new生成的新对象。

##### 指定函数运行时

call和apply可以指定函数运行时的this


```javascript
function add(c, d){
  return this.a + this.b + c + d;
}

var o = {a:1, b:3};
add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```

##### 箭头函数

箭头函数中，this指向不受调用影响，总是指向运行环境对象。

##### 总结

牢记this的指向基于函数调用的情况。和函数在哪定义无关，而和函数怎么调用有关。


