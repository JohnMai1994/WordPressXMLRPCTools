---
title: React Hook小结（二）--- useEffect
tags:
- 总结
categories:
- React
---

#### 二. useEffect -- 副作用
> useEffect是用来处理副作用side effect的。

什么是副作用？
> 对于 **数据抓取，注册监听事件，修改DOM元素等**在第一次渲染后，马后炮式的操作。
> 
> 因为React在第一次渲染后，如果有state状态发生改变，就会进行再次渲染，所以任何在**第一次**渲染后的操作，都会产生副作用


##### useEffect什么时候被调用
`useEffect` **必然会在render的时候执行一次**，其他的运行时机取决于以下的情况：
- **有没有第二个参数**。`useEffect` hook 接受两个参数，第一个是要执行的代码，第二个是一个数组，指定一组依赖的变量，其中任何一个变量发生变化时，此 effect 都会重新执行一次。
- **有没有返回值**。 `useEffect` 的执行代码中可以返回一个函数，在每一次新的 render 进行前或者组件 unmount 之时，都会执行此函数，进行清理工作。

##### useEffect与生命周期的关系
> `useEffect`我觉得可以想象成 `componentDidMount`, `componentDidUpdate`和`componentWillUmmount`三个生命周期的结合体


##### useEffect的使用
```js

function App() {
    const [showList, setShowList] = useState(false);
    const [postCount, setPostCount] = useState(5);
    
    return (
        <div className="App">
            <button onClick={() => setShowList(!showList)}>
            {showList ? "隐藏" : "显示"}
            </button>
            <button onClick={() => setPostCount(previousCount => previousCount + 1)}>
            增加数量
            </button>
            {showList && <PostList count={postCount} />}
        </div>
    )
}


function PostList({ count = 5 }) {
    useEffect(() => {
        // 添加新的document Element P
        let p = document.createElement("p");
        p.innerHTML = `当前文章数量：${count}`;
        document.body.append(p);
        
        // 当useEffect再次被调用时，会调用这个函数，清除掉 Element P
        return () => {
            p.remove();
        };
    });

    return (
    <ul>
    {new Array(count).fill("文章标题").map((value, index) => {
        return (
            <li key={index}>
                {value}
                {index + 1}
            </li>
        );
    })}
    </ul>
    );
}
```

##### 如何在useEffect抓取数据
如果使用`fetch`或者`axios`，它们是异步操作，那么得给`useEffect`hook 传递一个async的函数吧？
 
 错！！！传递给`useEffect`的函数不能说async，因为async/await的本质是返回来一个Promise，而`useEffect`唯一接收的返回值是个函数。所以会出现这个异常

> Warning: An effect function must not return anything besides a function, which is used for clean-up.

```js
// 错误的写法
useEffect( async () => {
    const response = await fetch("https://abc.com/post")
})
```

正确的写法是：把抓取数据的逻辑定义到一个单独的函数中，然后在`useEffect`中调用它

```js
useEffect(() => {
    // 抓取数据
  const loadPosts = async () => {
    setLoading(true);
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/posts?_limit=${count}`
    );
    const data = await response.json();
    // 调用useState Hook
    setPosts(data);
    setLoading(false);
  };
    
  // 记得跑这个function，不然只是定义一个function而已
  loadPosts();
}, [count]);

```

##### useEffect划重点

1. 它可不完全是 `componentDidMount`， `componentDidUpdate`，`componentWillUnmount` 三个生命周期的结合体哦（人家有自己的想法）。
2.  会在每次 render 的时候必定执行一次。
3. 如果返回了函数，那么在下一次 render 之前或组件 unmount 之前必定会运行一次返回函数的代码。
4. 如果指定了依赖数组，且不为空，则当数组里的每个元素发生变化时，都会重新运行一次。
5. 如果数组为空，则只在第一次 render 时执行一次，如果有返回值，则同 3。
6. 如果在 `useEffect` 中更新了 state，且没有指定依赖数组，或 state 存在于依赖数组中，就会造成死循环。

##### 参考资料
[React官网](https://zh-hans.reactjs.org/docs/hooks-overview.html)
[峰华大佬掘金博客](https://juejin.cn/post/6844903991302717448)
