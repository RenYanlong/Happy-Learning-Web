# Symbol

ES6之前我们有5种原始类型：null、undefined、number、string、boolean、objert。而在
ES6添加了第6种原始类型——Symbol。Symbol用于为属性添加非字符串名称。

### 创建Symbol

通过全局函数Symbol创建一个Symbol，Symbol函数接受一个可选参数，用于描述即将创建的Symbol。

```
let a = Symbol();
let a1 = Symbol('a1');
console.log(a,a1);  //Symbol(),Symbol(a1)

```

### 使用方法

使用可计算属性名的地方，都可以使用Symbol。

### Symbol共享体系

##### Symbol.for()

如果有多个不同的对象类型，但是希望可以使用同一个Symbol属性表示一个独特的标识符，这样我们应该创建一个共享的Symbol。

我们应该使用Symbol.for()方法。Symbol.for()会在全局搜索Symbol属性是否存在，如果存在则返回已有的Symbol，如果不存在，则创建新的Symbol并返回。

```
let num = Symbol.for('123');
    obj = {};
console.log(obj[num]);  //123
console.log(num);   //Symbol(123);
let num1 = Symbol.for('123');
consolr.log(num === num1);  //true
console.log(obj[num1]);  //123
console.log(num1);   //Symbol(123);
```

##### Symbol.keyFor()

Symbol.keyFor()则索引与Symbol有关的key。


```
let a = Symbol.for('a');
let b = Symbol.for('b');
console.log(Symbol.keyFor(a)) // a
console.log(Symbol.keyFor(b)) // b
```


### Symbol与类型转换

js中基本类型是可以隐形转换的，而Symbol是不会进行隐性转换操作的。

```
let a = Symbol('123');
    b = String(a);
console.log(b); //'Symbol(123)'
```

上面调用了String方法强制转换为一个字符串，如果不进行强制转换，则程序会报错。

也不能将Symbol转换为数字类型，使用运算符也会产生错误。


### 属性检索

在Symbol中我们需要通过新增加的方法检索属性，使用getOwnPropertySymbols()方法。

```
let a = Symbol('a');  
    obj = {
      [a]: "123";
    } 
const symbolsKey = Object.getOwnPropertySymbols(obj);
    for(let value of symbolsKey) {
      console.log(obj[value]);  //123
    }
```

### 总结




