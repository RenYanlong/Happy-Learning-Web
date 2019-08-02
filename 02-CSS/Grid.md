# Grid布局

## 背景

我最早接触到的Grid的概念是在bootstrapku库中，但是并没有在实际的工作中使用过。

如今浏览器已经内置了Grid，这让我们不需要通过引入第三方库去实现Grid布局。而随着网页布局复杂化，学习Grid相关显得尤为重要（在9102年学习Grid也不是很早了！）。

在CSS3中引入了flexbox为我们在布局操作提供了很大的方便，如：垂直方向的居中，在flex出现前，我们会使用position或者transform的方式去操作垂直居中，这样写的代码繁琐而难以维护，更不要提及更加原始的表格布局了。

## Grid概述

说回Grid，Grid布局可以说是CSS中最强大的布局方式了。

Grid布局将页面分割成一个个网格，可以任意合并网格为网格块。Grid布局和flexbox还是有相似之处的，就是通过父元素指定内部元素的位置。而最大的不同是排序的方式，flexbox是通过定义轴线的方式，而Grid是通过单元格。

## Grid容器

### 1. Grid容器定义

想要创建Grid布局的第一步是将单元格容器定义为grid。

我们使用display属性定义容器类型，这点和flex布局定义非常相似。

```
display: grid / inline-grid
```

### 2. 定义网格

既然称之为网格，那么需要行和列的组成。每行和没列相互交叉，则构成了单元格。这也是构成网格容器的基石。

使用grid-template-columns和grid-template-rows分别定义列和行的宽度。

```
display:grid;
grid-template-row:100px 100px 100px;
grid-templage-columns:100px 100px 100px;
```

上面我们定义了3行和3列，每行的宽度分别为100px,20%,和自动宽度。3列的宽度也和行一一对应的宽度。

这里定义的宽地仅仅使用了绝对单位。是为了更容易理解。

这里需要说几个宽度的单位：绝对单位、百分比、repeat()、auto-fill()、fr、minmax()、auto。这里仅仅是将这些设置宽度的单位罗列出来，不会对其他的概念造成影响。等我们对整体的网格布局有了更加深入的了解后，我们在回来看这一部分。

### 3. 网格间距设置

我们设置了网格，同时也可以让网格之间产生间距。

使用gap属性（缩写，我认为缩写可以让你记忆更加少的属性而不产生困扰）。

```
display:grid;
grid-template-row:100px 100px 100px;
grid-templage-columns:100px 100px 100px;
gap: 20px 30px; 
```

第一个参数为行与行之间的空隙，第二个参数表示列与列之间的空隙。

### 4. 指定网格区域

网格布局中我们是可以定义网格区域的，每个区域可以由一个或者多个网格构成。

使用grid-template-areas属性定义每个网格区域。

```
display:grid;
grid-template-row:100px 100px 100px;
grid-templage-columns:100px 100px 100px;
grid-template-areas:'a,a,c'
                    'd,e,f'
                    'g,h,i';
```

在设置网格区域的时候，会将相同名字的单元格划分以一个网格区域。如上面的第一个和第二个单元格设置为区域a。

### 5. 单元格顺序排列

单元格是可以设置排列顺序的，可以按照横向或者竖向排列。

使用grid-auto-flow属性进行排序。默认排序是横向的。

```
display:grid;
grid-template-row:100px 100px 100px;
grid-templage-columns:100px 100px 100px;
grid-auto-flow:row \ column (dense);
```
在设置为row时，按照横向排列，设置为column为竖向排列。这里说明一下括号里的dense属性，它表示尽量填满空格，会使用合适的单元格填充到剩余的空间。

### 6. 单元格内容布局

在网格容器中我们可以设置单元格内容布局，使用algin-items、justify-items、place-items属性即可。

```
display:grid;
grid-template-row:100px 100px 100px;
grid-templage-columns:100px 100px 100px;

justify-items:center; //水平方向
algin-items:center; //垂直方向
place-items:center center;  //垂直方向 / 水平方向
```

这样单元格内容会在单元格中按照相应的布局排列。

### 7. 整个单元格区域在容器里的布局

我们也可以设置整个内容区域在容器里面的位置。使用justify-content、align-content和place-contnt属性定义。

```
display:grid;
grid-template-row:100px 100px 100px;
grid-templage-columns:100px 100px 100px;

justify-content：center;  
algin-content:center;
place-content:center center;  //垂直方向 水平方向
```

整个内容区域在容器里面的位置会根据你设置的布局排列。


### 8. 多余的单元格

有时候，多余的单元格会超出我们已经创建的单元格。

使用grid-auto-columns属性和grid-auto-rows属性；

```
display:grid;
grid-template-row:100px 100px 100px;
grid-templage-columns:100px 100px 100px;
grid-auto-columns:50px;
grid-auto-rows:50px;
```

超出单元格数量的单元格会按照你设置的相应的宽度。


这里就是所有网格容器的所有属性。其实还是有规律可言的，先设置排列方式 -> 设置行和列的宽度 -> 设置行间距和列间距 -> 设置网格区域 -> 单元格顺序 -> 单元格内容布局 -> 整体单元格内容布局

已上就是可以在网格容器设置的属性，必须设置的是前两个，而后面的属性更是像是对单元格样式的定义，即使不定义也可以正常设置为网格布局。

## 项目属性

### 1. 指定单元格的位置

我们设置指定单元格的位置属性。具体方法就是指定项目的四个边框，分别定位在哪根网格线。

```
grid-column-start:1;  //列起始位置
grid-column-end:3;  //列结束位置
grid-row-start:1; //行起始位置
grid-row-end:3; //列结束位置
```

设置指定单元格的位置属性也有缩写方式，下面的书写方式和上面的作用一样。

```
grid-column: 1 / 3; //列起始位置 / 结束位置
grid-row: 1 / 3;  //行起始位置 / 结束位置
```
这样就可以根据网格线设置单元格位置，如果产生了项目的重叠，则使用z-index属性指定项目的重叠顺序。

### 2. 指定项目放置区域

我们可以设置指定单元格放在哪一个区域，使用grid-area属性即可设置。

```
grid-area:e;
```

上面的代码将单元格放置在区域e。

### 3. 设置单元格自身内容排列方式

我们可以给指定相应的单元格内容的排列方式，使用justigy-self、align-self、place-self属性可以单独设置自己的单元格内容排列方式。

```
justify-self:center;  
align-self;center;
place-self:cneter;
```
place-self设置和前两行的作用一致。如果省略第二个值，place-self属性会认为这两个值相等。

单元格自身属性的设置就在三个点：1. 设置自身位置；2. 设置自身区域；3. 设置自身内容排列方式。在自身设置属性更多的意义是和在网格容器中定义统一的样式布局有更多自我的样式布局。

## 总结

Grid布局的属性还是很多的，我们需要一些时间和实践去消耗理解，如果你希望可以在项目中使用Grid布局，你应该关注Grid布局的兼容性。

说一下我自己对Grid布局如何加深理解的：有时候用生活更加拟物的概念去理解我们学习中抽象内容会有利于我们的理解。我就会将网格系统联想到现实中的渔网。单元格更像是每个网眼。网格线就是我们我们的渔网线，我们可以对渔网尽心定制，使用不用粗细的渔网线就是我们设置网格间距等等。