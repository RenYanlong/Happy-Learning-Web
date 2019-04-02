# 新的集合类型——Set和Map

ES6新标准加入了Set集合和Map集合，解决了之前使用对象模拟集合的操作。

#### Set集合

ES6中新增的Set类型时一种**无重复有序**列表。包含有一些相互独立的非重复值，通过Set集合可以快速的访问其中的数据，更有效的追踪各种离散值。

###### 创建Set集合

通过**new**关键字创建Set集合

```
let set = new Set();
```

###### 添加元素

通过add()方法为集合添加元素

```
let set = new Set();
set.add(5);
set.add('5');
```

###### 获取集合长度

在数组中我们通过length方法获取长度，在Set集合，我们通过size属性获取集合长度

```
let set = new Set();
set.add(5);
set.add('5');
console.log(set.size);  //2
```

###### 检测是否有指定值

通过has()方法检测集合中是否含有某些值

```
let set = new Set();
set.add(5);
set.add('5');
console.log(set.has(5));    //true
```

###### 移除元素

通过delete()方法移除集合中的某个元素

```
let set = new Set();
set.add(5);
set.add('5');
set.delete(5);
console.log(set.has(5));  //false
```

###### 移除所有元素

通过clear()方法移除集合中的所有元素

```
let set = new Set();
set.add(5);
set.add('5');
set.delete(5);
console.log(set.size);  //0
```

###### forEach()方法

Set集合与数组非常相似，Set集合也添加了forEach()方法，其运行机制也与数组类似。

forEach()方法接收三个参数：
1. Set集合中下一次索引的位置。
2. 与第一个参数一样的值。
3. 被遍历的Set集合本身

因为Set集合没有key，第一个参数和第二个参数一致就是符合逻辑了，使用forEach()方法的回调函数每次执行时，输出的键和值的保持一致。

```
let set = new Set([1,2]);
set.forEach((value,key) =>
    console.log(value + key);   //1+1
                                //2+2
)
```

###### Set合集与数组之间的转换

将数组转换为Set合集非常简单，只要给Set构造器函数传入数组即可。

```
let set = new Set([1,2,3,4,5]);
```

将合集转换为数组也很简单，可以通过**展开运算符**将合集的可迭代对象转换为数组。

```
let set = new Set([1,2,3,4,5]);
let arr = [...set];
console.log(arr);   //1,2,3,4,5
```

###### 数组去重

我们可以运用Set集合元素的非重复性，在数组的去重时使用Set合集的方式

```
let arr1 = [1,2,3,3,3,4,4,6];
console.log([...new Set(arr1)]);    //1,2,3,4,6
```


#### Weak Set集合

Set集合被看成是一个强引用集合，而Weak Set则是弱引用。

Set集合没有其他的变量或属性引用这个对象值, 这个对象值不会被当成垃圾回收掉。而Weak Set则在失去引用后被回收并释放相应内存。所以，Weak Set集合只能储存对象。

###### 创建Weak Set集合和相关方法

Weak Set集合与Set集合类似，同样使用new关键字创建，同时还有add()、has()和delete()方法。

###### 与Set集合不同

1. Weak Set集合是弱引用，而Set集合是强引用。
2. Weak Set集合只能接收对象参数
3. Weak Set集合不可迭代
4. Weak Set集合不支持size属性。

如果希望跟踪对象引用，我们更应该使用Weak Set集合。这样能够更加正确的处理内存中的数据。


#### Map集合

Set集合可以用来处理列表中的值，但是不适合处理键值对这样的信息解构，所以ES6添加了Map集合来解决该问题。

###### 创建Map集合

同样使用new关键字。

```
let map = new Map();
```

###### 添加元素 

我们需要使用set()方法添加元素

```
let map = new Map();
map.set('name':'xiaoming');
```

###### 获取元素

使用get()方法获取数据

```
let map = new Map();
map.set('name':'xiaoming');
console.log(map.get('name'));

```

###### 检测是否有指定值

与Set集合相似使用has()方法检测是否有指定值。

```
let map = new Map();
map.set('name','xiaoming');
console.log(map.has('name'));  //true
```

###### 获取集合长度

我们还使用size属性获取集合长度

```
let map = new Map();
map.set('name','xiaoming');
console.log(map.size);  //1
```

###### 删除指定项

同样使用delete()方法删除指定值。

```
let map = new Map();
map.set('name':'xiaoming');
map.delete('name');
conssole.log(map.has('name'));

```

###### 清空集合

也使用同样的clear()方法清空集合。

```
let map = new Map();
map.set('name', 'xiaoming');
map.clear('name');
console.log(map.size);     //0
```

###### forEach()方法

Map集合同样可以使用forEach()方法。

```
let map = new Map();
map.set('name', 'xiaoming');
map.set('id', 1);
map.forEach((value, key) => {
    console.log(key, value)     //name:xiaoming
                                //id:1
})
```

#### Weak Map

同样Weak Map是弱类型集合。也就是说在失去引用后会自动回收这个对象。

Weak Map集合最大的用处就是保存web页面的DOM元素。

```
let map = new WeakMap();
    element = document.querySelector('.element');
    
map.set(element,'this is .element');

console.log(map.get(element));  //this is .element

element.parentNode.removeChild(element);
element = null;
console.log(map.size);  //0
```

###### 与Map集合的不同

Weak Map集合不支持forEach()、size属性和clear()方法。如果非常需要这些方法特性，则使用Map集合更好。

同时如果使用非对象名作为键名，使用Map集合更好，如果使用对象名作为键名，则使用Weak Map集合更好

#### 总结

ES6中加入了Set和Map集合用于保存数据，上面着重讲了Set和Map的使用方法，我们的重点也应该放在这两种集合的使用上：

1. Set集合的使用和方法
2. Weak Set集合的使用和方法
3. Map集合的使用和方法
4. Weak Map集合的使用和方法

