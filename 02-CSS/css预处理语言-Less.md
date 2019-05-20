# css预处理语言-Less

Less在一定程度上拓展了css语言，增加的一些特性可以更加方便的维护和编写css。

### 变量

Less允许我们定义通用样式，然后在使用的地方调用通用样式，这样在全局调整的时候不用每处都进行修改，直接改变通用样式即可。

```
//Less
@color: red;
@color2: #eee;
#header{
    color:@rolor;
}
#footer{
    color:@color2;
}
```

生成：

```
#header{
    color:red;
}
#footer{
    color:#eee;
}
```

### 混合

可以将一个定义好的样式的元素引入到另一个元素中。不仅我们可以继承整个定义好的属性，我们还可以传递参数。


```
.class(@color:red){
    color:@color;
}
#header{
    .class;
}
#footer{
    .class(#eee);
}
```

生成：


```
.class{
    color:red;
}
#header{
    color:red;
}
#footer{
    color:#eee;
}
```

### 嵌套

我们可以通过一个选择器前套另一选择器，这样可以让我们在css中的选择器结构更加清晰。


```
#header{
    p{
        color:red;
    }
}
```

 生成
 
 
```
#header p{
    color:red;
}
```

我们也可以通过&符号编写串联选择器。


```
.bordered {
  &.float {
    float: left; 
  }
}
```
生成

```
.bordered.float  {
    float: left; 
}
```

### 函数和运算

在Less中给我们提供了加、减、乘、除操作，这样我们就可以给颜色或者属性值进行操作，这样就可以实现属性之间复杂的关系。


```
@the-border:1px;
@the-color:#111;

#header{
    border:@the-border * 2;
    color:@the-color * 2;
}
```

生成

```
#header{
    border:2px;
    color:#222;
}
```

### Math函数

Less提供了Math函数，让我们处理一些数字类型的值

```
round(1.67); // `2`
ceil(2.4);   // `3`
floor(2.6);  // `2`
```

### 作用域

Less中的作用域和其他语言相似，首先在局部作用域中查找，如没有则向上查找，直到找到为止。

### 注释

CSS中的注释方法得以保留，Less同样支持//注释语法，不同的是，//注释在编译成css文件后会自动过滤掉。

### 模块导入

我们可以通过导入的形式引入less文件,less后缀可以不带


```
@import 'index.less';
@import 'index';
```

### 字符串插值

我们可以嵌入变量到字符串中。


```
@color:'https://www.baidu.com';
backetground-image('url(@{color}/images.img.jpg'));
```