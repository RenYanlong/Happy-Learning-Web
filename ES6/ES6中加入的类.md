# ES6中加入的类

一开始我们应该知道一件事：*class声明就是一个语法糖，class声明语法从本质上是基于原型代码的。*

ES6中引入了类的特性，让JS看起来更下像其他语言。但ES6中的类与其他面向对象的语言还是不太一样。ES6中的类语法是作为了ES5传统继承模型的语法糖出现。

class语法通过使用了*原型的技术*模仿了传统类的机制，以便提供更加简介的语法。

#### 定义类

我们使用*class关键字*创建类，关键字后面是变量标识符，最后是*类主体*。这样的写法称之为**类声明**。没有使用extends关键字的类声明称之为**基类**。

###### 类声明

使用**class关键字**声明一个类。

```
//Proson是一个基类
class Proson {
  constructor(name，age) { 
    this.name = name;
    this.age = age;
  }
  todo(){
    console.log(this.name,this.age);
  }
}
const lili = new Proson(`lili`,20);
lili.todo();  //lili,20
```

将一个类赋值给一个变量的形式叫**类表达式**。类表达式是定义类的另一种方式，可以替代上面的**类声明**。

```
//这是一个匿名类表达式
let Preson = class {
  //与上面一样的定义
}

//这是一个命名类表达式
let Preson = class PresonClass {
  //与上面一样的定义
}
```

定义类时我们应该注意的是：

1、类中只有方法定义，不能有数据属性
2、定义方法时，可以使用简写方法定义
3、不能使用逗号对类中的方法定义进行分割
4、我们可以在实例化对象上直接使用类的属性

###### constructor方法

类有一个独有的特性，就是contructor构造方法。在构造方法中我们可以初始化对象的属性。也就是说，ES5的构造函数Preson，对应ES6的Preson类的构造方法。

contructor构造方法不是必须的，如果没写contructor构造方法，引擎会自动为我们添加一个空的contructor构造方法。


#### 使用extends创建子类以及使用super调用

使用extends创建的类被称作**子类**，或**派生类**。也就是我们通常说的**继承**的概念，通过类的extends让我们已更轻松的实现继承功能，

```
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

继承自其他类的类被称之为派生类，如果派生类中指定了构造函数则必须调用super()；如果不指定构造函数，则新创建类的实例时会自动调用super();

子类拥有拥有一切关于基类的特性，同时还有其他的特点：
1、子类希望引用它的父类，可以使用spuer();
2、子类里的构造函数不能为空，即使仅仅调用了super(),也需要显示的写出来。但是子类中可以没有构造函数
3、在子类的构造函数中，仅仅使用了super()，才可以使用this关键字。

在JavaScript中仅仅有连个地方可以使用super():

1、在子类构造函数中调用。如果初始化子类需要使用父类中的构造函数，我们可以在子类中的构造函数中调用super(),
2、引用父类的方法。派生类可以使用点运算符来引用父类的方法，如：super.fatherName


#### class怎么映射到原型上的

在ES6之前我们使用构造函数创建对象。构造函数我们很熟悉，使用new关键字调用构造函数返回新对象。

```
function Food(name,age){
  this.name = name;
  this.age = age
}

const food = new Food('chicken',2)
console.log(food.name); //chicken

```

这里我们在回顾一下new关键字调用构造函数时发生了什么：

1、创建一个新的对象
2、将this指向新对象（原型）
3、为新对象添加属性
4、返回新对象

###### 原型链

通常在JavaScript中所有的对象都都会链接到另一个对象上，这就是**原型**。

如果一个对象中不存在我们访问的属性，则JavaScript会在对象的原型上检查属性。这也就称之为**委托**。

```
const lili = {
  name:`lili`
},
huahua = {
  name:`huahua`
}
//检测对象中是否有toString方法
Object.hasOwnProperty(lili,toString); //false
Object.hasOwnProperty(huahua,toString); //false

//调用toString方法
lili.toString();  //'[object Object]'
huahua.toString();  //'[object Object]'
```

上面的例子在没有在自身对象上检测到toString方法时，会在原型上检测是否存在toString方法。从而调用原型上的方法。

我们就可以访问到对象上并不存在的属性，只要其的原型上有这些属性。我们可以利用这一点将属性和方法赋值到对象的原型上，然后我们就可以调用这些属性，好像它们真的存在在那个对象上一样。

原型上的属性是共有的，不是单独的将属性拷贝到每一个对象上。

这也就是大家常说的**原型继承**。如果对象没有，但对象的原型有，那我的对象也能*继承*这个属性。这里的*继承*并没有发生传统面向对象中继承的复制操作，而只是*委托到原型上*。

#### 设置对象的原型

当我们创建一个函数，这个函数就会有一个属性prototype，指向一个叫做.prototype的对象。

与之相反.prototype对象会有一个contructor的属性，它的引用指回函数。

设置原型对象有三个规则：
1、默认规则
2、使用new隐式规则
3、使用Object.create显式设置原型

###### 默认规则

const food = {name:`lili`};

当创建一个对象，JavaScript将原型对象指向Object.prototype并设置原型的contructor的属性为Object。

###### new隐式规则

```
function food (name){
  name:`lili`
}
const food = new food(`lili`);
```

当我们使用new关键字创建一个对象，原型指向new关键字调用函数的prototype属性。这个对象的contructor属性指向我们使用new调用的构造函数。

###### 使用Object.create显式设置原型

最后我们使用Object.create方法手动设置对象的原型引用。

```
const foo = {
    speak () {
        console.log('Foo!');
    }
};
const bar = Object.create(foo);
bar.speak(); // 'Foo!'
Object.getPrototypeOf(bar) === foo; // true
```

Object.create方法在幕后做了下面的三件事：
1、创建一个新对象；
2、设置它的原型引用；
3、返回这个新对象。


#### class的方法

类支持三种方法，以及一种特殊情况。

*类构造器
*静态方法
*原型方法
*特殊情况——标记方法

###### 类构造器

constructor方法用于关注我们初始化的逻辑，constructor方法几个特殊点：

1、只有在构造器中才能调用父类的构造器
2、它在背后处理了所有设置原型链的设置
3、用作类的定义

###### 静态方法

**静态方法**是构造方法自己的方法，不能被类的实例化对象调用。我们使用*static*关键字定义静态方法。

###### 原型方法

任何不是构造方法和静态方法的方法都是**原型方法**。之所以叫原型方法，是因为我们之前通过给构造函数的原型上附加方法的方式来实现这一功能。

###### 标志方法

**标志方法**，这是一些名为Symbol值的方法，当我们在自定义对象中使用内置构造器时，JavaScript引擎可以识别并使用这些方法。

#### 总结

ES6中没有给我们带来真正的**类**，它只是提供了一种更加方便的语法来创建通过原型关联的对象，本质上没有什么新东西。

我们应该了解JavaScript的原型机制，可以让我们在class的原理上理解class的由来和作用