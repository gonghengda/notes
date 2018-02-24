
在 JavaScript 中`this`总是指向调用它所在方法的对象。因为this是在函数运行时，自动生成的一个内部对象，只能在函数内部使用。

1. 全局的函数调用

```js
var name = "Ane";

function globalTest() {
  console.log(this.name);
}

globalTest(); // Ane
```

```js
var name = "Ane";

function globalTest() {
  this.name = "new Ane"
  console.log(this.name);
}

globalTest(); //new Ane
```

从中可以看出：对于全局的方法调用，this 指向的是全局对象 window，即调用方法所在的对象。

2. 对象方法的调用

如果函数作为对象的方法调用，this 指向这个上级对象，即调用方法的对象
```js
function showName() {
   console.log(this.name);
}

var obj = {};
obj.name = "安能";
obj.show = showName;
obj.show(); // 安能
```

该方法中，this 指向对象 obj

3. 构造函数的调用

**构造函数中的this指向新创建的对象本身。**

```js
var name = "Ane name";

function showName() {
  this.name = "showName function";
}

var obj = new showName();

console.log(obj.name); // showName function
console.log(name);     // Ane name
```

我们通过 new 关键字创建一个对象，this 的指向就从 global 变成了 obj。  
在构造函数的内部，我们对 this.name 进行赋值，但并没有改变全局变量name。

4. call 和 apply 方法中的 this 指向问题

**call方法**

调用一个对象的方法，用另一个对象替换当前对象。

```js
var name = "Ane";
function ftn(name){
  console.log(name);
  console.log(this.name);
  console.log(this);
}
ftn("姓名");
// 姓名
// Ane
// window

var obj = {
  name:"名字"
};
ftn.call(obj,"安能");
// 安能
// 名字
// { name="名字"}
```

```js
function add(a, b) {
  alert(a + b);
}

function sub(a, b) {
  alert(a - b);
}

add.call(sub, 3, 1); // 4
```

这里就是调用对象 add 的方法，并用 add 对象替换当前对象 sub；

**apply方法**

调用函数，并用指定对象替换函数的 this 值
```js
function ane(a, b){
 return alert(a + b);
}
 
function ane_1(a, b){
    ane.apply(ane_1, [a, b]);
}
 
 
ane_1(1,2); // 3
```

这里调用函数 ane，并用指定的对象 ane_1 替换 ane 函数的 this 值。

5. ES6中箭头函数的this指向问题

在 ES6 的箭头函数中，箭头函数没有自己的 this，导致内部的this就是外层代码块的this，所以不能用作构造函数，也不能用 `call()`、`apply()`、`bind()` 这些方法去改变this的指向。  
但this指向是固定的，因为箭头函数导致this总是指向函数定义生效时所在的对象。

```js
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 });   // 输出 id: 42
```

这个箭头函数的定义生效是在 foo 函数生成时，而它的真正执行要等到100毫秒后。

6. Component内部的this  

只要不采用function定义函数，Component 所有方法内部的this对象始终指向该类自身。  

初始化数据：

```js
constructor(props) {
  super(props)
  this.state = {
    dataSource: props.dataSource || [],
    queryHouseData: [],
    visible:false
  }
}
```

存入和改变数据：

```js
this.setState({queryHouseData:json.data,visible:true})
```

调取数据：

```js
this.state.queryHouseData
this.state.visible
```

