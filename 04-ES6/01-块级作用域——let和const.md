# 块级作用域-let和const

ES5中，不管是在函数的局部作用域中还是在全局作用域中，都是用**var关键字**定义变量。所以我们无法在if语句、for循环以及其他的块级作用域中定义块级别的变量。

同时，var关键字还带来了**变量提升**的问题。

#### 块级作用域-let和const

ES6新加入了块级作用域——**let关键字**和**const关键字**。

**let**和**const**关键字强化对开发者对变量生命周期的控制。解决了**作用域**和**变量提升**的问题。

用**let替代var**来声明变量，就可以把变量的作用域限制在当前的块中。而且let声明变量不会被提升，因此我们将let声明放在块作用域的顶部，以便整个代码块都可以访问。

在大部分代码都是用在类实例、对象常量或者不会改变的值，所以大部分情况下我们使用**const**。即使是可修改属性的对象，也是可以用const声明的，因为*const表示的是引用的只读，其对象本身仍是可变的*。

**const**和**let**都有暂时性死区，因此只能*先声明，在访问*。

**临时死区**：count和let关键字声明变量不会被提升到作用域顶部，如果在声明之前访问这些变量，就会报错，就是临时死区。

```javascript
function fun(){
    if(true){
        console.log(a); //临时死区,用来描述变量不提升的现象
        console.log(b); //b提升到作用域顶部，但未初始化，值为undefined
        const a = 1;
        var b = 2;
    }
    console.log(a); //undefined  let关键字只在块中有效，所以在if块之外访问a是无效的
    console.log(b); //2  
}
```

#### 总结

声明方式可以翻阅在MDN相关章节。我们重点应放以下几点：

    1. let和const给我们解决的块级作用域和变量提升的问题。
    2. 何时使用let和const这两个关键字。
    3. 这两个关键字给我们带来的临时死区的问题。

###### 相关链接

[let](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let)
[const](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/const)
[为什么选取let这个名字](https://stackoverflow.com/questions/37916940/why-was-the-name-let-chosen-for-block-scoped-variable-declarations-in-javascri)
[let和const命令——阮一峰](http://es6.ruanyifeng.com/#docs/let)