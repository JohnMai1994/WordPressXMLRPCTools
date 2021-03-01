---
title: JavaScript基础小结（二）
tags:
- 总结
categories:
- JS
---

## 中文版
#### 四. 面向对象
##### 面向过程(OPP) vs. 面向对象(OOP) vs 面向切面(AOP)
**面向过程**（Oriented-Process Programming）：先分析好的具体步骤，然后按照步骤一步一步来
- 优点：性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机采用面向过程编程。
- 缺点：比起面向对象编程，难维护，难复用，难扩展

**面向对象**（Oriented-Object Programming）：以对象功能来划分问题，而不是步骤
> 对代码数据进行封装，并以对象调用的方式，对外提供统一的调用接口

- 优点：易维护，易复用，易扩展。而且有三大特性：封装，多态，继承的特性。
- 缺点：性能比面向过程低

**面向切面**（Aspect-Oriented Programming）：针对业务处理过程中的切面进行提取，它所面对的是处理过程中的某个步骤or阶段，以获得逻辑过程中部分之间低耦合性的隔离效果
> 简单来说：把与主业务无关的代码提取出来，放到代码外面去做。比如添加一层Security进行安全管理

优点：降低主代码的复杂程度，保持主业务代码逻辑干净
缺点：编写复杂，需要使用动态代理模式
例子：Spring， Javaweb的拦截器，装饰器模式，代理模式。

##### 有几种方法创建对象?


> 1. 构造函数 Person 有一个prototype（原型）属性，这个属性是一个指针，指向一个对象即：Person.prototype(原型对象)
> 2. 上面实例 p1 p2 也有一个 [prototype] 属性 或者叫做 `__proto__`这个属性，也是指向Person.prototype
> 3. Person.prototype中有一个constructor属性，这个属性也是一个指针，指向构造函数Person。这样一来，实例 也指向了Person，那么实例也共享了构造函数的属性和方法。
> 4. 构造函数，实例，原型对象里所有的属性和方法 都是共享的


- 方式一：工厂模式 new Object()

```js
function createPerson(name, age) {
    var obj = {};
    obj.name = name;
    obj.age = age;
    obj.eat = function() {
        console.log("张三在吃东西")
    }
    return obj;
}

let p1 = person("张三", 18);
console.log(p1);  //  {name: "张三", age: 18, eat: [Function]}
p1.eat(); // "张三在吃东西"

// p1是Object但不是createPerson
console.log(p1 instanceof Object) //true
console.log(p1 instanceof createPerson)  //false


function Person() {}
p1.__proto__ = Person.prototype
console.log(p1) // Person {name: "张三", age: 18, eat: [Function]}
console.log(p1 instanceof Person) // true
```

- 方式二：构造函数模式

```js
function Person (name, age) {
    this.name = name;
    this.age = age;
    this.eat = function () {
        console.log("李四在吃东西")
    }
}

let p2 = new Person("李四", 19);
console.log(p2);  //  Person {name: "李四", age: 19, eat: [Function]}
p2.eat() // "李四在吃东西"

// p2是Object而且是Person
console.log(p2 instanceof Object)  //true
console.log(p2 instanceof Person)  //true
console.log(Person.prototype) // Person { }

```

- 方式三：Class模式

```js
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
        this.eat = function () {
            console.log("王五在吃东西")
        }
    }
}

let p3 = new Person("王五", 20);
console.log(p3)  //  Person {name: "王五", age: 20, eat: [Function]}
p3.eat();  // "王五在吃东西"

// p3是Object而且是Person
console.log(p3 instanceof Object)  //true
console.log(p3 instanceof Person)  //true
console.log(Person.prototype) // Person { }
```

##### 构造函数的缺点

> 构造函数虽然好用，但也有缺点。既每个new出来的实例 里的方法都要重新创建一遍。
> 没创建一次实例，里面的方法都需要在内存中创造一片空间。每个实例的方法都是不一样的

##### 什么是JS中的`__proto__`
> 每个实例对象（object）都有一个私有属性（称之为`__proto__`）**指向**它的构造函数的原型对象（prototype）
> 
> 如果不是使用new关键词创建的实例对象，那么这个实例对象的`__proto__`应该指向Object的prototype

##### for in 和 hasOwnProperty() 和 Object.keys()

> **for in** 遍历对象所有可枚举属性，包括原型链上的属性
> **Object.keys**遍历对象所有可枚举属性，不包括原型链上的属性
> **hasOwnProperty**检查对象是否包含属性名，无法检查原型链上是否具有此属性名


##### 什么是原型重写
> 原型： 每个JS函数都有prototype属性，这个属性引用了一个对象，这个对象就是原型对象

- 方式一：在原有的原型对象上增加属性or方法

```js
function Person(){}
 
Person.prototype.add = function(){
    alert(this.name);
};
 
var p1 = new Person();
p1.add(); // 这个方法还没有被定义

Person.prototype.name = "Johnny Boy"; 
p1.add(); // Johnny Boy
```

- 方式二：重写（覆盖）原型对象

```js
function Person() {}

// 这里是重写了 原型方法，大括号是代表新一个Object
Person.prototype = {
    add: function () {
        alert(this.name);
    },
    name: "Johnny Boy"
}

var p2 = new Person();
p2.add(); // Johnny Boy
```

> 两种原型重写方法：
> 如果先创建实例，然后再修改原型，采用方式一
> 如果还没有创建实例，采用方式二
> 因为方式二对已经创建的对象无法访问到修改后的原型
> 
>**总的来说：方法一更推荐！！**

##### 属性遮蔽
> 代表原型上也有"name"这个关键词，但是它不会被访问到

```js
function Person() {
    this.name = "王五";
    this.age = 28;
}

const person = new Person();
Person.prototype.name = "赵六";
Person.prototype.sex = "男";

// 最终会显示： 属性遮蔽
console.log(person.name) // 王五
console.log(person.age) // 28
console.log(person.sex) // 男
```



##### 使用不同方法来创建对象和生成原型链
> 因为在JS中，不管你是方法，Array数组，对象都是对象（Object），它们的最终类型都是object

- 对象：`var o = {a : 1}`
> o这个对象继承了Object.prototype上面的所有属性

> o自身没有hasOwnProperty的属性
> hasOwnProperty是Object.prototype的属性
> 因此o继承了Object.prototype的hasOwnProperty

> Object.prototype的原型为null
> 原型链如下：
> o ---> Object.prototype ---> null

- 数组：`var a = ["yo", "what's up", "?"]`
> 数组都继承于Array.prototype
> (Array.prototype 中包含 indexOf, forEach 等方法)

> 原型链如下：
> a ---> Array.prototype ---> Object.prototype ---> null

- 函数：`function f() { return 2 }`
> 函数都继承于 Function.prototype
> (Function.prototype 中包含call, bind等方法)

> 原型链如下：
> f ---> Function.prototype ---> Object.prototype ---> null


##### 深拷贝（Deep Copy） vs 浅拷贝（Shallow Copy）

> **深拷贝**：拷贝多层数据；每一层级别的数据都会拷贝
> **浅拷贝**：只拷贝最外面一层的数据；更深层次的对象，只拷贝引用

- 浅拷贝的实现方式
1. 使用for...in实现浅拷贝
2. 用Object.assgin()实现浅拷贝`Object.assign(目标对象，源对象)`

- 深拷贝的实现方式
1. 通过for in 递归实现

```js
// 方法：深拷贝
function deepCopy(newObj, oldObj) {
    for (let key in oldObj) {
        // 获取属性值 oldObj[key]
        let item = oldObj[key]
        // 判断这个值是否是数组
        if (item instanceof Array) {
            newObj[key] = [];
            deepCopy(newObj[key], item);
        }
        // 判断这个值是否为对象
        else if (item instanceof Object) {
            newObj[key] = {};
            deepCopy(newObj[key], item);
        }
        // 简单数据类型，之间赋值
        else {
            newObj[key] = item;
        }
    }
}
```

##### 对象的冻结（Object.freeze()）
冻结对象后：
- 对象不能被修改
- 不能向这个对象添加新的属性
- 不能删除已有的属性
- 冻结对象后，该对象的原型也不能被修改（prototype）



#### 五. DOM

##### 什么是事件
> 事件：就是文档or浏览器窗口中发生的一些特定的交互瞬间。
> 
> **例子**：点击某个元素，将鼠标移动至某个元素上方，关闭弹窗等等。
> 
> 事件的三要素：**事件源**，**事件**，**事件驱动程序**
> - 事件源：引发后续事件的HTML标签
> - 事件：JS定义好的，如onclick, onkeyup等
> - 事件驱动程序：用JS对CSS和HTML的操作，也就是DOM

##### 常见的事件有哪些（不用背）
| 事件名 | 说明 |
| -- | -- |
| onclick | 鼠标单机 |
| ondblclick | 鼠标双击 |
| onkeyup | 按下并释放键盘上的一个键时触发 |
| onchange | 文本内容or下拉菜单中的选项发生改变 |
| onfocus | 获得焦点，表示文本框等获得鼠标光标 |
| onblur | 失去焦点，表示文本框等失去鼠标光标 |
| onmouseover | 鼠标悬停，即鼠标停留在图片等的上方 |
| onmouseout | 鼠标移除，即离开图片等所在的区域 |
| onload | 网页文档加载事件 |
| onunload | 关闭网页时 |
| onsubmit | 表单提交事件 |
| onreset | 重置表单时 |

##### 什么是DOM
> DOM（Document Object Model）: 操作网页上的元素的API，比如让盒子移动，变色，轮播图
> 
> DOM为文本提供了结构化表示，并定义了如何通过脚本来访问文档结构。目的是为了让js操作html元素而制定的一个规范

##### 什么是节点（Node）
> 节点： 构成HTML网页的最基本单元，网页中的每一个部分都可以称为是一个节点，比如：html标签，属性，文本，注释
> 
> 节点的类型不同，属性和方法也都不尽相同，但是所有的节点都是Object

##### DOM可以做什么？
- 找对象（元素节点）
- 设置元素的属性值
- 设置元素的样式
- 动态创建和删除元素
- 事件的触发响应：事件源，事件，事件的驱动程序

##### 如何获取元素节点
> 使用 document.getElementByXXX()

##### Node节点的相对关系访问（不需要记）

| 父节点 | 兄弟节点 | 子节点 | 所有子节点 |
| -- | -- | -- | -- |
| parentNode | nextSibling | firstChild | childNodes |
|  | nextElementSibling | firstElementChild | childrent |
|  | previousSibling | lastChild |  |
|  | previousElementSibling | lastElementChild |  |

##### Node节点的操作
- 创建节点
    - document.createElement("li");
- 插入节点
    - 父节点.appendChild(新的子节点)
- 删除节点
    - 父节点.removeChild(子节点)
    - 自己删除自己 node1.parentNode.removeChild(node1)
- 复制节点
    - 要复制的节点.cloneNode(); 
- 设置节点的属性
    - 节点.getAttribute();
    - 节点.setAttribute(属性名, 新的属性值);
    - 节点.removeAttribute(属性名);

