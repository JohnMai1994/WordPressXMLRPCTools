---
title: JavaScript基础小结（一）
tags:
- 总结
categories:
- JS
---

## 中文版
#### 一. 基本知识

> JavaScript是运行在浏览器，不是在服务器上，用于实现页面交互效果，美化，不能操作数据库
> Node.js是用于JavaScript开发的，现在也可以基于Node技术进行服务器端编程

##### JavaScript的基础组成

- **ECSMA**: JavaScript的语法标准。包括变量，表达式，运算符，函数，if语句，for语句等
- **DOM**: Document Object Model(文档对象模型), 操作页面上的元素的API。 比如让盒子移动，变色，改变大小，轮播图等
- **BOM**: Browser Object Model(浏览器对象模型), 通过BOM可以操作浏览器窗口，比如弹框，控制浏览器跳转，获取浏览器分辨率等等

##### JavaScript的特点
1. **解释型语言**: 
> - 不需要被编译，而是可以直接执行，
> - 开发快，但是运行较慢
2. **单线程**
3. **ECMAScript标准**
> ECMAScript是**ECMA制定和发布的脚本语言规范**
> 规定了JS的**编程语法和基础核心知识**
> ECMAScript6 (ES6), 2015年6月发布，能力更强（更多新特性）

##### 编程语言的分类

- **翻译器**
计算机不能直接理解任何除计算机语言以外的的语言，所以必须要把程序员所编写的语言翻译成机器语言

> 计算机能读懂的语言：汇编语言

- **编译型语言**:
    - 定义：实现把所有的代码一次性翻译和，然后整体执行
    - 优点：运行更快
    - 缺点：不能跨平台，移植性不好
    - 编译型语言：C, C++

- **解释型语言**：
    - 定义：边翻译边执行（翻译一行，执行一行），不需要事先一次性翻译
    - 优点：移植性好，跨平台
    - 缺点：运行慢
    - 解释型语言：JavaScript, php, python

- **Java语言**
    - 既不是编译型语言，也不是解释型语言
    - 编译：`.java`代码需要先编译成`.class`
    - 执行：`.class`文件再通过jvm虚拟机，解释执行，有了JVM虚拟机，才可以让java跨平台执行



#### 二. 变量

##### 什么是变量
> 用于存放数据的容器。我们通过`变量名`获取数据，甚至修改数据
> 变量的本质：内存中申请一块用于存储数据的空间，变量名存储指向这个存储数据空间的指针

##### 变量的声明和赋值
> ES5: 使用var来声明一个变量
> ES6: 使用cons和let来声明一个变量，const来定义常量，let来定义一个变量

##### 标识符，关键字，保留字
- 标识符(Identifier)：变量名、函数名、属性名、参数名都是属于标识符

- 关键字：JS 本身已经使用了的单词，我们不能再用它们充当变量、函数名等标识符。

- 保留字：实际上就是预留的“关键字”。意思是现在虽然还不是关键字，但是未来可能会成为关键字

##### 变量的数据类型

- 基本数据类型（值类型）：String 字符串、Number 数值、Boolean 布尔值、Null 空值、Undefined 未定义。
> **直接保存**在栈内存中。值与值之间是独立存在，修改一个变量不会影响其他的变量

- 引用数据类型（引用类型）：Object对象
> 内置对象如Function, Array, Date, RegExp, Error等都是Object类型

> 创建一个新的对象，就会在堆内存中开辟出一个新的空间；变量保存了对象的内存地址（对象的引用）


##### Null和Undefined的区别
- **null**： 专门用来定义一个空对象，它的类型是object
- **undefined**：变量以声明，但是没有赋值，它的类型是undefined

当使用==比较时：null == undefined return true
当使用===比较时：null == undefined return false

##### typeof的代码结果
| typeof的代码写法 | 返回结果 |
| -- | -- |
| typeof 数字 | number |
| typeof 字符串 | string |
| typeof 布尔型 | boolean |
| typeof 对象 | object |
| typeof 方法 | function |
| typeof null | object |
| typeof undefined | undefined |
| typeof NaN | number |

> 备注 1：为啥 typeof null的返回值也是 object 呢？因为 null 代表的是空对象。
备注 2：typeof NaN的返回值是 number, NaN 是一个特殊的数字。

##### 什么是显式类型转换和隐式类型转换
显式：toString(), String(), Number(), parseInt(String), parseFloat(String), Boolean()
隐式：isNaN(), `++, --`, 字符串拼接 


##### 什么是对象
> 对象是一组**无序**的相关属性的方法的集合，由若干个”键值对“(key-value)构成
> 用于封装信息
> 具有**特征**（属性）和**行为**（方法）

##### JS中类（class）和对象（object）的区别
JavaScript语言没有”类“，是通过变通的方法，模拟出”类“
> 所谓”类“就是对象的模板，对象就是”类“的实例

下面的例子用来解释，不需要背
```js
// Class写法
class Person {
    constructor(name) {
        this.name = name;
    }
    
    method = () => {
        console.log("print "+ this.name) 
    }
}

const John1 = new Person("John")
John1.method()  // print John

// Object写法
const John2 = {
    name: "John",
    method() {
       console.log("print "+ this.name) 
    }
   // 不能这么写，这样this是undefined的
   method: () => {
        console.log("print "+ this.name) 
   }
   
}

John2.method() // print John
```


##### JS中对象（Object）和Map的区别，应用场景
> Map对象是一种由对应 Key/Value 对的对象，JS的Object也是 Key/Value 对的对象

区别：
1. Object对象中，只能吧String作为key值，而Map中，key可以是任何基本类型
2. Map有size属性，可以很方便的获取Map的长度
3. Map对象的排序是根据push的顺序排序的，而Object实例中key的对象是有规律的

##### JS中数组（Array）和对象（Object）的区别
> 数组和普通对象的功能类似，也是用来存储一些值的。

区别：
1. 普通对象是使用字符串作为属性名的，而数组是使用数字作为索引来操作元素。
2. 数组的存储性能比普通对象要好
3. 数组中的元素可以是任意的数据类型，也可以是对象，也可以是函数，也可以是数组。数组的元素中，如果存放的是数组，我们就称这种数组为二维数组。

##### 数组常用方法（不需要记）
数组类型相关的

| 方法 | 描述 | 备注 |
| --- | --- | --- |
| Array.isArray() | 判断是否为数组 |      |
| toString()                       | 将数组转换为字符串                 |      |
| Array.from(arrayLike)            | 将**伪数组**转化为**真数组**       |      |
| Array.of(value1, value2, value3) | 创建数组：将**一系列值**转换成数组 |      |

数组元素的添加和删除

| 方法     | 描述                                                 | 备注             |
| :------- | :--------------------------------------------------- | :--------------- |
| concat() | 合并数组：连接两个或多个数组，返回结果为**新的数组** | 不会改变原数组   |
| join()   | 将数组转换为字符串，返回结果为**转换后的字符串**     | 不会改变原数组   |
| split()  | 将字符串按照指定的分隔符，组装为数组                 | 不会改变原字符串 |

数组排序

| 方法      | 描述                                                    | 备注         |
| :-------- | :------------------------------------------------------ | :----------- |
| reverse() | 反转数组，返回结果为**反转后的数组**                    | 会改变原数组 |
| sort()    | 对数组的元素,默认按照**Unicode 编码**，从小到大进行排序 | 会改变原数组 |

查找数组的元素

| 方法                  | 描述                                                                           | 备注                                                     |
| :-------------------- | :----------------------------------------------------------------------------- | :------------------------------------------------------- |
| indexOf(value)        | 从前往后索引，检索一个数组中是否含有指定的元素                                 |                                                          |
| lastIndexOf(value)    | 从后往前索引，检索一个数组中是否含有指定的元素                                 |                                                          |
| includes(item)  | 数组中是否包含指定的内容                                                        |                                                        |
| find(function())      | 找出**第一个**满足「指定条件返回 true」的元素                                  |                                                          |
| findIndex(function()) | 找出**第一个**满足「指定条件返回 true」的元素的 index                          |                                                          |
| every()               | 确保数组中的每个元素都满足「指定条件返回 true」，则停止遍历，此方法才返回 true | 全真才为真。要求每一项都返回 true，最终的结果才返回 true |
| some()                | 数组中只要有一个元素满足「指定条件返回 true」，则停止遍历，此方法就返回 true   | 一真即真。只要有一项返回 true，最终的结果就返回 true     |

遍历数组

| 方法 | 描述 | 备注 |
| :-------- | :--------------------------------------------------------------------- | :----------------------------------------------------- |
| for 循环  | 这个大家都懂 |  |
| forEach() | 和 for 循环类似，但需要兼容 IE8 以上 | forEach() 没有返回值。也就是说，它的返回值是 undefined |
| map() | 对原数组中的每一项进行加工，将组成新的数组 | 不会改变原数组 |
| filter() | 过滤数组：返回结果是 true 的项，将组成新的数组，返回结果为**新的数组** | 不会改变原数组 |
| reduce | 接收一个函数作为累加器，返回值是回调函数累计处理的结果 |  |


#### 三. 函数

##### 什么是函数
> 函数就是将一些功能or语句进行封装，在需要的时候，通过调用的形式，执行这些语句
> - 函数是一个对象
> - 使用typeof 检查函数对象时，会返回function

##### 函数的声明（declare）方式
方式一：命名函数
```js
function 函数名([形参1,形参2...形参N]){  // 备注：语法中的中括号，表示“可选”
        语句...}
```

方式二：函数表达式（匿名函数）
```js
var 变量名  = function([形参1,形参2...形参N]){
        语句....
}
```

方式三：箭头函数
```js
var 变量名 = ([形参1,形参2...形参N]) => {
        语句....
}
```

##### 命名函数 vs (函数表达式 vs 箭头函数)
- 函数表达式和箭头函数之间区别不大，箭头函数是函数表达式的简略写法
- **命名函数**不可以函数表达式提升（hoisting），但是函数表达式可以
- 如果需要在对象内引用函数，使用**命名函数**

##### 函数调用
方式一：普通调用
```js
函数名();
```
方式二：通过对象的方法来调用
```js
var obj = {
        a: 'qianguyihao',
        fn2: function() {
                console.log('千古壹号，永不止步!');
        },};

obj.fn2(); // 调用函数
```
方式三：立即执行函数
```js
(function() {
        console.log('我是立即执行函数');
})();
```
方式四：定时器函数
```js
 let num = 1;
 setInterval(function () {
     num ++;
     console.log(num);
 }, 1000);
```

##### 什么是作用域（Scope）
> Scope是一个变量or函数的作用范围。作用域在函数定义时，就已经确定

两种作用域
- 全局作用域（Global Scope）：变量声明不在函数（function）或者大括号（{  }）中间，被定义为全局作用域，只有在浏览器被关闭时候才会被销毁
- 局部作用域（Local Scope）：分为**函数作用域**和**模块作用域**，代码块运行结束后被销毁

##### 什么是声明提升（Hoisting）
> 整个函数汇总所有的代码执行之前就被**创建完成**。
```js
fn1();  // 虽然 函数 fn1 的定义是在后面，但是因为被提前声明了， 所以此处可以调用函数

function fn1() {
    console.log('我是函数 fn1');
}
```
注意：
1. 函数声明可以使用声明提升，但是函数表达式不可以
2. var可以使用声明提升，但是const和let不可以


##### JS运行的步骤
- 语法分析
- 预编译
- 解释执行

##### 什么是执行上下文（context）
> 当**函数执行**，会创建一个执行期上下文的内部对象，一个执行期上下文定义了一个函数执行时的环境
> 每调用一次函数，就会创建一个新的上下文对象，他们之间是相互独立且独一无二的。当函数执行完毕，它所产生的执行期上下文会被销毁。


##### 什么是this，以及this在函数内的指向（**重要**）
> this 指向的是一个对象，这个对象我们称为函数执行的 上下文对象。

根据函数调用的方式不同，this的指向不同的函数

- 1.以函数的形式（包括普通函数、定时器函数、立即执行函数）调用时，this 的指向永远都是 window。比如`fun();`相当于`window.fun();`

```js
function fun() {
    console.log(this);
    console.log(this.name);}

var obj1 = {
    name: 'smyh',
    sayName: fun,};

var name = '全局的name属性';

//以函数形式调用，this是window
fun(); //可以理解成 window.fun()

// 打印结果：
Window
全局的name属性
```

- 2.以方法的形式调用时，this 指向调用方法的那个对象

```js
function fun() {
    console.log(this);
    console.log(this.name);}

var obj2 = {
    name: 'vae',
    sayName: fun,};

var name = '全局的name属性';

//以方法的形式调用，this是调用方法的对象
obj2.sayName();

// 打印结果
Object
vae
```

- 3. 以构造函数的形式调用时，this 指向实例对象
- 4. 以事件绑定函数的形式调用时，this 指向绑定事件的对象
- 5. 使用 call 和 apply 调用时，this 指向指定的那个对象
- 6. 箭头函数通过继承外层海曙调用的this绑定（无论this绑定到什么）

##### 什么是Call(), Apply() 和 Bind()
- call()
> 可以调用一个函数，与此同时，它还可以改变这个函数内部的**this**指向
> 可以实现继承

举个例子（不需要记）=>解释call()方法

```js
// 例子1：跟普通的调用 fn1() 没有区别
function fn1() {
    console.log(this);
    console.log(this.nickName);
}
    
fn1.call(this); 
// this的指向并没有被改变，此时相当于 fn1();

// 打印结果
window
undefine
```

```js
// 例子2：通过call() 改变this指向
var obj1 = {
    nickName: 'JohnnyBoy',
    age: 28
};

function fn1(a, b) {
    console.log(this);
    console.log(this.nickName);
    console.log(a + b);
}

fn1.call(obj1, 2, 4); // 先将 this 指向 obj1，然后执行 fn1() 函数

// 打印结果
obj1
JohnnyBoy
6
```

```js
// 例子3：通过call()实现继承
// 给 Father 增加 name 和 age 属性function 
Father(myName, myAge) {
    this.name = myName;
    this.age = myAge;}

function Son(myName, myAge) {
    // 【下面这一行，重要代码】
    // 通过这一步，将 father 里面的 this 修改为 Son 里面的 this；另外，给 Son 加上相应的参数，让 Son 自动拥有 Father 里的属性。最终实现继承
    Father.call(this, myName, myAge);}

const son1 = new Son('Johnny Boy', 28);
console.log(JSON.stringify(son1));

// 打印结果
{"myName":"Johnny Boy","myAge":28}
```

- apply()
> 可以调用一个函数，与此同时，它还可以改变这个函数内部的 this 指向。这一点，和 call()类似。
> 
> 由于 apply()需要传递数组，所以它有一些巧妙应用，稍后看接下来的应用举例就知道了。

```js
// 例子1：通过apply() 改变this指向

var obj1 = {
    nickName: 'qianguyihao',
    age: 28,};

function fn1(a) {
    console.log(this);
    console.log(this.nickName);
    console.log(a);}

fn1.apply(obj1, ['hello']); // 先将 this 指向 obj1，然后执行 fn1() 函数
```

- bind()
> 不会调用函数，但是可以改变函数内部的this指向
> 如果我们不需要立即调用，但是需要改变这个函数内部的this指向，使用bind()是最为合适的

```js
新函数 = fn1.bind(想要将this指向哪里，函数实参1，函数实参2)
```

##### 什么是高阶函数（Higher Order Function）
> 高阶函数就是 **参数或者返回值**其中之一是函数

参数是函数：callback function
返回值是函数：闭包

##### 什么是闭包（closure）
> 指有权**访问**另一个函数作用域中**变量**的函数。
> 
> 如果**这个作用域可以访问另外一个函数内部的局部变量**，那就产生了闭包（此时，你可以把闭包理解成是一种现象）；而另外那个作用域所在的函数称之为**闭包函数**。

作用：
```js
function fn1() {
    let a = 20;

    function fn2() {
        console.log(a);
    }
    return fn2;}

const foo = fn1(); // 执行 fn1() 之后，会得到一个返回值。foo 代表的就是 fn2 函数
foo();
```
- 一般来说，在 fn1 函数执行完毕后，它里面的变量 a 会立即销毁。
- 时由于产生了闭包，所以 fn1 函数中的变量 a 不会立即销毁，因为 fn2 函数还要继续调用变量 a。只有等所有函数把变量 a 调用完了，变量 a 才会销毁。
- 通过闭包实现了：全局作用局成功访问到了局部作用域中的变量 a。
