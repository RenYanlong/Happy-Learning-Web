# ES6中加入的类

ES6之前我们使用**构造函数**和**原型**实现类以及类的继承。

ES6中引入了类的特性，让JS看起来更下像其他语言。但ES6中的类与其他面向对象的语言还是不太一样。ES6中的类语法是作为了ES5传统继承模型的语法糖出现。

#### 定义类

类更像一个**特殊的函数**，因此你可以像定义函数声明或者函数表达式一样定义类，类也可以通过**类声明**和**类表达式**定义。

###### 类声明

使用**class关键字**声明一个类。

```
class Proson {
  constructor(name) {
    this.name = name;
  }
}
```

###### 类表达式

类表达式是定义类的另一种方式，类表达式可以是匿名的，也可以是命名表达式。

```
//匿名类表达式
let Preson = class {
  constructor() { }
}
//命名类表达式
let Preson = class Preson1 {
  constructor() { }
}
```

#### 类的实例

生成类的实例，直接对类使用new命令，跟构造函数的用法完全一致。如果没有通过new关键字，而是想调用函数那样调用类，则会报错。

```
class Proson {
  say() {
    console.log('lili');
  }
}
let lili = new Proson();
lili.say(); //lili
let lili = Proson();  //报错
```

#### 类与自定义类型之间的差异

1. 类声明不会被提升，而自定义函数会提升
2. 类声明强制执行严格模式
3. 类声明所有方法都不可枚举，而自定义类型则可以通过Object.definePrototype()方法手工指定不可枚举属性。
4. 每个类都有一个[[construct]]的方法
5. 类声明只能使用new关键字调用
6. 不能在类中修改类名。

#### 类同样是一等公民

函数作为一等公民，而类也被设计成一等公民，允许通过多种方法使用类的特性。

如：

###### 通过类构造函数创建单例

```
let preson = new class {
  constructor(name) {
    this.name = name
  }
  sayName() {
    console.log(this.name);
  }
}('eryue')
preson.sayName(); // eryue

```

###### 访问器属性

类允许直接在原型上定义访问器属性

```
class Preson {
  constructor(state) {
    this.state = state
  }
  // 创建getter
  get myName() {
    return this.state.name
  }
  // 创建setter
  set myName(name) {
    this.state.name = name
  }
}
let desriptor = Object.getOwnPropertyDescriptor(Preson.prototype, "myName")
console.log("get" in desriptor) // true
console.log(desriptor.enumerable) // false
```

###### 可计算成员名称

类方法与函数相似，可以使用可计算属性。

```
let sayname = 'say';
class Preson {
  constructor(name) {
    this.name = name;
  }
  [sayname](){
    console.log(this.name)
  }
}
let xiaoming = new Preson('xiaoming');
xiaoming.say(); //xiaoming
```

###### 静态成员

静态成员在所有方法和访问器属性使用static关键字。static修饰的方法不能在实例中访问，只能在类中直接访问。

```
class Preson {
  constructor(name) {
    this.name = name;
  }
  static create(name){
    return new Preson(name)
  }
}
let xiaoming = Preson.create('xiaoming')
console.log(xiaoming.name); //xiaoming
```

#### 继承

类的出现让我们已更轻松的实现继承功能，使用extends关键字可以指定类继承的函数

```
class father{
  constructor(length,width){
    this.length = length;
    this.width = width;
  },
  getArea(){
    return this.length * this.width;
  }
}

class son extends father{
  constructor(length){
    super(length,length); //调用了基类的构造函数
  }
}

let father = new father(3);
console.log(father.getArea());  //9
```

继承自其他类的类被称之为派生类，如果派生类中指定了构造函数则必须调用super()；如果不指定构造函数，则新创建类的实例时会自动调用super();

