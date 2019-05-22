[TypeScript](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md#31-the-any-type)

# 公共，私有与受保护的修饰符

1. 默认为 public
2. private 私有的
> 当成员被标记成 private时，它就不能在声明它的类的外部访问。比如：
```js
class Animal {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}

new Animal("Cat").name; // 错误: 'name' 是私有的.
```
3. protected修饰符 与 private修饰符的行为很相似，但有一点不同， protected成员在派生类中仍然可以访问。
4. readonly修饰符
> 你可以使用 readonly关键字将属性设置为只读的。 只读属性必须在声明时或构造函数里被初始化。

```js
class Octopus {
    readonly name: string;
    readonly numberOfLegs: number = 8;
    constructor (theName: string) {
        this.name = theName;
    }
}
let dad = new Octopus("Man with the 8 strong legs");
dad.name = "Man with the 3-piece suit"; // 错误! name 是只读的.
```
# interface

- 我们也可以使用 interface 定义我们的复杂类型，在 TS 中我们也可以直接定义 interface：  可以继承
```js
interface Application {
    init(): void
    get(key: string): object
}
```

# declare

- declare 可以创建 *.d.ts 文件中的变量，declare 只能作用域最外层：

```js
declare var foo: number;
declare function greet(greeting: string): void;
declare namespace tasaid {
    interface blog {// 这里不能 declare
        website: 'http://tasaid.com'
    } 
}
```

# namespace 命名空间

- 为防止类型重复，使用 namespace 用于划分区域块，分离重复的类型，顶层的 namespace 需要 declare 输出到外部环境，子命名空间不需要 declare。

```js
declare namespace Models {// 命名空间
    type A = number
    // 子命名空间
    namespace Config {
        type A = object
        type B = string
    }
}
type C = Models.Config.A
```


# SFC类型

- 使用 SFC 进行无状态组件开发。
> 在 React 的声明文件中 已经定义了一个 SFC 类型，使用这个类型可以避免我们重复定义 children、 propTypes、 contextTypes、 defaultProps、displayName 的类型。

```js 
import { SFC } from 'react'
import { MouseEvent } from 'react'
import * as React from 'react'
interface IProps {
  onClick (event: MouseEvent<HTMLDivElement>): void,
}
const Button: SFC<IProps> = ({onClick, children}) => {
  return (
    <div onClick={onClick}>
      { children }
    </div>
  )
}
export default Button
```


# 数据类型

```js

let isDone: boolean = false;  // 布尔值
let decLiteral: number = 6;   // 数字
let name: string = "bob"; // 字符串
let notSure: any = 4;
let list: number[] = [1, 2, 3];  //   第一种，表示由此类型元素组成的一个数组：
let list: any[] = [1, true, "free"];
let list: Array<number> = [1, 2, 3]; // 第二种方式是使用数组泛型，Array<元素类型>：
let list: Array<any> = [1, 2, 3];

```

### 元组 Tuple

```js
let x: [string, number];
x = ['hello', 10]; // OK
x = [10, 'hello']; // Error
```

### 枚举 enum

```js
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
console.log(c); // 1
enum Color {Red = 1, Green, Blue=4} // 手动的指定成员的数值。

enum Color { Red = 1, Green, Blue }
let colorName: string = Color[2];
console.log(colorName); // Green
```

### Void

- 某种程度上来说，void类型像是与any类型相反，它表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 void：
```js
function warnUser(): void {
    console.log("This is my warning message");
}
```
- 声明一个void类型的变量没有什么大用，因为你只能为它赋予undefined和null：

### Null 和 Undefined

- TypeScript里，undefined和null两者各自有自己的类型分别叫做undefined和null。 和 void相似，它们的本身的类型用处不是很大：

### Never

- never类型表示的是那些永不存在的值的类型。 例如， never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是 never类型，当它们被永不为真的类型保护所约束时。

```js
function error(message: string): never {    // 返回never的函数必须存在无法达到的终点
    throw new Error(message);
}
function fail() {                           // 推断的返回值类型为never
    return error("Something failed");
}
function infiniteLoop(): never {            // 返回never的函数必须存在无法达到的终点
    while (true) {    }
}
```

### Object
- object表示非原始类型，也就是除number，string，boolean，symbol，null或undefined之外的类型。
> 使用object类型，就可以更好的表示像Object.create这样的API。例如：
```js
declare function create(o: object | null): void;
create({ prop: 0 }); // OK
create(null); // OK
create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```

### 类型断言
- 有时候你会遇到这样的情况，你会比TypeScript更了解某个值的详细信息。 通常这会发生在你清楚地知道一个实体具有比它现有类型更确切的类型。
> 通过类型断言这种方式可以告诉编译器，“相信我，我知道自己在干什么”。 类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。 它没有运行时的影响，只是在编译阶段起作用。 TypeScript会假设你，程序员，已经进行了必须的检查。

```js
let someValue: any = "this is a string";

let strLength: number = (\<string>someValue).length; // 其一是“尖括号”语法：
let strLength: number = (someValue as string).length; // 另一个为as语法：

```

# 接口

- 介绍
> TypeScript的核心原则之一是对值所具有的结构进行类型检查。 它有时被称做***“鸭式辨型法”***或***“结构性子类型化”***。 在TypeScript里，**接口**的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

### 可选属性

```js
interface LabelledValue { // 称为接口
  label: string;
  white?: number;   // 加问号  代表这个不是必须的
  [propName: string]: any; // 额外的属性检查 表示的是LabelledValue可以有任意数量的属性
}
function printLabel(labelledObj: LabelledValue):void {
  console.log(labelledObj.label);
}
let myObj = { size: 10, label: "Size 10 Object" }; // 不推荐 不能绕过检查
printLabel(myObj);  // 如果直接把myobj的对象写进函数  会报错  size没有在LabelledValue存在
printLabel({ size: 10, label: "Size 10 Object" } as LabelledValue); // 额外的属性检查 或者使用类型断言
```

### 只读属性
- 一些对象属性只能在对象刚刚创建的时候修改其值。 你可以在属性名前用 readonly来指定只读属性:

```js
interface Point {
    readonly x: number;
    readonly y: number;
}
let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!
```

- TypeScript具有ReadonlyArray<T>类型，它与Array<T>相似，只是把所有可变方法去掉了，因此可以确保数组创建后再也不能被修改：
```js
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error!
```

### 函数类型

- 接口能够描述JavaScript中对象拥有的各种各样的外形。 除了描述带有属性的普通对象外，接口也可以描述函数类型。
> 为了使用接口表示函数类型，我们需要给接口定义一个调用签名。 它就像是一个只有参数列表和返回值类型的函数定义。参数列表里的每个参数都需要名字和类型。
```js 
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(src: string, sb: string) : boolean{
  let result = src.search(sb);
  return result > -1;
}
console.log(mySearch("123", "1")); //  函数类型的检测 true
```
- 对于函数类型的类型检查来说，函数的参数名不需要与接口里定义的名字相匹配。

# 类类型 实现接口

- 可以在接口中描述一个方法，在类里实现它，如同下面的setTime方法一样：
```js
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date);
}
class Clock implements ClockInterface {
    currentTime: Date;
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```
............
# 继承接口
- 和类一样，接口也可以相互继承。 这让我们能够从一个接口里复制成员到另一个接口里，可以更灵活地将接口分割到可重用的模块里。
```js
interface Shape {
    color: string;
}

interface Square extends Shape {
    sideLength: number;
}

let square = <Square>{};
square.color = "blue";
square.sideLength = 10
```


# 存取器
- TypeScript支持通过getters/setters来截取对对象成员的访问。 它能帮助你有效的控制对对象成员的访问。

```js
let passcode = "secret passcode";

class Employee {
    private _fullName: string;
    get fullName(): string { return this._fullName }
    set fullName(newName: string) {
        if (passcode && passcode == "secret passcode") {
            this._fullName = newName;
        }else {
            console.log("Error: Unauthorized update of employee!");
        }
    }
}
let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    alert(employee.fullName);
}
```
- 首先，存取器要求你将编译器设置为输出ECMAScript 5或更高。 不支持降级到ECMAScript 3。 其次，只带有 get不带有 set的存取器自动被推断为 readonly。 这在从代码生成 .d.ts文件时是有帮助的，因为利用这个属性的用户会看到不允许够改变它的值。


# 静态属性

- 我们使用 static定义 origin，因为它是所有网格都会用到的属性。 每个实例想要访问这个属性的时候，都要在 origin前面加上类名。 如同在实例属性上使用 this.前缀来访问属性一样，这里我们使用 Grid.来访问静态属性。

```js
class Grid {
    static origin = {x: 0, y: 0};
    calculateDistanceFromOrigin(point: {x: number; y: number;}) {
        let xDist = (point.x - Grid.origin.x);
        let yDist = (point.y - Grid.origin.y);
        return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
    }
    constructor (public scale: number) { }
}
let grid1 = new Grid(1.0);  // 1x scale
let grid2 = new Grid(5.0);  // 5x scale
console.log(grid1.calculateDistanceFromOrigin({x: 10, y: 10}));
console.log(grid2.calculateDistanceFromOrigin({x: 10, y: 10}));
```

# 抽象类

- 抽象类做为其它派生类的基类使用。 它们一般不会直接被实例化。 不同于接口，抽象类可以包含成员的实现细节。 abstract关键字是用于定义抽象类和在抽象类内部定义抽象方法。
> 抽象方法必须包含 abstract关键字并且可以包含访问修饰符。
```js
    abstract class Department {
      constructor(public name: string) {
      }
      printName(): void {
        console.log('Department name: ' + this.name);
      }
      abstract printMeeting(): void; // 必须在派生类中实现
    }
    class AccountingDepartment extends Department {
      constructor() {
        super('Accounting and Auditing'); // 在派生类的构造函数中必须调用 super()
      }
      printMeeting(): void {
        console.log('The Accounting Department meets each Monday at 10am.');
      }
      generateReports(): void {
        console.log('Generating accounting reports...');
      }
    }
    let department: Department; // 允许创建一个对抽象类型的引用  意思是 Department类的实例的类型是 Department
    // department = new Department(); // 错误: 不能创建一个抽象类的实例
    department = new AccountingDepartment(); // 允许对一个抽象子类进行实例化和赋值
    department.printName()
    department.printMeeting();
    // department.generateReports(); // 错误: 方法在声明的抽象类中不存在
```

### 书写完整函数类型

```js
function add(x: number, y: number): number {
    return x + y;
}
//完整类型。
//函数类型包含两部分：参数类型和返回值类型。  我们以参数列表的形式写出参数类型，为每个参数指定一个名字和类型。名字x,y只是为了增加可读性。
let myAdd: (x: number, y: number) => number = function(x: number, y: number): number { return x + y; };
// 推断类型 TypeScript编译器会自动识别出类型
let myAdd: (baseValue: number, increment: number) => number = function(x, y) { return x + y; };
let myAdd = function(x: number, y: number): number { return x + y; };
```

### 函数的可选参数

```js
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}
```

### 函数的默认参数

```js
function buildName(firstName: string, lastName = "Smith") {
   return firstName + " " + lastName;
}
```

###  剩余参数

```js
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}

let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");

```

# 泛型之Hello World  范型函数

- 使用了 类型变量，它是一种特殊的变量，只用于表示类型而不是值。
```js
//使用any类型会导致这个函数可以接收任何类型的arg参数，这样就丢失了一些信息：传入的类型与返回的类型应该是相同的。
//如果我们传入一个数字，我们只知道任何类型的值都有可能被返回。
function identity(arg: any): any {
    return arg;
}
//我们给identity添加了类型变量T。 T帮助我们捕获用户传入的类型（比如：number），之后我们就可以使用这个类型。 之后我们再次使用了 T当做返回值类型。
function identity<T>(arg: T): T {
    return arg;
}

let output = identity<string>("myString");  // type of output will be 'string'
//----------------------------- -->
function loggingIdentity<T>(arg: T): T {
    console.log(arg.length);  // Error: T doesn't have .length
    return arg;
}
function loggingIdentity<T>(arg: T[]): T[] {
    console.log(arg.length);  // Array has a .length, so no more error
    return arg;
}
```

# 范型类型

```js
function identity<T>(arg: T): T {
    return arg;
}
let myIdentity: <T>(arg: T) => T = identity;
//我们也可以使用不同的泛型参数名，只要在数量上和使用方式上能对应上就可以。
let myIdentity: <U>(arg: U) => U = identity;
// 带有调用签名的对象字面量来定义泛型函数：
let myIdentity: {<T>(arg: T): T} = identity;
```

# 范型接口

```js
interface GenericIdentityFn {
    <T>(arg: T): T;
}

function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: GenericIdentityFn = identity;
```

# 泛型类
- 泛型类看上去与泛型接口差不多。 泛型类使用（ <>）括起泛型类型，跟在类名后面。
```js
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };
```

# 范型约束

```js
interface Lengthwise {
    length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);  // Now we know it has a .length property, so no more error
    return arg;
}
loggingIdentity(3);  // Error, number doesn't have a .length property
loggingIdentity({length: 10, value: 3}); //10
loggingIdentity([1, 2, 3]); //3
```

# 数字枚举

```js
enum Direction {
    Up = 1,
    Down,
    Left,
    Right
}
// Up使用初始化为 1。 其余的成员会从 1开始自动增长。 Down为 2， Left为 3， Right为 4。
// 不使用初始化器： Up的值为 0， Down的值为 1
```
# 类型兼容
```js
let x = (a: number) => 0;
let y = (b: number, s: string) => 0;
y = x; // OK
x = y; // Errorx的每个参数必须能在y里找到对应类型的参数
// ------------------------------------
// TypeScript结构化类型系统的基本规则是，如果x要兼容y，那么y至少具有与x相同的属性。比如：
interface Named {
    name: string;
}
let x: Named;
// y's inferred type is { name: string; location: string; }
let y = { name: 'Alice', location: 'Seattle' };
x = y;  // ok
```
