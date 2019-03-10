# Flex布局

#### Flex布局的由来

CSS标准为我们提供了3种布局方式：

* 标准文档流
* 浮动布局（float）
* 定位布局（position）

这几种方式的搭配使用可以轻松搞定 PC 端页面的常见需求。

但是这些写法都存在缺少语义并且不够灵活的缺陷。我们需要的是通过一个属性就能优雅的实现子元素居中或均匀分布，甚至可以随着窗口缩放自动适应。就这样flex布局诞生了。

#### 概念

flex布局的核心的概念就是**容器**和**轴**。可以说flex布局的全部特性都构建在这两个概念上。

**容器**包括外层的*父容器*和内层的*子容器*，**轴**包括*主轴*和*交叉轴*。

flex布局涉及到12个CSS 属性（不含 display: flex），其中父容器、子容器各6个。

~~都记住！~~不过常用的属性只有4个，父容器、子容器各2个。

#### 容器

**容器**具有这样的特点：父容器可以统一设置子容器的排列方式，子容器也可以单独设置自身的排列方式，如果两者同时设置，以子容器的设置为准。

##### 父容器

display是用来定义伸缩容器，是内联还是块取决于设置的值。

```
display:flex | inline-flex  
```  

flex-direction用来定义主轴的方向，即项目的排列方向。

```
flex-direction: row | row-reverse | column | column-reverse;
//row:水平方向，起始点在左侧 | row-reverse:水平方向，起始点在右侧 | column:垂直方向，起始点在上沿 | column-reverse:垂直方向，起始点在下沿       
```

flex-wrap用来定义如何换行。

```
flex-wrap: nowrap | wrap | wrap-reverse;
//nowrap:不换行 | wrap:换行，第一行在上 | wrap-reverse:换行。第一行在下
```

上面两个属性我们可以使用flex-flow属性简写。

```
flex-flow:<flex-direction> | <flex-wrap>
```

justify-content定义子容器如何沿着主轴方向排列。

```
justify-content:flex-start | flex-end | center | space-around | space-between 
//flex-start:主轴起点对齐 | flex-end:主轴终点对齐 | center:居中对齐 | space-around:每个项目的两侧间隔相等，首尾两端的子容器到父容器的距离是子容器间距的一半。 | space-between:两端对齐，项目之间的距离都相等
```

align-items定义如何沿着交叉轴方向分配子容器的间距。

```
align-items:flex-start | flex-end | center | baseline | stretch;
//flex-start:与交叉轴的起点对齐 | flex-end:与交叉轴的终点对齐 | center:居中对齐 | baseline:首行文字基线对齐 | stretch:拉伸至与父容器一致
```

align-content定义多根轴线的对齐方式，如果只有一行，则不生效。

```
align-content:flex-start | flex-end | center | space-around | space-between;
//flex-start: 与交叉轴起点对齐| flex-end:与交叉轴终点对齐 || center:居中对齐 | space-around:两侧间隔相等，首尾两端的子容器到父容器的距离是子容器间距的一半 | space-between:两端对齐，项目之间的距离都相等
```

以上就是所有父容器的所有属性了，我们应该终点清楚flex布局的思路：

1. 定义flex布局，也就是使用display属性
2. 定义主轴方向和换行，这里我们用flex-flow属性
3. 定义主轴上子容器的布局排列，这里我们使用justify-content属性
4. 最后我们定义交叉轴上子容器的排列顺序，如果只有一行的话使用align-items属性，多行的话使用align-content

这就是一个flex布局父容器的完整定义思路了。下面我们看看子容器。


##### 子容器

order定义了项目子容器的排列顺序，数值越小，排列越靠前。

```
order:<integer>;
```

flex-grow定义了项目放大比例。默认值是0，也就是即使有剩余空间也不放大。flex-grow数值越大，占据剩余空间越大。

```
flex-grow:<number>;
```

flex-shrink定义了项目的缩小比例,默认为1，即当空间不足时，项目会自动缩小。如果设置为0，则不缩小。

```
flex-shrink:<number>
```

flex-basis定义了项占据主轴的空间。默认值为auto，即子容器原本的大小。单位可以设置为像素或者百分比。

```
flex-basis: <length> | auto;
```

我们通常会使用flex属性缩写上面的三个属性。默认值为0,1,auto

```
flex:<flex-grow> | <flex-shrink> | <flex-basis>;
```

align-self定义了单个项目与其他项目不一样的对齐方式。覆盖了align-items属性，默认auto，继承了父容器align-items属性。

```
align-self: auto | flex-start | flex-end | center | baseline | stretch;
//align-items属性一致
```
以上就是所有父容器的所有属性了，我们定义子容器的属性的时候应按照以下思路：

1. 是否需要排序，有则使用order属性
2. 使用flex定义子容器的放大、缩放等属性
3. 如子容器的对齐方式与其他的不一致，则使用flex-self属性


### 总结

以上介绍了Flex布局的语法，Flex布局更灵活、易懂，能解决很多复杂场景。

缺点就是浏览器的兼容性没有传统布局的好。当然这一切都交给时间就可以了。


