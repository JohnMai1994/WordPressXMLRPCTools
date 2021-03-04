---
title: React Hook小结（一）--- Hook介绍和useState
tags:
- 总结
categories:
- React
---

#### 一. React Hook

##### 什么是React Hooks
> Hooks是钩子的意思，表示的是**React代码执行到特定时期时，会自动调用hooks中的代码，进而完成相应的功能**。
> 
> Hooks可以让函数式组件拥有和class组件同样的功能，可以拥有**state**以及**类似的生命周期**

##### 为什么使用React Hooks
- React Hooks 支持绝大部分的生命周期
- React Hooks可以让界面表现和逻辑分离，React组件负责渲染，Hooks负责数据逻辑的处理，不同组件还可以复用Hooks的代码逻辑。

特点： 
1. 完全可选的，可以选择用Hook或者Class
2. 100%向后兼容的
3. 现在可用

##### React Hooks VS. React Class Component

Class：
> 在定义class类型的组件时，我们通常会把业务逻辑放到几个重要的生命周期函数中
- `componentDidMount`
- `componentDidUpdate`
- `componentWillMount`

例子：注册和取消监听事件（注册监听事件在`componentDidMount`而取消监听事件`componentWillMount`）这样两个组件有相似的业务逻辑，但是却拆解到独立的代码单元中去

Hooks：
> Hooks通过使用`useEffect`把生命周期有关的逻辑合并，并且可以方便进行清理和复用。
> 可以减少使用`this`的使用


##### Hooks的种类

* useState
* useEffect
* useContext
* useReducer
* useCallback
* useMemo
* useRef
* useImperativeHandle
* useLayoutEffect
* useDebugValue


#### 二. useState -- 状态
> 利用 `useState` hook 可以让函数式组件拥有状态管理特性，它与传统的 class 组件的状态管理类似，但是更加简洁，不用频繁的使用 `this`

##### 函数组件使用useState VS. 类组件setState的区别（代码展示）

类组件setState

```js
import React from "react";

export default class ClassComp extends React.Component{
    // 使用构造函数，
    constructor(props) {
        super(props);
        this.state = {
            count :0
        }
    }

    render() {
        // 导入count
        const {count} = this.state;

        return (
            <div>
                 {count} 
                <button onClick={() => {this.setState({count: count +1})}}>
                    变化
                </button>
            </div>
        );
    }
}
```

函数组件useState

```js
import React, {useState} from "react"

export default function FuncComp() {

    const [count, setCount] = useState(0);

    return (
        <div>
            {count}
            <button onClick={() => setCount(count + 1)}>
            	变化
            </button>
        </div>
    )

}
```

##### 注意事项
> useState的参数可以是基本类型，也可以是对象类型，在更新对象类型的时候，要**合并旧的状态**，否则会丢失旧的状态

```js
const [value, setValue] = useState({ name: "John", age: 27}); 

const handleInputChange = () => {
    setValue({
        ...props,
        sex: "男"
    })
}
```


##### 参考资料
[React官网](https://zh-hans.reactjs.org/docs/hooks-overview.html)
[峰华大佬掘金博客](https://juejin.cn/post/6844903991302717448)
