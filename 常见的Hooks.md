#常见的Hooks总结

##useState

### 使用方式

```typescript
const [count,setcount] = useState("1")
```

### 参数解析

> count:存储当前状态
> setcount：修改状态
> 1:初始值

### 函数解析

调用 useState 方法的时候做了什么? 它定义一个 “state 变量”。我们的变量叫 count， 但是我们可以叫他任何名字，比如 banana。这是一种在函数调用时保存变量的方式 —— useState 是一种新方法，它与 class 里面的 this.state 提供的功能完全相同。一般来说，在函数退出后变量就会”消失”，而 state 中的变量会被 React 保留。

useState 需要哪些参数？ useState() 方法里面唯一的参数就是初始 state。不同于 class 的是，我们可以按照需要使用数字或字符串对其进行赋值，而不一定是对象。在示例中，只需使用数字来记录用户点击次数，所以我们传了 0 作为变量的初始 state。（如果我们想要在 state 中存储两个不同的变量，只需调用 useState() 两次即可。）

useState 方法的返回值是什么？ 返回值为：当前 state 以及更新 state 的函数。这就是我们写 const [count, setCount] = useState() 的原因。这与 class 里面 this.state.count 和 this.setState 类似，唯一区别就是你需要成对的获取它们。如果你不熟悉我们使用的语法，我们会在本章节的底部介绍它。



##useRequest

###简介
一个强大的管理异步数据请求的Hook。

###使用方式
 ```typescript

const {
  data,
  error,
  loading,
  run,
  params,
  cancel,
  refresh,
  fetches,
} = useRequest(service, {
  manual,
  initialData,
  refreshDeps,
  onSuccess,
  onError,
  formatResult,
  loadingDelay,
  defaultParams,
  pollingInterval,
  pollingWhenHidden,
  refreshOnWindowFocus,
  focusTimespan,
  debounceInterval,
  throttleInterval,
});

 ```

 ### 重点参数解析
>run: 手动触发 service 执行，参数会传递给 service
debounce 模式与 throttle 模式返回值为Promise<null>
>params:当次执行的 service 的参数数组。比如你触发了 run(1, 2, 3)，则 params 等于 [1, 2, 3]



>manual:默认 false。 即在初始化时自动执行 service。如果设置为 true，则需要手动调用 run 触发执行。
>initialData:默认的 data.
>refreshDeps	在 manual = false 时，refreshDeps 变化，会触发 service 重新执行.
>formatResult	格式化请求结果
>defaultParams	如果 manual=false ，自动执行 run 的时候，默认带上的参数
>loadingDelay	设置显示 loading 的延迟时间，避免闪烁
>pollingInterval	轮询间隔，单位为毫秒。设置后，将进入轮询模式，定时触发 run
>pollingWhenHidden	
在页面隐藏时，是否继续轮询。默认为 true，即不会停止轮询
如果设置为 false , 在页面隐藏时会暂时停止轮询，页面重新显示时继续上次轮询
>refreshOnWindowFocus	
在屏幕重新获取焦点或重新显示时，是否重新发起请求。默认为 false，即不会重新发起请求。
如果设置为 true，在屏幕重新聚焦或重新显示时，会重新发起请求。
>focusTimespan	屏幕重新聚焦，如果每次都重新发起请求，不是很好，我们需要有一个时间间隔，在当前时间间隔内，不会重新发起请求需要配置 refreshOnWindowFocus 使用。
>debounceInterval	防抖间隔, 单位为毫秒，设置后，请求进入防抖模式。
>throttleInterval	节流间隔, 单位为毫秒，设置后，请求进入节流模式。

###函数解析

useRequest是一个十分高效的数据处理函数，封装了日常使用中能用到的绝大部分功能，例如：防抖和节流，要善于使用。

##useCallback

###使用

```javaScript

const getnum=useCallback(fn,deps)

```

###参数简介
>fn:要使用的回调函数
>deps:fn依赖的数据
>getnum:返回的新函数

###函数解析
把内联回调函数及依赖项数组作为参数传入 useCallback，它将返回该回调函数的 memoized 版本，该回调函数仅在某个依赖项改变时才会更新。当你把回调函数传递给经过优化的并使用引用相等性去避免非必要渲染（例如 shouldComponentUpdate）的子组件时，它将非常有用。

>注意：依赖项数组不会作为参数传给回调函数。虽然从概念上来说它表现为：所有回调函数中引用的值都应该出现在依赖项数组中。


#？？？？？useCallback作用及原理

##useEffect

这是一个庞大而且冗杂的知识点，但是却可以对React有一个更加深入的认识。

在学习useEffect之前，首先需要了解一下什么是纯函数、什么是副效应、什么是钩子等等。

###纯函数

>纯函数：只进行单纯的数据计算（换算）的函数，在函数式编程里面称为 "纯函数"（pure function）

###副效应
>副效应：函数式编程将那些跟数据计算无关的操作，都称为 "副效应" （side effect） 。如果函数内部直接包含产生副效应的操作，就不再是纯函数了，我们称之为不纯的函数。

举个例子来说：比如生成日志、储存数据、改变应用状态等等都是副作用。

###钩子（Hook）的作用

一句话，钩子（hook）就是 React 函数组件的副效应解决方案，用来为函数组件引入副效应。 函数组件的主体只应该用来返回组件的 HTML 代码，所有的其他操作（副效应）都必须通过钩子引入。

由于副效应非常多，所以钩子有许多种。React 为许多常见的操作（副效应），都提供了专用的钩子。

useState()：保存状态
useContext()：保存上下文
useRef()：保存引用
......
上面这些钩子，都是引入某种特定的副效应，而 useEffect()是通用的副效应钩子 。找不到对应的钩子时，就可以用它。其实，从名字也可以看出来，它跟副效应（side effect）直接相关。


###useEffect用法

```typescript

import React, { useEffect } from 'react';

function Welcome(props) {
  useEffect(() => {
    document.title = '加载完成';
  });
  return <h1>Hello, {props.name}</h1>;
}

```

useEffect()的作用就是指定一个副效应函数，组件每渲染一次，该函数就自动执行一次。组件首次在网页 DOM 加载后，副效应函数也会执行。


###useEffect第二个参数

```typescript
function Welcome(props) {
  useEffect(() => {
    document.title = `Hello, ${props.name}`;
  }, [props.name]);
  return <h1>Hello, {props.name}</h1>;
}
```


上面例子中，useEffect()的第二个参数是一个数组，指定了第一个参数（副效应函数）的依赖项（props.name）。只有该变量发生变化时，副效应函数才会执行。

如果第二个参数是一个空数组，就表明副效应参数没有任何依赖项。因此，副效应函数这时只会在组件加载进入 DOM 后执行一次，后面组件重新渲染，就不会再次执行。这很合理，由于副效应不依赖任何变量，所以那些变量无论怎么变，副效应函数的执行结果都不会改变，所以运行一次就够了。

###useEffect返回值
useEffect()允许返回一个函数，在组件卸载时，执行该函数，清理副效应。如果不需要清理副效应，useEffect()就不用返回任何值。

```typescript
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    subscription.unsubscribe();
  };
}, [props.source]);
```

上面例子中，useEffect()在组件加载时订阅了一个事件，并且返回一个清理函数，在组件卸载时取消订阅。

实际使用中，由于副效应函数默认是每次渲染都会执行，所以清理函数不仅会在组件卸载时执行一次，每次副效应函数重新执行之前，也会执行一次，用来清理上一次渲染的副效应。



##useMount

###用法

```typescript

const MyComponent = () => {
  useMount(
    () => {
      message.info('mount');
    }
  );


```

###函数作用
在组件mount时执行的Hook

##useRef


### 知识点总结

1.useRef是一个方法，且useRef返回一个可变的ref对象（对象！！！）
2.initialValue被赋值给其返回值的.current对象
3.可以保存任何类型的值:dom、对象等任何可辨值
4.ref对象与自建一个{current：‘’}对象的区别是：useRef会在每次渲染时返回同一个ref对象，即返回的ref对象在组件的整个生命周期内保持不变。自建对象每次渲染时都建立一个新的。
5.ref对象的值发生改变之后，不会触发组件重新渲染。有一个窍门，把它的改边动作放到useState()之前。
6.本质上，useRef就是一个其.current属性保存着一个可变值“盒子”。目前我用到的是pageRef和sortRef分别用来保存分页信息和排序信息。

作者：是你的山楂
链接：https://juejin.cn/post/6844904174417608712
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

> 需要注意的是，useRef还需要在真正的应用中慢慢总结其使用场景。


> 待补充待补充待补充待补充待补充待补充


##usePersistFn
##usememo