下面是 ES6 的常用语法入门实例，通过实例来快速学习 ES6 语法；对 JavaScript 更全面的了解可以参考 Mozilla 提供的更详细的文档 [MDN web docs](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference) ，规范 [ ECMAScript 2015 (6th Edition, ECMA-262)](http://www.ecma-international.org/ecma-262/6.0/#sec-class-definitions)

[![MDN web docs](./assets/mdn-logo.svg)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference)

## 变量声明

#### const 和 let

ES6的新的代码模式不用 `var`声明变量，而用 `const` 和 `let`，分别表示常量和变量。
不同于 `var` 的函数作用域，`const` 和 `let` 都是块级作用域。
  
`var` 声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象；  
`let` 声明的变量，其作用域为该语句所在的代码块内，不存在变量提升；  
`const` 声明的是常量，在后面出现的代码中不能再修改该常量的值。  
  
```js
const DELAY = 1000;

let count = 0;
count = count + 1;
```


#### 模板字符串

模板字符串提供了另一种字符串拼接的方法，使用`${}`替换。  
`${}`中可以放   1.变量  2.表达式  3.函数  

```js
// 模板字符串之中镶入变量。
const user = 'world';
console.log(`hello ${user}`);  
// hello world

// 模板字符串之中进行运算
let x = 1;
let y = 2;
`${x} + ${y} = ${x + y}`
// "1 + 2 = 3"

// 模板字符串之中调用函数。
function fn(){
  return 'Hello world';
}
`foo ${fn()} bar` 
// foo Hello world bar

// 多行
const content = `
  Hello ${firstName},
  Thanks for ordering ${qty} tickets to ${event}.
`;

// 标签模版  
let a = 5;
let b = 10;

tag`Hello ${ a + b } world ${ a * b }`;
// 等同于
tag(['Hello ', ' world ', ''], 15, 50);
```

#### 默认参数  
     
ES6函数默认值比以前的写法优势在于：  
1. 代码简洁、易懂。    
2. 易于维护,函数内不用再次声明，即使函数内代码有删减这个参数，也不会报错。  
  
```js
//ES6之前写法
function logActivity(activity) {
  activity = activity || 'skiing';
  console.log(activity)
}
logActivity();  // skiing

// ES5写法缺点在于赋值为false，赋值就不起作用了。如上代码赋值为 '' 时，返回还是为默认值。
// 为了避免这个问题，通常需要先判断一下参数y是否被赋值，写法就繁琐了。
if(typeof activity === 'undefined') {
  y = 'skiing'
}
 
 // ES6写法就不存在以上问题
function logActivity(activity = 'skiing') {
  console.log(activity);
}

logActivity();   // skiing
logActivity(''); // undefined
```

 函数的 length 属性  
```js
 // 指定了默认值后，length属性将失真
(function (a, b, c = 5) {}).length //  2  
```
注意事项：
    
1. 参数变量是默认声明的，所以不能用`let`或`const`再次声明。  
2. 使用参数默认值时，函数不能有同名参数。  
3. 参数默认值不是传值的，而是每次都重新计算默认值表达式的值,参数默认值是惰性求值的。 

##  Arrow Function (箭头函数)

函数的快捷写法，不需要通过 `function` 关键字创建函数，并且还可以省略 `return` 关键字。

同时，箭头函数还会继承当前上下文的 `this` 关键字。

例如：

```js
// 简化回调函数
[1, 2, 3].map(x => x + 1);  // [2, 3, 4]
```

等同于：

```js
[1, 2, 3].map((function(x) {
  return x + 1;
}).bind(this));  // [2, 3, 4] 
```
  
注意事项:  

1. 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象,并且指向固定。  

```js
// 实例1
  
function foo() {
  setTimeout(() =>{
  console.log('id',this.id);
  },100); 
}
var id =21;
foo.call({id: 42}); 
// 42 
// this指向foo()函数内部
  
```
  
2. 箭头函数作为匿名函数,是不能作为构造函数的,不能使用new，否则会报错。
  
```js
// 实例2
const B = ()=>{
  value:1;
}
var b = new B(); //TypeError: B is not a constructor  
// this指向的固定,原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。所以也就不能用作构造函数。

```
  
3. 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 `rest` 参数代替。
  
```js
//实例3
//(argument) 是函数收到实参副本
function A(a){ console.log(arguments)}   // [object Arguments] {0,1}
const B = (b) =>{ console.log(arguments)}  // ReferenceError: arguments is not defined
// 正确写法
const c = (...c)=>{ // ...c 即为rest参数(没有给出名称的参数)
  console.log(c); 
}
  
```
  
4. 只有一个参数的函数可以省略括号()
  
```js
// 两个参数:
(x, y) => x * x + y * y

// 无参数:
() => 3.14

// 一个参数
x => x * x

// 可变参数:
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
```
## 模块的 Import 和 Export

`import` 用于引入模块，`export` 用于导出模块。  
`export`用于对外输出本模块（一个文件可以理解为一个模块）变量的接口。  
`import`用于在一个模块中加载另一个含有export接口的模块。  

引入非默认组件需要加`{}`,默认组件不需要。  
例如：

```js
// 引入全部 .
//导入‘react’文件里export的默认的组件
import React from 'react';

// 导入多个组件
import React, { PureComponent } from 'react';
// 附加小知识点：PureComponent也就是,要把继承类从 Component 换成 PureComponent,
// 减少不必要的 render操作的次数,从而提高性能

// 导入多个组件
// 组件名必须和组件里的组件名相同
import { Switch, Link, Route, Redirect } from 'react-router-dom';

// 引入'./services/github‘所有非默认组件，重新命名为 github 通过 import载入
import * as github from './services/github';

// 模块指定默认输出  
//(模块APP系统为其取默认名为default，自然当前文件里不能拥有多个export default)
export default App;
// 部分导出，需 import { App } from './file'; 引入
export class App extend Component {};
```

## ES6 对象和数组

#### 析构赋值
  
析构赋值让我们从 Object 或 Array 从数组和对象中提取值，对变量进行赋值。
  
```js
// 对象:对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
const user = { name: 'guanguan', age: 2 };
const { name, age } = user;
console.log(`${name} : ${age}`);  // guanguan : 2
```

```js
// 数组: 数组的元素是按次序排列的，变量的取值由它的位置决定。
const arr = [1, 2];
const [foo, bar] = arr;
console.log(foo);  // 1

let [head, ...tail] = [1, 2, 3, 4]; // 扩展运算符将一个数组，变为参数序列为一个数组序列的
console.log(head) // 1
console.log(tail) // [2, 3, 4],可以看到这里也是一个数组
```

我们也可以析构传入的函数参数。

```js
const add = (state, { payload }) => {
  return state.concat(payload);
};
```

析构时还可以配 alias，让代码更具有语义。

```js
const add = (state, { payload: todo }) => {
  return state.concat(todo);
};
```

#### 对象字面量改进

这是析构的反向操作，用于重新组织一个 Object 。

```js
const name = 'dog';
const age = 8;
const user = { name, age }; // 等同于 const user = {name:mame, age:age};
// { name: 'dog', age: 8 }
```

定义对象方法时，还可以省去 `function` 关键字。

```js
const obj = {
  user: {
    add() {}  // 等同于 add: function() {}
  },
  model: {
    *addRemote() {}  // 等同于 addRemote: function*() {}
  },
}
```

#### 扩展符号(Spread Operator)

`rest` 参数（形式为...变量名），作用类似`arguments`对象 ，参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

`rest`与`arguments`区别:  

arguments:  
只在函数内去作用指向调用者所有的参数，即使不定义也能获取它的值，常用于判断参数个数。  
rest:  
用于获取函数的其余参数，rest参数搭配的变量是一个数组，该变量将其余的参数放入数组中，主要用于函数调用。  

Spread Operator 即 3 个点 `...`，有几种不同的使用方法。

可用于组装数组。

```js
const todos = ['Learn dva'];
[...todos, 'Learn antd'];  // ['Learn dva', 'Learn antd']
```

也可用于获取数组的部分项。

```js
const arr = ['a', 'b', 'c'];
const [first, ...rest] = arr;
rest;  // ['b', 'c']

// With ignore
const [first, , ...rest] = arr;
rest;  // ['c']
```

还可收集函数参数为数组。

```js
function directions(first, ...rest) {
  console.log(rest);
}
directions('a', 'b', 'c');  // ['b', 'c'];
```

代替 apply。  
由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数了

```js
function foo(x, y, z) {}
const args = [1,2,3];

// 下面两句效果相同
foo.apply(null, args);
foo(...args);
```

对于 Object 而言，用于组合成新的 Object 。(ES2017 stage-2 proposal)

```js
const foo = {
  a: 1,
  b: 2,
};
const bar = {
  b: 3,
  c: 2,
};
const d = 4;

const ret = { ...foo, ...bar, d };  // { a:1, b:3, c:2, d:4 }
```

## 异步(Promises)


Promise 类似一个容器，这让异步方法可以像同步方法那样返回值.

相比传统的解决方法（回调函数和事件）优势在于：
避免了层层嵌套的回调函数。此外，Promise 对象提供统一的接口，使得控制异步操作更加容易

Promise对象有以下两个特点：  
1. Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。异步操作出来的结果来决定当前状态，其他任何操作都无法改变。

2. Promise对象的状态改变，只有两种可能：从`pending`变为`fulfilled`或者`rejected`。一旦状态改变，就不会再变，这时就称为 resolved（已定型）。如果改变已经发生了再向Promise对象添加回调函数，也能立即获得结果。

Promise 用于更优雅地处理异步请求。比如发起异步请求：

```js
fetch('/api/todos')
  .then(res => res.json())
  .then(data => ({ data }))
  .catch(err => ({ err }));
```

定义 Promise 。

```js
const delay = (timeout) => {
  return new Promise(resolve => {
    setTimeout(resolve, timeout);
  });
};
delay(1000).then(_ => {
  console.log('executed');
});
```


## 生成器函数(Generators)

生成器函数在执行时能暂停，后面又能从暂停处继续执行。

调用一个 `生成器函数` 并不会马上执行它里面的语句，而是返回一个这个生成器的`迭代器（iterator）`对象。当这个迭代器的 `next()` 方法被首次（后续）调用时，其内的语句会执行到第一个（后续）出现yield的位置为止，`yield` 后紧跟迭代器要返回的值。或者如果用的是 `yield*`（多了个星号），则表示将执行权移交给另一个生成器函数（当前生成器暂停执行）。

```js
function *gen(y){     //声明时需要添加*，普通函数内部不能使用yield关键字，否则会出错
  yield 10;
  y=yield 'foo';
  yield y;
}

var gen_obj=gen();
console.log(gen_obj.next());// 执行 yield 10，返回 10
console.log(gen_obj.next());// 执行 yield 'foo'，返回 'foo'
console.log(gen_obj.next(10));// 将 10 赋给上一条 yield 'foo' 的左值，即执行 y=10，返回 10
console.log(gen_obj.next());// 执行完毕，value 为 undefined，done 为 true
```

实例二

```js
function* quips(name) {
  yield "你好 " + name + "!";
  yield "希望你能喜欢这篇介绍ES6的译文";
  if (name.startsWith("X")) {
    yield "你的名字 " + name + "  首字母是X，这很酷！";
  }
  yield "我们下次再见！";
}
var iter = quips("jorendorff"); //调用函数后不会运行，而是返回指向函数内部状态的指针
iter.next() //=> { value: "你好 jorendorff!", done: false }  // 遇到yield暂停
iter.next() //=> { value: "希望你能喜欢这篇介绍ES6的译文", done: false }
iter.next() //=> { value: "我们下次再见！", done: false }
iter.next() //=> { value: undefined, done: true }
```
