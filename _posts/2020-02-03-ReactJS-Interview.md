---
title: ReactJS面试小结
tags:
- 总结
categories:
- React
- JS
---


#### 一. 基础知识

##### 什么是React
- React是Facebook开发的前端JS库
- 遵循组件的方法，有助于构建可重用的UI组件
- 开发复杂和交互式Web和移动UI
- 庞大的社区支持

##### React的特点
- 使用JSX
- 组件化开发
- 使用虚拟DOM，不是用真实DOM操作
- 它可以用服务器端渲染，好像使用NestJS
- 遵循单向数据流

##### React的优点和限制

优点：
- 提高应用性能
- 方便客户端&服务端使用
- 使用JSX，可读性强
- React容易和Angular等其他框架集成
- 编写UI测试用例变得非常容易

缺点：
- React只是一个库，不是一个完整的框架
- 库非常庞大，需要时间来理解
- 编码变得复杂，因为它使用内联模板和JSX

---

##### 什么是JSX
JSX就是使用 render 和 return 
render后面{} 是加 JS语法
return后面() 是加 HTML语法

##### 为什么浏览器无法读取JSX
- 因为浏览器智能处理JS对象
- 为了可以读取JSX，需要使用Babel这种JSX转换器，把JSX转换成JS对象，传给浏览器

---

##### Real DOM和Virtual DOM两者有什么区别？
> 虚拟DOM是真实DOM在内存中的表示。UI的表示形式保存在内存中，并与实际的DOM同步。

| Real DOM | Virtual DOM |
| --- | --- |
| 1. 更新缓慢 | 1. 更新更快 |
| 2. 可以直接更新HTML | 2. 无法直接更新HTML |
| 3. 如果元素更新，创建新的DOM | 3. 如果元素更新，则更新JSX |
| 4. DOM操作代价很高 | 4. DOM操作非常简单 |
| 5. 消耗内存多 | 5. 很少内存消耗 |

##### Virtual DOM的工作原理
- Virtual DOM是real DOM的副本，是一个节点树
Virtual DOM工作的三个步骤
1. 每当底层数据发生改变，整个UI都将在Virtual DOM中重新渲染
2. 通过算法，计算与之前DOM之间的差异
3. 完成计算后，将实际更改的内容更新到real DOM里面

##### 当调用setState时，render是如何工作的?
将render分成两步：
1. 虚拟DOM渲染: 当render方法被调用时，它返回一个新的组件的虚拟DOM结构。当调用setState()时，render会被再次调用，因为默认情况下shouldComponentUpdate总是返回true
2. 原生DOM渲染：React只会在虚拟DOM中修改真实DOM节点，而且修改的次数很少。


##### ES5 和 ES6的区别
1. require 与 import
- ES5：require库，ES6：import需要的模块

```js
// ES5
var React = require('react');
 
// ES6
import React from 'react';

```

2. export 与 exports

```js
// ES5
module.exports = Component;
 
// ES6
export default Component;

```

3. component 和 function
- ES5: 使用createClass，ES6：使用class和function

```js
// ES5
var MyComponent = React.createClass({
    render: function() {
        return
			<h3>Hello Edureka!</h3>;
    }
});
 

// ES6
class MyComponent extends React.Component {
    render() {
        return
			<h3>Hello Edureka!</h3>;
    }
}

````

4. props
- ES5：需要写propTypes， ES6:直接默认导入

```js
// ES5
var App = React.createClass({
    propTypes: { name: React.PropTypes.string },
    render: function() {
        return
			<h3>Hello, {this.props.name}!</h3>;
    }
});

// ES6
class App extends React.Component {
    render() {
        return
			<h3>Hello, {this.props.name}!</h3>;
    }
}

```

5. state
- ES5: 使用getInitialState来初始化state，ES6: 使用constructor

```js
// ES5
var App = React.createClass({
    getInitialState: function() {
        return { name: 'world' };
    },
    render: function() {
        return
	        <h3>Hello, {this.state.name}!</h3>;
    }
});

// ES6
class App extends React.Component {
    constructor() {
        super();
        this.state = { name: 'world' };
    }
    render() {
        return
	        <h3>Hello, {this.state.name}!</h3>;
    }
}

```

---

#### 二. React组件

##### 为什么React中，一切都是组件？什么是组件化编程？
> 组件是React应用UI的构建块。这些组件将整个UI分成小的独立并且可以复用的部分，每个组件相互独立，不会影响UI的其余部分

##### React中render()的目的
> render: 返回一个React元素，是原生DOM组件的表示。如果需要渲染多个HTML元素，则必须将这些元素都有一个大div包裹起来

##### React 中的StrictMode(严格模式)是什么??
- <StrictMode /> 可以帮助我们检查
    - 验证内部组件是否遵循某些推荐做法
    - 验证是否使用的已经废弃的方法
    - 通过识别潜在的风险预防一些副作用

##### 什么是Props
Props是一个只读组件，它是从父组件传递到子组件中。子组件永远不能将prop送回父组件。维护单向数据流 父组件 -> 子组件

##### 什么是State
State是数据来源，与props不同，它是可变的，创建动态和交互式组件

##### State Vs Props 之间的不同
| 条件 | State | Props |
| --- | --- | --- |
| 从父组件中接收初始值 | Yes | Yes |
| 父组件可以改变值 | No | Yes |
| 在组件中设置默认值 | Yes | Yes |
| 在组件的内部变化 | Yes | No |
| 设置子组件的初始值 | Yes | Yes |
| 在子组件的内部更改 | No | Yes |

总结
- state是组件自己管理自己的数据和状态
- props是外部传入数据和参数
- 没有state叫做无状态组件，有就是有状态组件

##### PropTypes有哪些?为什么使用PropType
> React将自动检查咱们组件上设置的所有props，以确保它们具有正确的数据类型

- 下面是一组预定义的 prop 类型:
    - React.PropTypes.string
    - React.PropTypes.number
    - React.PropTypes.func
    - React.PropTypes.node
    - React.PropTypes.bool

##### 类组件(Class) 和 函数组件(Function) 的区别
- 类组件可以使用其他特性，如状态 state 和生命周期钩子。
- 当组件只是接收 props 渲染到页面时，就是无状态组件，就属于函数组件，也被称为哑组件或展示组件。

##### 如何更新组件的状态
- Class
    - 使用this.setState改变
- Functio
    - 使用 [stateValue, setStateValue] = useState(false);

##### 为什么部直接更新State，而是使用setState的方法?
> 如果直接更新state, 则不会宠幸渲染组件，仅仅只是改变state的参数

##### 什么是React Hooks? 为什么使用它? 
> Hooks是React 16.8新内容，允许不编写类的情况下，使用state和其他React特性。

1. Hooks 通常支持提取和重用跨多个组件通用的有状态逻辑，而无需承担高阶组件或渲染props的负担。可以轻松操组件状态，而不需要将他们转换为类组件。
2. Hooks不能在类中使用，可以完全避免使用生命周期的方法。相反，使用像useEffect这样的内置钩子

##### React中的 useState() 是什么
> useState()是一个内置的React Hook， ()内的内容，可以是数字,可以是Bool...

```
...
const [count, setCounter] = useState(0);
const [moreStuff, setMoreStuff] = useState(...);
...

const setCount = () => {
    setCounter(count + 1);
    setMoreStuff(...);
    ...
};
```

##### 如何使用React Hooks获取数据
> 名为 useEffect 的 effect hook 可用于使用 axios 从 API 中获取数据，并使用 useState 钩子提供的更新函数设置组件本地状态中的数据。让我们举一个例子，它从 API 中获取 react 文章列表。

```js
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function App() {
  const [data, setData] = useState({ hits: [] });

  useEffect(async () => {
    const result = await axios(
      'http://hn.algolia.com/api/v1/search?query=react',
    );

    setData(result.data);
  }, []);

  return (
    <ul>
      {data.hits.map(item => (
        <li key={item.objectID}>
          <a href={item.url}>{item.title}</a>
        </li>
      ))}
    </ul>
  );
}

export default App;
```

> 记住，我们为 effect hook 提供了一个空数组作为第二个参数，以避免在组件更新时再次激活它，它只会在组件挂载时被执行。比如，示例中仅在组件挂载时获取数据。


##### React Hooks会取代 render props还有高阶组件吗?

> Hooks 并没有涵盖类的所有用例，但是有计划很快添加它们。目前，还没有与不常见的 getSnapshotBeforeUpdate 和componentDidCatch 生命周期等效的钩子。


##### 构造函数调用super并将props作为参数传入的作用是什么?

> 在子构造函数中能够通过this.props来获取传入的 props

- 传递props
```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log(this.props);  // { name: 'sudheer',age: 30 }
  }
}
```

- 没传递props
```js
class MyComponent extends React.Component {
  constructor(props) {
    super();
    console.log(this.props); // undefined
    // 但是 Props 参数仍然可用
    console.log(props); // Prints { name: 'sudheer',age: 30 }
  }

  render() {
    // 构造函数外部不受影响
    console.log(this.props) // { name: 'sudheer',age: 30 }
  }
}
```

##### 箭头函数是什么?怎么用?

> 箭头函数（=>）是用于编写函数表达式的简短语法
> 1. 使用箭头函数，在class里面不需要绑定this
> 2. 函数表达式返回的是一个function，通常用于onClick事件上面，来调用某个写好function

```js
 (para1,para2) => {
    console.log("Hello world")
 } 
```

##### 这三个点(...)在React干嘛用的?

"..."是扩展操作符，它是帮助懒人的利器

1. 可以省略大部分重复性的继承 {...this.props}
2. 对于创建具有现有对象的大多数属性的新对象非常方便

```js
// prevState.foo = {b: "abc", c:"abc", d: "abc"}
this.setState(prevState => {
    return {foo: {...prevState.foo, a: "updated"}};
});
```

##### 有状态组件 vs. 无状态组件

| 有状态组件 | 无状态组件 |
| --- | --- |
| 有State，且组件状态会随外部信息变化而变化 | 没有State |
| 通常带有生命周期 | 复用性强，如按钮，标签，输入框 |
| 需要有自己的私有数据 |   |
|  | 运行效率高  |

---

##### ⭐React组件的生命周期（重要）
1. Initialization: 在这个阶段，组件准备设置初始化状态和默认属性
2. 初始渲染阶段（Mounting）： 这是组件即将开始其生命之旅并进入DOM的阶段
    - componentWillMount 在渲染前调用,在客户端也在服务端。
    - componentDidMount : 在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构

3. 更新阶段(Updating)： 一旦组件被添加到DOM，它只有在prop或者状态发生变化时才可能更新和重新渲染
    - componentWillReceiveProps 确定是否更新组件。默认情况下，它返回true。如果确定在 state 或 props 更新后组件不需要在重新渲染，则可以返回false，这是一个提高性能的方法。
    - shouldComponentUpdate 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。
    - componentWillUpdate在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。
    - componentDidUpdate 在组件完成更新后立即调用。在初始化时不会被调用。

4. 卸载阶段(Unmounting)：这是组件生命周期的最后阶段，组件被消耗并从DOM中删除
    - componentWillUnmount在组件从 DOM 中移除之前立刻被调用。

![生命周期图](./JavaScript/Front-End/React/lifeCycle.png)

##### ⭐React中的事件是什么?

- 事件event：鼠标悬停Hover， 鼠标点击Click， 按键等特定操作的触发翻译
    - 用驼峰命名对事件命名
    - 事件作为函数

- 例子(**不需要记得特别详细**)：
    - 剪贴板事件： 
    > onCopy onCut onPaste
    - 键盘事件
    > onKeyDown onKeyPress onKeyUp
    - 焦点事件
    > onFocus onBlur(点别的地方)
    - 表单事件
    > onChange onInput onSubmit
    - 鼠标事件
    > onClick onContextMenu onDoubleClick onDrag onDragEnd onDragEnter onDragExit
onDragLeave onDragOver onDragStart onDrop onMouseDown onMouseEnter onMouseLeave
onMouseMove onMouseOut onMouseOver onMouseUp
    - Selection Events
    > onSelect
    - 触控事件
    > onTouchCancel onTouchEnd onTouchMove onTouchStart
    - 用户界面事件
    > onScroll
    - 滚轮事件
    > onWheel
    - Media Events
    > onAbort onCanPlay onCanPlayThrough onDurationChange onEmptied onEncrypted onEnded onError onLoadedData onLoadedMetadata onLoadStart onPause onPlay onPlaying onProgress onRateChange onSeeked onSeeking onStalled onSuspend onTimeUpdate onVolumeChange onWaiting
    - 图片读取事件
    > onLoad onError

##### 事件处理ES6语法处理class的方法

方法一：通过在constructor中，方法绑定this，默认class是不绑定的(不推荐)

```js
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 为了在回调中使用 `this`，这个绑定是必不可少的
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

方法二：使用箭头函数

```js
class LoggingButton extends React.Component {
  // 此语法确保 `handleClick` 内的 `this` 已被绑定。
  // 注意: 这是 *实验性* 语法。
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

方法三：在回调中使用箭头函数

```js
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // 此语法确保 `handleClick` 内的 `this` 已被绑定。
    return (
      <button onClick={() => this.handleClick()}>
        Click me
      </button>
    );
  }
}
```


##### React中的合成事件
    合成事件是围绕浏览器原生事件充当跨浏览器包装器的对象：简单点来说，就是将不同浏览器的行为合并成一个API

---

##### React的refs是什么
Refs是React中引用References的简写。
    - 有助于存储特定的React元素or组件的引用的属性，它将由组件渲染配置函数返回
    - 用于对render()返回的特定元素or组件的引用
    - 常用场景：input输入value，需要在页面中渲染这个value处理

在Class中使用

```js

class ReferenceDemo extends React.Component{
    display() {
        const name = this.inputDemo.value;
        document.getElementById('disp').innerHTML = name;
    }
    render() {
        return(        
              <div>
                Name: <input type="text" ref={input => this.inputDemo = input} />
                <button name="Click" onClick={this.display}>Click</button>            
                <h2>Hello <span id="disp"></span> !!!</h2>
              </div>
        );
       }
 }

```

也可以在Function中使用
```js
function CustomForm ({handleSubmit}) {
  let inputElement
  return (
    <form onSubmit={() => handleSubmit(inputElement.value)}>
      <input
        type='text'
        ref={(input) => inputElement = input} />
      <button type='submit'>Submit</button>
    </form>
  )
}

```


##### 使用Refs的情景
    - 需要管理焦点，选择文本or媒体播放时
    - 触发式动画
    - 与第三方DOM库集成

---

##### 受控组件 vs 非受控组件

| 受控组件 | 非受控组件 |
| --- | --- |
| 1. 没有维持自己的状态 | 1. 保持自己的状态 |
| 2. 数据由父组件控制 | 2. 数据由DOM控制 |
| 3. 通过Props获取当前值 | 1. 保持自己的状态 |

##### 什么是高阶组件（HOC）?
> 高阶组件: 参数为组件，返回值为新组件的函数。

为什么使用高阶组件：
    1. 抽取重复代码，实现组件复用，常见场景：页面复用。
    2. 条件渲染，控制组件的渲染逻辑（渲染劫持），常见场景：权限控制。
    3. state抽象和控制
    4. Props控制

#####  什么是纯组件
> 纯（Pure） 组件是可以编写的最简单、最快的组件。它们可以替换任何只有 render() 的组件。这些组件增强了代码的简单性和应用的性能。

---

#### 三. React Redux

##### 什么是Redux?
> 是前端开发库之一。用于整个应用的状态管理

##### Redux遵循的三大原则
1. 单一事实来源：整个应用的状态存储在单个 store 中的对象/状态树里。单一状态树可以更容易地跟踪随时间的变化，并调试或检查应用程序。
2. 状态是只读： 改变状态的唯一方法是去触发一个动作（Action）
3. 使用纯函数进行更改： 为了指定状态树如何通过操作进行转换，你需要纯函数。纯函数是那些返回值仅取决于其参数值的函数。


##### Redux的组件
1. Action: 这是一个用来描述发生了什么事情的对象。
2. Reducer: 这是一个确定状态将如何变化的地方。
3. Store: 整个程序的状态/对象树保存在Store中。
4. View: 只显示 Store 提供的数据。

##### 如何在Redux中定义Action
- Action必须具有type属性，指示正在执行的ACTION的类型

```js
function addTodo(text) {
       return {
                type: ADD_TODO,    
                text
               }
}
```

##### 解释Reducer的作用。
> Reducers是一个纯函数，根据ACTION中的type，对store进行更新

##### Store在Redux的意义
> Store是一个JS对象，它可以保存程序的状态，并提供一些方法来访问状态，调度操作和注册侦听器。

##### Redux的优点
1. 总是存在一个真实来源
2. 可维护性
3. 服务器端渲染
4. 易于测试


#### 四. React Router DOM 路由

##### 什么是React路由
> React路由：用于开发单页Web应用，这使URL与网页上显示的数据保存同步

##### React Router的优点
1. 可以将Router可视化为单个根组件(<BrowserRouter>)，其中我们将特定的子路由(<route>)包起来
2. 无需手动设置历史值，使用React-Router-DOM中的useHistory(), useLocation()

##### 为什么使用Switch关键词
> 用于封装 Router 中的多个路由，当你想要仅显示要在多个定义的路线中呈现的单个路线时，可以使用 “switch” 关键字。
> <switch>标记会按顺序将已定义的URL和已定义的路由进行匹配，找到第一个匹配项后，将渲染指定的路径。


##### React路由简单写法

```js
<switch>
    <route exact path=’/’ component={Home}/>
    <route path=’/posts/:id’ component={Newpost}/>
    <route path=’/posts’   component={Post}/>
</switch>
```

#### 五. 优秀React库推荐
- [storybook - 一个让你专心组件开发的工具](https://storybook.js.org/)
- [style-component - ES6用js写css](https://styled-components.com/)
- [antd - 蚂蚁框架，企业级产品设计体系](https://ant.design/index-cn)
- [hygen - 代码模板生成器](https://www.hygen.io/)
- [react-router-DOM - React的路由器](https://reactrouter.com/web/guides/quick-start)
- [react-spring - 弹簧动画效果](https://www.react-spring.io/)
- [react-redux - 全局管理数据](https://react-redux.js.org/introduction/quick-start)

