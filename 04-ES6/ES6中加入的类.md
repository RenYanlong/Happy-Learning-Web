# JavaScript的新特性-class

一开始我们应该知道一件事：**ES6中的class关键字就是一个语法糖，class语法从本质上是基于原型代码的。**

ES6中引入了类关键字是将ES5中传统继承模型通过语法包装成的语法糖。让JS看起来更下像其他语言。但实质ES6的类与其他面向对象的语言还是有区别的。

#### 类声明

使用*class关键字*创建类，关键字后面是变量标识符，最后是*类主体*。这样的写法称之为**类声明**。

```JavaScript
//类声明
class Proson {                          
  constructor(name,age) {   //constructor方法等价于之前的构造函数
    this.name = name;
    this.age = age;
  }
  dosomething(){
    console.log(this.name,this.age);
  }
}
const lili = new Proson('lili',20);
lili.dosomething();  //lili,20
```

#### 类表达式

将一个类赋值给一个变量的形式叫**类表达式**。类表达式是定义类的另一种方式，仅仅是语法上的不同。

```JavaScript
//匿名类表达式
let Preson = class {
  constructor(name,age) {  
    this.name = name;
    this.age = age;
  }
  dosomething(){
    console.log(this.name,this.age);
  }
}
```

```JavaScript
//命名类表达式
let Preson = class PresonClass {
  constructor(name,age) {   
    this.name = name;
    this.age = age;
  }
  dosomething(){
    console.log(this.name,this.age);
  }
}
```

#### constructor方法

contructor方法用来定义构造函数。我们可以在contructor方法中初始化对象的属性。也就是说，ES5的的构造函数Preson，对应ES6的Preson类的contructor方法。

contructor构造方法不是必须的，如果没写contructor构造方法，引擎会自动为我们添加一个空的contructor构造方法。


#### 类的继承和子类

ES6的类让继承功能更加容易的实现。**extends**关键字用于指定**继承的类**。也就是我们通常说的**继承**的概念，通过类的extends让我们已更轻松的实现继承功能，而通过super()方法访问基类的构造函数。

```JavaScript
//son是一个子类
class son extends father{
  constructor(name,age){
    super(name,age);  
  }
  say(){
    console.log(name,age);
  }
}
let lili = new son('lili',20);
console.log(lili.say());  //lili,20
```

**继承**自其他类的类被称之为**派生类**或**子类**。如果派生类中指定了构造函数则必须调用super()，如果不指定构造函数，则新创建类的实例时会自动调用super();

子类拥有拥有一切关于基类的特性，同时还有其他的特点：

    1. 仅可以在子类中的构造函数中使用spuer();
    2. 子类里的构造函数不能为空，即使仅仅调用了super(),也需要显示的写出来。但是子类中可以没有构造函数
    3. 在子类的构造函数中，仅仅使用了super()初始化this后才可以使用this关键字。


#### 类的方法遮蔽

子类的方法总是会屏蔽父类中的同名方法。


```JavaScript
class son extends father{
    constructor(name){
        super(name);
    }
    //say方法会覆盖father类的say方法
    say(){
        console.log(this.name);
    }
}
```

#### 总结

总的来说，class的加入让JavaScript中继承更方便使用，通过语法糖的形式，让JavaScript看着更加像面向对象的语言。但是我们还应了解内在的原型相关知识。