# Promise

Promise的用处是改进JavaScript中的异步编程。它可以让更好的控制多个同步操作，相比以往的函数回调更加实用。

### Promise基础知识

Promise有三个声明周期阶段：进行中（pending）、操作成功（fulfilled）、操作失败（rejected）;

Promise构造函数只有一个参数，该参数是一个函数，成为执行器。执行器有两个参数，分别是resolve()和reject(),分别表示成功的回调和失败的回调。

##### then()

而我们检测Promise的状态需要通过then()方法，then()方法可以接受两个参数：1.Promise状态为fulfilled时调用的函数；2.Promise状态为rejected时调用的函数。

这两个参数都是可选的，我们可以根据情况选择Promise是否响应fulfilled状态或者rejected状态。

```JavaScript
let pro = readFile('example.tex');
pro.then(null, function (a) {
  console.log('失败');    //只响应fulfilled状态
})
pro.then(function () {
  console.log('成功') //只响应rejected状态
}, null)
```


##### catch()

catch()方法只能接受拒绝处理程序

```JavaScript
let pro = readFile('example.tex');
pro.then(null, function (err) {
  console.log(err)
})
//在then()方法中只处理rejected状态，相当于catch()方法
pro.catch(function (err) {
  console.log(err)
})
```

更加建议then()和catch()一起使用，可以更好的指明Promise()的状态。


#### 串联Promise

我们可以通过将Promise串联起来实现更加复杂的异步特性方法。

每次调用then()或者catch()方法时，实际上创建并返回了另一个Promise，
只有当第一个Promise完成或者被拒绝后，后一个Promise才会被解决。

```JavaScript
let a = new Promise(function(resolve,reject){
  resolve('123');
})
a.then(function (err) {
  console.log(err)
}).then(function(){
  console.log('234')
})
//123
//234
```

a.then()返回了新的Promise，接着调用了then()方法。只有当第一个Promise解决之后才会执行第二个Promise程序。

#### 多个Promise

如果希望响应多个Promise，我们可以使用ES6提供的方法来监听。

##### Promise.all()

Promise.all()同样只接受一个参数并返回一个Promise。参数时一个可以迭代的对象。Promise.all()表示只有当参数对象所有的Promise都解决后，返回的Promise才被完成，只要有一个被拒绝，那么返回的Promise接回被立刻拒绝

```JavaScript
Promise.all([
  new Promise(function (resolve, reject) {
    resolve(1)
  }),
  new Promise(function (resolve, reject) {
    resolve(2)
  }),
  new Promise(function (resolve, reject) {
    resolve(3)
  })
]).then(arr => {
  console.log(arr) // [1, 2, 3]
})
```

##### Promise.race()

Promise.race()同样接受一个可迭代参数，但是只要有一个Promise解决，就立刻返回Promise为成功状态。

```JavaScript
Promise.race([
  new Promise(function(resolve, reject) {
    setTimeout(() => resolve(1), 1000)
  }),
  new Promise(function(resolve, reject) {
    setTimeout(() => resolve(2), 100)
  }),
  new Promise(function(resolve, reject) {
    setTimeout(() => resolve(3), 10)
  })
]).then(value => {
  console.log(value) // 3
})
```




