
JavaScript对于不同的操作对象有着不同的方法。
## JavaScript常用的操作对象

常用操作对象有：Array、String、Math、Date

### Array 常用方法

1. `pop` : 删除数组最后一位元素
2. `shift` : 删除数组第一位元素
3. `push` : 往数组的末尾新增一个或多个元素
4. `unshift` : 往数组的开头新增一个或多个元素
5. `reverse` : 把数组元素顺序逆转
6. `sort` : 数组排序
7. `splice` : 给数组添加或者删除元素
8. `forEach` : 遍历数组
9. `filter` : 从数组中找出所有符合指定条件的元素
10. `every` : 数组中是否每个元素都满足指定的条件
11. `some` : 数组中是否有元素满足指定的条件
12. `map` : 将数组映射成另一个数组
13. `reduce` : 将数组合成一个值
14. `isArray` : 是否是数组
15. `concat` : 合并数组或合并数组的值
16. `join` : 合并数组所有元素拼接成字符串
17. `slice` : 选择数组中的一部分元素
18. `indexOf` : 查找数组中指定元素的下标
19. `lastIndexOf` : 查找数组中指定元素的下标。查找方向为从后往前

示例：

*修改数组*

1. array.pop 删除数组最后一位元素

```js
var arr = [1, 2, 3];
arr.pop();    // 返回 3
arr;          // [1,2]
```

2. array.shift 删除数组第一位元素

```js
var arr = [1, 2, 3];
arr.shift();  // 返回 1
arr;          // [2,3]
```

3. array.push 往数组的末尾新增一个或多个元素

```js
var arr = [];
arr.push(1);  // 返回数组长度 1
arr;          // [1]
arr.push(2,3);
arr;          // [1,2,3]
```

4. array.unshift 往数组的开头新增一个或多个元素

```js
var arr = [1, 2, 3];
arr.unshift(0);
arr.unshift(-1, -2);
arr;          // [-1, -2, 0, 1, 2]
```

5. array.reverse 把数组元素顺序逆转

```js
var arr = [1, 2, 3];
arr.reverse();// [3, 2, 1]
arr;          // [3, 2, 1]
```

6. array.sort 数组排序

```js
var arr = [1 ,-1, 2];
arr.sort();   // [-1, 1, 2]
arr;          // [-1, 1, 2]
```

```js
arr = [{
    age: 10,
},{
    age: 1
}, {
    age: 12
}];
arr.sort(function(a, b){        // 按照 age 从小到大排序
    return a.age - b.age > 0 ? 1 : -1;
}); 
```

7. array.splice 给数组添加或者删除元素

splice(开始下标, 删除个数，插入元素(可以多个)）

```js
var arr = [1, 2, 3, 4];
arr.splice(1, 2);               // [2,3]
arr;                            // [1,4]
arr = [1, 2, 3, 4];
arr.splice(1, 2, 'a', 'b', 'c');// [2,3]
arr;                            // [1, "a", "b", "c", 4]
```

*迭代方法*

8. array.forEach 遍历数组

```js
['a' ,'b' ,'c'].forEach(function(each, index){
    console.log(each,index);    // 输出 'a' 0  'b' 1 'c' 2
});
```

9. array.filter 从数组中找出所有符合指定条件的元素

```js
var res = [3, 4, -1].filter(function(each){ // 找出所有正数
    return each > 0;
});
res;                                        // [3,4]
```

10. array.every 数组中是否每个元素都满足指定的条件

```js
var isAllPositive = [3, 4, -1].every(function(each){
    return each > 0;
});
isAllPositive;
```

11. array.some 数组中是否有元素满足指定的条件

```js
var isSomePositive = [3, 4, -1].some(function(each){
    return each > 0;                        // 是否有正数
});
isSomePositive;                             // true;

isSomePositive = [-3, -4].every(function(each){
    return each > 0;
});
isSomePositive;                             // false;
```

12. array.map 将数组映射成另一个数组

```js
[1, 2, 3].map(function(each){
    return each * 2;                        // 返回 [2, 4, 6]
});
```

13. array.reduce 将数组合成一个值

```js
[1, 2, 3].reduce(function(prev, each){      // 数组内容求和。0 为初始值
    return prev + each;                     // 返回 6
}, 0);
```

**其它方法**

14. Array.isArray 是否是数组

```js
Array.isArray(3);     // false
Array.isArray({});    // false
Array.isArray([]);    // true
```

15. array.concat 合并数组或合并数组的值

```js
[1,2,3].concat(4,5);  // 输出 [1, 2, 3, 4, 5]
```

16. array.join 合并数组所有元素拼接成字符串

```js
[1,2,3].join();       // 输出 '1,2,3'
[1,2,3].join('@');    // 输出 '1@2@3'
```

17. array.slice 选择数组中的一部分元素

slice(开始下标, 结束下标（可选，默认为数组长度）)

```js
['a', 'b', 'c', 'd'].slice(1);      // ["b", "c", "d"]
['a', 'b', 'c', 'd'].slice(1, 2);   // ["b"]
['a', 'b', 'c', 'd'].slice(1, 3);   // ["b", "c"]
```

18. array.indexOf 查找数组中指定元素的下标

```js
['a', 'b', 'c', 'd'].indexOf('c');  // 2
['a', 'b', 'c', 'd'].indexOf('g');  // -1
```

19. array.lastIndexOf 查找数组中指定元素的下标。查找方向为从后往前

```js
['c', 'd', 'c'].lastIndexOf('c');       // 2
['a', 'b', 'c', 'd'].lastIndexOf('g');  // -1
```
### String 常用方法

1. `typeof` : 类型判断
2. `indeOf` : 查询字符串中是否包含指定子字符串
3. `length` : 返回数组长度
4. `charAt(下标)` : 取字符串中指定下标的字符
5. `substring(开始下标, 结束下标)` : 取字符串中指定范围的子字符
6. `substr(开始下标, 长度)` : 取字符串中指定范围的子字符
7. `replace` : 将字符串中的部分内容替换
8. `toUpperCase/toLowerCase` : 将字符串变成大/小写
9. `trim` : 去除字符串两头的空格(包括 space, Tab 等)
10. `split` : 将字符串分割成数组

示例：

**获取字符串信息**

1. typeof 类型判断

```js
typeof 'abc' === 'string';  // 返回 true
typeof {} === 'string';     // 返回 false
typeof 123 === 'string';    // 返回 false
```

2. indeOf 查询字符串中是否包含指定子字符串

```js
var str = 'abcde';
str.indexOf('b');           // 返回 1
str.indexOf('cd');          // 返回 2
str.indexOf('###');         // 返回 -1
```
若存在，则返回子字符串在字符串中的下标，否则返回 -1

3. length 返回数组长度

```js
var str = 'abcde';
str.length;                 // 返回 5
```

4. charAt(下标) 取字符串中指定下标的字符

```js
var str = 'abc';
str.charAt(1);              // 返回 'b'
str[1];                     // 返回 'b'
str.charAt(4);              // 返回 ''
str.charAt(-1);             // 返回 ''
```

5. substring(开始下标, 结束下标) 取字符串中指定范围的子字符

```js
var str = 'abcde';
str.substring(1);           // 返回 'bcde'
str.substring(1,3);         // 'bc'
str.substring(0,3);         // 'abc'
```

6. substr(开始下标, 长度) 取字符串中指定范围的子字符

```js
var str = 'abcde';
str.substr(1);              // 返回 'bcde'
str.substr(1,3);            // 返回 'bcd'
str.substr(0,3);            // 返回 'abc'
```

**字符串变换**

7. replace 将字符串中的部分内容替换

```js
var str = 'My name is Lucy';
str.replace('Lucy', 'Joel'); // 返回 'My name is Joel'
str;                         // 返回 'My name is Lucy'
```

8. toUpperCase/toLowerCase 将字符串变成大/小写

```js
var str = 'aBc1';
str.toUpperCase();          // 返回 'ABC1'
str.toLowerCase();          // 返回 'abc1'
str;                        // 返回 'aBc1'
```

9. trim 去除字符串两头的空格(包括 space, Tab 等)

```js
var str = '   abc   ';
str.trim();                 // 返回 'abc'
str;                        // 返回 '   abc   '
```

10. split 将字符串分割成数组

```js
var str = 'abc';
str.split('');              // 返回 ['a', 'b', 'c']
str;                        // 'abc'
str = 'a&b&c';
str.split('&');             // 返回 ['a', 'b', 'c']
str = 'a334b344c';
str.split(/\d+/);           // 返回 ['a', 'b', 'c']
```
### Math 常用方法

1. `Math.max()` : 最大值
2. `Math.min()` :  最小值
3. `Math.ceil()` : 向上取整
4. `Math.floor()` : 向下取整
5. `Math.round()` : 四舍五入
6. `Math.random()` : 获取一个属于[0,1)的随机数
7. `Math.abs(num)` : 是返回num的绝对值
87. `toFixed()` : 将数值格式化为字符串
98. `parseInt()` : 返回整型的数字
10. `parseFloat()` : 将字符串转为数字，返回浮点型的数字
11. `Number()` : 函数把对象转换为数字

示例：

1. Math.max()和Math.min(); 最大值和最小值

常用于避免多余循环和在if语句中确定一组数的最值

```js
var max = Math.max(3,54,32,16);
console.log(max);   // 54

var min = Math.min(3,54,32,16);
console.log(min);   // 3
```

也可以使用

```js
var values = [1,2,3,4,5,6,7,8];
var max = Math.max.apply(Math,values);
```

2. 舍入方法

Math.ceil()是向上取整；  
Math.floor()是向下取整；  
Math.round()是数学课上的正常的四舍五入。  

```js
Math.ceil(1.1);     // 2
Math.floor(25.9)    // 25
Math.round(25.1)    // 25
Math.round(25.9)    // 26
```

**注意**：Math.round(-num.5)的结果为-num

3. Math.random() 获取一个属于[0,1)的随机数

```js
var num = Math.random();
```

4. Math.abs(num)是返回num的绝对值

```js
Math.abs(-10);      // 10
```

*数值类型转换的方法*

5. toFixed() 将数值格式化为字符串

```js
var num = 10.005;
console.log(num.toFixed(2));    // "10.01"
```

6. parseInt() 返回整型的数字

```js
parseInt(string,radix)
console.log(parseInt("25"));    // 返回25
console.log(parseInt("11",2));  // 参数是2进制，返回十进制结果，返回3
console.log(parseInt("8M"));    // 参数首字符是数字，但后面的是字符，返回8
console.log(parseInt("M8"));    // 返回NaN
```

radix表示string参数中数字的进制，默认是十进制，取值范围为2~32

7. parseFloat() 将字符串转为数字，返回浮点型的数字

```js
console.log(parseFloat("r25.33M22"));   // NaN
console.log(parseFloat("25.33M22"));    // 25.33
```

8. Number()函数把对象转换为数字

```js
var date = new Date();
console.log(Number(date));  // 1515736559035
var str = new String("999 888"); 
console.log(Number(str));   // NaN
Number('100.1')             // 100.1
Number('12.4b5')            // NaN
Number('www')               // NaN
```
### Date 常用方法

操作 Date 的常用方法

1. `new Date()` : 获取时间
2. `get` : 获取年月日时分秒的单独一个
3. `set` : 设置数值，跟 get 用法类似
4. `getTime` : 时间转毫秒数

示例：

1. new Date() 获取时间

```js
var date = new Date();                // 获取当前时间
console.log(date);                    // Fri Jan 12 2018 14:03:29 GMT+0800 (CST)
var date = new Date(2018,1,13,14,52); // 获取指定时间
console.log(date);                    // Mon Feb 13 2018 14:52:00 GMT+0800 (CST)
```

2. get 获取年月日时分秒的单独一个

```js
var date = new Date(2018,1,13,14,57,18)

date.getFullYear();   // 2018
date.getMonth();      // 1
date.getDate();       // 13
date.getHours();      // 14
date.getMinutes();    // 57
date.getSeconds();    // 18
```

3. set 设置数值，跟 get 用法类似

```js
var date = new Date(2018,1,13,14,57,18)
date.setFullYear(2046);       // 年份变为2046
...
```

4. getTime 时间转毫秒数

```js
var date = new Date(2018,1,3,12,12,12);
console.log(date.getTime());  // 1517631132000
```
