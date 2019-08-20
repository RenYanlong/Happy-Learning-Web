# 新加入的原始类型——Symbol

ES6添加了新的基本数据类型——Symbol。Symbol的目的是：*作为对象属性的标识符*。

#### 创建Symbol

通过全局函数Symbol创建一个Symbol，Symbol函数接受一个可选参数，用于描述即将创建的Symbol。

```JavaScript
let a = Symbol();
let a1 = Symbol('a1');
console.log(a,a1);  //Symbol(),Symbol(a1)
```

每次都会创建一个新的symbol类型

```javascript
symbol('sym') === symbol('sym');  //false
```

#### Symbol共享体系

###### Symbol.for()

如果有多个不同的对象类型，但是希望可以使用同一个Symbol属性表示一个独特的标识符，这样我们应该创建一个共享的Symbol。

我们应该使用Symbol.for()方法。Symbol.for()会在全局搜索Symbol属性是否存在，如果存在则返回已有的Symbol，如果不存在，则创建新的Symbol并返回。

```javascript
let num = Symbol.for('123');
    obj = {};
console.log(obj[num]);  //123
console.log(num);   //Symbol(123);
let num1 = Symbol.for('123');
consolr.log(num === num1);  //true
console.log(obj[num1]);  //123
console.log(num1);   //Symbol(123);
```

###### Symbol.keyFor()

Symbol.keyFor()则索引与Symbol有关的key。

```
let a = Symbol.for('a');
let b = Symbol.for('b');
console.log(Symbol.keyFor(a)) // a
console.log(Symbol.keyFor(b)) // b
```

#### Symbol与类型转换

JavaScript中基本类型是可以隐形转换的，而Symbol是不会进行隐性转换操作的。

```javascript
let a = Symbol('123');
    b = String(a);
console.log(b); //'Symbol(123)'
```

上面调用了String方法强制转换为一个字符串，如果不进行强制转换，则程序会报错。

也不能将Symbol转换为数字类型，使用运算符也会产生错误。


#### 属性检索

在Symbol中我们需要通过新增加的方法检索属性，使用**getOwnPropertySymbols()**方法。

```javascript
let a = Symbol('a');  
    obj = {
      [a]: "123";
    } 
const symbolsKey = Object.getOwnPropertySymbols(obj);
    for(let value of symbolsKey) {
      console.log(obj[value]);  //123
    }
```

#### 总结

我们需要理解Symbol被创建的意义就是**作为对象属性的标识符**。如何定义Symbol类型和相关Symbol类型的方法是我们应该记住的！