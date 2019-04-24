# JavaScript学习路径

在9102年，我们常说的JavaScript应该包括了是ES6,而ES6是向下兼容的！

###### 基本语法

[JavaScript 基本语法](https://wangdoc.com/javascript/basic/grammar.html)是JavaScript最最最基础的知识。

###### 对象

JavaScript中的值“皆为”*[对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Working_with_Objects)*，对象作为属性的容器，是非常适合用于汇集和管理数据的。

这里需要强调的是，**JavaScript是一门基于原型的语言**。

###### 函数

JavaScript中[函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions#函数参数)是*对象*，函数可以像任何其他值一样被使用。

函数名是指向函数对象的**指针**，它不会与函数本体绑定，这个概念很重要！

函数中有个很重要的概念——[闭包](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)。这是大家需要重点理解的。掌握**作用域**对理解闭包有很重要的作用。

###### 原型

[原型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)是JavaScript实现继承主要的方式。

在新的标准中我们可以通过[类](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes)实现继承等特性，也让JavaScript看起来更像面向对象的语言。但是我们需要知道：实际上**类**也是通过原型实现的。所以原型是我们实现*继承*的重中之重！

###### 内置对象

 我们应该了解JavaScript 中所有的[标准的内置对象、以及它们的方法和属性](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects)。
 
 包括上面我们列出的**对象**、**函数**等。以及我们没有列出的**Date**、**Array**等。这部分需要记住的内置对象方法较多。
 
###### BOM

BOM(浏览器对象模型)用于访问浏览器的功能。它提供了很多对象，我们应该将重点放在[Location对象](https://developer.mozilla.org/zh-CN/docs/Web/API/Location)和[history](https://developer.mozilla.org/zh-CN/docs/Mozilla/Add-ons/WebExtensions/API/history)两个对象上面。

###### DOM

[DOM(文档对象模型) ](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Introduction)则是HTML和XML文档的编程接口。它提供了对文档的结构化的表述，并定义了一种方式可以使从程序中对该结构进行访问，从而改变文档的结构，样式和内容。

在现代网页编程中， 我们可以使用react、vue、angular 等不直接操作DOM的框架。当然，这需要看个人情况而定。

###### 事件

[事件](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events)可以监控用户发生的动作或者事情。

我们应该重点了解事件冒泡、事件捕获等事件概念。这对我们整个事件发生的过程理解非常重要。

###### JSON

[JSON对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON)如果你看了内置对象后应该有所了解，JSON对象是一种轻量级的数据交换格式。我们在日常的工作中最最最常见的！

###### 网络编程

这部分希望大家可以使用[Fetch API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch) 接口，用于访问和操纵HTTP管道的部分。

同时在网络上有较多的开源库，如axios，都很好的让我们实现Ajax所做的事情。~~拥抱新技术是学习前端正确姿势！~~
