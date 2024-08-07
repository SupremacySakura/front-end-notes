# React开发环境搭建

**使用create-react-app快速搭建开发环境**

`create-react-app`是一个快速**创建React开发环境的工具**,底层由WebPack构建,**封装了配置细节**,开箱即用

执行命令:

npx create-react-app react-basic

1. npx Node.js工具命令,查找并执行后续的包命令
2. creat-react-app 核心包(固定写法),用于创建React项目
3. react-basic React项目的名称(可以自定义)

创建React项目的更多方式

https://zh-hans.react.dev/learn/start-a-new-react-project

# JSX基础

## 概念与本质

**什么是JSX**

概念:JSX是JavaScript和XML(HTML)的缩写,表示在JS代码中编写HTML模板结构,它是React中编写UI模板的方式

```react
const message = 'this is message'
function APP(){
    return(
    	<div>
        	<h1>this is title</h1>
            {message}
        </div>
    )
}
```

优势:

1. HTML的声明式模板写法
2. JS的可编程能力

**JSX的本质**

JSX并不是标准的JS语法,它是JS的语法扩展,浏览器本身不能识别,需要通过解析工具做解析之后才能在浏览器中运行

## 识别JS表达式

在JSX中可以通过**大括号语法{}**识别JavaScript中的表达式,比如常见的变量,函数调用,方法调用等等

1. 使用大括号传递字符串
2. 使用JavaScript变量
3. 函数调用和方法调用
4. 使用JavaScript对象

**注意**:if语句,switch语句,变量声明语句,不是表达式,不能出现在{}中

## 实现列表渲染

语法:在JSX中可以使用原生JS中的**map方法**遍历渲染列表

```react
const list = [
    { id: 1001 , name: 'Vue' }
    { id: 1002 , name: 'React' }
    { id: 1003 , name: 'Angular' }
]
```

```react
<ul>
	{list.map(item => <li key={item.id}>{item.name}</li>)}
</ul>
```

## 实现基础条件渲染

语法:在React中,可以通过**逻辑与运算符,三元表达式(?:)**实现基础的条件渲染

```react
{flag&&<span>this is span</span>}
{loading?<span>loading...</span>:<span>this is span</span>}
```

## 实现复杂条件渲染

```react
const articleType = 3 //0 1 3

function getArticleTem(){
    if (articleType===0){
        return <div>我是无图文章</div>
    } else if (articleType===1) {
        return <div>我是单图文章</div>
    } else if (articleType===3) {
        return <div>我是三图文章</div>
    }
}

function App(){
    return (
    <div className="App">
   		{getArticleTem()}     
    </div>
   )
}
```

# React中的事件绑定

## React基础事件绑定

语法:	**on + 事件名称 = { 事件处理程序 }**,整体上遵循驼峰命名法 

```react
function App () {
    const clickHandler = () => {
        console.log('button按钮点击了')
    }
    return (
    	<button onClick={clickHandler}></button>
    )
}
```

## 使用事件对象参数

语法:在事件回调函数中**设置形参e**

```react
function App () {
    const clickHandler = (e) => {
        console.log('button按钮点击了',e)
    }
    return (
    	<button onClick={clickHandler}></button>
    )
}
```

## 传递自定义参数

语法:事件绑定的位置改造成**箭头函数的写法**,在执行clickHandler实际处理业务函数的时候传递实参

```react
function App () {
    const clickHandler = (name) => {
        console.log('button按钮点击了',name)
    }
    return (
    	<button onClick={()=>clickHandler('Jack')}></button>
    )
}
```

注意:不能直接写函数调用,这里事件绑定需要一个**函数引用**

## 同时传递事件对象和自定义参数

语法:在事件绑定的位置传递事件实参和自定义参数,clickHandler中声明形参,注意顺序对位

```react
function App () {
    const clickHandler = (name,e) => {
        console.log('button按钮点击了',name)
    }
    return (
    	<button onClick={(e)=>clickHandler('Jack',e)}></button>
    )
}
```

# React组件的基础使用

## 组件是什么

概念:一个组件就是用户界面的一部分,它可以有自己的逻辑和外观,组件之间**可以相互嵌套,也可以使用多次**

组件化开发可以让开发者像搭积木一样构建一个完整庞大的应用

## React组件

在React中,一个组件就是**首字母大写的函数**,内部存放了组件的逻辑和视图UI,渲染组件只需要把组件**当成标签书写**即可

```react
//1.定义组件
function Button() {
    //组件内部逻辑
    return <button>click me</button>
}
//2.使用组件
function App() {
    return(
    <div>
    	{/*自闭合*/}
    	<Button/>
        {/*成对标签*/}
        <Button></Button>
    </div>
    )
}
```

# useState

## useState-基础使用

`useState`是一个React Hook (函数) , 它允许我们向组件添加一个**状态变量**,从而控制影响组件的渲染结果

本质:和普通的JS变量不同的是,状态变量一旦发生变化组件的视图UI也会跟着变化(数据驱动视图)

```react
const [count,setCount] = useState(0)

const handleClick = () => {
    //作用:1.用传入的新值修改count
    //2.重新使用新的count渲染UI
    setCount( count + 1 )
}
```

1. useState是一个函数,返回值是一个数组
2. 数组中的第一个参数是状态变量,第二个参数是set函数用来修改状态变量
3. useState的参数将作为count的初始值

## useState-修改状态的规则

**状态不可变**

在React中,状态被认为是只读的,我们应该始终**替换它而不是修改它**,直接修改状态不能引发视图更新

```react
const [count,setCount] = useState(0)

const handleClick = () => {
    //直接修改无法引发视图更新
    count++
}
```

```react
const handleClick = () => {
    //作用:1.用传入的新值修改count
    //2.重新使用新的count渲染UI
    setCount( count + 1 )
}
```

**修改对象状态**

规则:对于对象类型的状态变量,应该始终传给set方法一个**全新的对象**来进行修改

```react
const [form,setForm] = useState(
    {
        name:'Jack',
    }
)
const handleChangeName = () => {
    setForm(
    	{
            ...form,
            name:'John',
        }
    )
}
```

# 基础样式控制

## 基础类名控制

React组件基础的样式控制有俩种方式

1.行内样式(不推荐)

```react
<div style={{color:'red'}}>this is div</div>
<div style={style}>this is div</div>
```

2.class类名控制

```react
//index.css
.foo{
    color:red
}
//App.js
import './index.css'

function App(){
    return (
    	<div>
        	<span className='foo'> this is span </span>
        </div>
    )
}
```

## classnames工具优化类名控制

`classnames`是一个简单JS库,可以非常方便的通过条件动态控制class类名的显示

```powershell

npm install classnames

yarn add classnames

```



```react
import classNames from 'classnames'

//语法
// classname={classnames('nav-item',{active:type===item.type})}
//'nav-item'为静态类名
//active为动态类名,在返回值为true时显示
```

# 受控表单绑定

概念:使用React组件的状态(useState)控制表单的状态

1.准备一个React状态值

```react
const [value,setValue] = useState('')
```

2.通过value属性绑定状态,通过onChange属性绑定状态同步的函数

```react
<input
	type="text"
    value={value}
    onChange={(e)=>setValue(e.target.value)}
    ></input>
```

# React获取DOM

在React组件中获取/操作DOM,需要使用`useRef`钩子函数,分为两步:

1.使用useRef创建ref对象,并与JSX绑定

```react
const inputRef = useRef(null)


<input type="text" ref={inputRef} />
```

2.在DOM可用时,通过inputRef.current拿到DOM对象

```react
console.log(inputRef.current)
```

示例:

```react
//React中获取DOM
import { useRef } from "react"
//1.useRef生成ref对象 绑定dom标签身上

//2.dom可用时,ref.current获取dom
//渲染完毕之后dom生成之后才可用

function App(){
    const inputRef = useRef(null)
    const showDom = () => {
        console.log(inputRef.current)
    }
    return (
    	<div>
        	<input type="text" ref={inputRef}></input>
            <button onClick={showDom}>获取dom</button>
        </div>
    )
}
```

# 组件通信

## 父传子-基础实现

理解组件通信:组件通信就是组件之间的数据传递,根据组件嵌套关系的不同,有不同的通信方法

实现步骤:

1. 父组件传递数据-在子组件标签绑定属性
2. 子组件接收数据-子组件通过`props`参数接收数据

```react
function Son (props) {
    //props:对象里面包含; 父组件传递过来的所有数据
    console.log(props)
    return (<div>this is son ,{props.name}</div>)
}

function App () {
    const name = 'this is app name'
    return(
    	<div>
        	<Son name={name}></Son>
        </div>
    )
}
```

## 父传子-props说明

1.`props`可以传递任意的数据

数字,字符串,布尔值,数组,对象,函数,JSX

```react
<Son
	name={appName}
    age={20}
    isTrue={false}
    list={['Vue','React']}
    obj={{name:'Jack'}}
    cb={()=>console.log(123)}
    child={<span>this is span child</span>}
>
</Son>
```

2.props是只读对象

子组件**只能读取props中的数据**,不能进行直接修改,父组件的数据只能由父组件修改

## 父传子-children说明

场景:当我们想要把内容嵌套在子组件标签中时,父组件会自动在名为children的prop属性中接收该内容

```react
<Son>
	<span>this is span</span>
</Son>

//props.children
```

## 子传父

核心思路:在子组件中调用父组件中的函数并传递参数

```react
//父组件
function App () {
    const getMsg = (msg) => console.log(msg)
    return (
    	<div>
        	<Son onGetMsg={getMsg}></Son>
        </div>
    )
}
```

```react
//子组件
function Son ({onGetMsg}) {
    const sonMsg = 'this is son msg'
    return (
    	<div>
        	<button onClick={() => onGetMsg(sonMsg)}></button>
        </div>
    )
}
```

## 兄弟组件通信

**使用状态提升实现兄弟组件通信**

实现思路:借助"状态提升"机制,通过父组件进行兄弟组件之间的数据传递

1.一个子组件通过子传父的方式把数据传递给父组件App

2.App拿到数据后通过父传子的方式再传递给另一个子组件

## 使用context机制跨层传递数据

实现步骤:

1. 使用`creatContext`方法创建一个上下文对象Ctx
2. 在顶层组件(App)中通过`Ctx.Provider`组件提供数据
3. 在底层组件(B)中通过`useContext`钩子函数获取消费数据

```react
import { createContext } from "react"

//1.createContext方法创建一个上下文对象
const MsgContext = createContext()

//2.在顶层组件 通过Provider组件提供数据

//3.在底层组件 通过useContext钩子函数使用数据

function A () {
    return(
    	<div>
        	<B/>
        </div>
    )
}
function B () {
    const msg = useContext(MsgContext)
    return (
    	<div>
        	this is B component,{msg}
        </div>
    )
}

function App () {
    const msg = 'this is app msg'
    return (
    	<div>
        	<MsgContext.Provider value = {msg}>
            	this is App
                <A/>
            </MsgContext.Provider>
        </div>
    )
}
```

# useEffect

## useEffect-概念理解与基础使用

1.useEffect的概念理解

`useEffect`是一个React Hook函数,用于在React组件中创建不是由事件引起而是**由渲染本身引起的操作**,比如发送AJAX请求,更改DOM等等

2.useEffec的基础使用

**需求**:在组件渲染完毕之后,立刻从服务端获取频道列表数据并显示到页面中

**语法**:

```react
useEffect(()=>{},[])
```

参数1是一个函数,可以把他叫做**副作用函数**,在函数内部可以放置需要执行的操作

参数2是一个数组(可选参),在数组里面放置依赖项,不同的依赖项会影响第一个参数函数的执行,**当是一个空数组的时候,副作用函数只会在组件渲染完毕之后执行一次**

```react
import { useEffect, useState } from "react"

cosnt URL = 'http://geek.itheima.net/v1_0/channels'

function App () {
    //创建一个状态数据
    const [ List , setList ] = useState([])
    useEffect(()=>{
        //额外的操作 获取频道列表
        async function getList () {
            const res = await fetch(URL)
            const jsonRes = await res.json()
            console.log(jsonRes)
            setList(jsonRes.data.channels)
        }
        getList()
    },[])
    return(
    	<div>
        	this is app 
            <ul>
            	{list.map(item => <li key = {item.id}>{item.name}</li>)}
            </ul>
        </div>
    )
}
```

## useEffect-不同依赖项说明

useEffect副作用函数执行的时机存在多种情况,根据**传入的依赖项不同**,会有不同的执行表现

|     依赖项     |        副作用函数执行时机         |
| :------------: | :-------------------------------: |
|   没有依赖项   |    组件初始渲染+组件更新时执行    |
|   空数组依赖   |      只在初始渲染时执行一次       |
| 添加特定依赖项 | 组件初始渲染+特效依赖项变化时执行 |

## useEffect-清除副作用

在useEffect中编写的**由渲染本身引起的对接组件外部的操作**,社区页经常把它叫做**副作用操作**,比如在useEffect中开启了一个定时器,我们想在组件卸载时把这个定时器清理掉,这个过程就是清理副作用

语法:

```react
useEffect(()=>{
    //实现副作用的操作逻辑
    const timer = setInterval(()=>{
        console.log('定时器执行中...')
    },1000)
    return()=>{
        //清除副作用逻辑
        clearInterval(timer)
    }
},[])
```

# 自定Hook实现

概念:自定义Hook是以**use打头的函数**,通过自定义Hook函数可以用来实现**逻辑的封装和复用**

```react
//问题:布尔值切换的逻辑 当前组件耦合在一起的 不方便使用

//解决思路:自定义hook

import { useState } from "react"

function useToggle () {
    //可复用的逻辑代码
    const [value,setValue] = useState(true)
    const toggle = () => setValue(!value)
    //哪些状态和回调函数需要在其他组件中使用return
    return {
        value,
        toggle
    }
}

function App () {
    const { value, toggle } = useToggle()
    return (
    	<div>
        	{value && <div>this is div</div>}
            <button onClick={toggle}>toggle</button>
        </div>
    )
}
```

# ReactHooks使用规则

使用规则

1. 只能在组件中或者其他自定义Hook函数中调用
2. 只能在组件的顶层调用,不能嵌套在if,for,其他函数中

# Redux

## 快速上手

**什么是Redux**

`Redux`是React最常用的**集中状态管理工具**,类似于Vue中Pinia(Vuex),**可以独立与框架运行**

作用:通过集中管理的方式管理应用的状态

**Redux快速体验**

需求:不和任何框架绑定,不使用任何构建工具,使用纯Redux实现计数器

使用步骤:

1. 定义一个`reducer`函数(根据当前想要做的修改返回一个新的状态)
2. 使用`createStore`方法传入一个reducer函数,生成一个store实例对象
3. 使用store实例的`subscribe`方法订阅数据的变化(数据一旦改变,可以得到通知)
4. 使用store实例的`dispatch`方法提交action对象,触发数据变化(告诉reducer你想怎么修改数据)
5. 使用store实例的`getState`方法获取最新的状态数据更新到视图中

```javascript
//1.定义reducer函数

//作用:根据不同的action对象,返回不同的新的state

//state:管理的数据初始状态

//action:对象type标记当前想要做什么样的修改

function reducer (state = { count: 0 },action) {

	if(action.type === 'INCREMENT'){
		return { count:state.count + 1 }
	}
    if(action.type === 'DECREMENT'){
        return { count:state.count - 1 }
    }
	return state
}
//2.使用reducer函数生成store实例
const store = Redux.createStore(reducer)

//3.通过store实例的subscribe订阅数据变化
//回调函数可以在每次state发生变化的时候自动执行
store.subscribe(() => {
    console.log('state变化了',store.getState())
    document.getElementById('count').innerText = store.getState().count
})

//4.通过store实例的dispatch函数提交action更改状态
const inBtn = document.getElementById('increment')
inBtn.addEventListener('click',()=>{
    //增
    store.dispatch(
    	{type:'INCREMENT'}
    )
})
const dBtn = document.getElementById('decrement')
inBtn.addEventListener('click',()=>{
    //减
    store.dispatch(
    	{type:'DECREMENT'}
    )
})

```

**Redux管理数据流程**

1. state - 一个对象,存放着我们管理的数据状态
2. action - 一个对象,用来描述你想怎么修改数据
3. reducer - 一个函数,根据action的描述生成一个新的state

## Redux与React-环境准备

**配套工具**

在React中使用Redux,官方要求安装其他俩个插件 - Redux Toolkit 和 react-redux

1.Redux Toolkit (RTK) - 官方推荐的编写Redux逻辑的方式,是一套工具的集合集,**简化书写方式**

| 简化store的配置方式 | 内置immer支持可变式状态修改 | 内置thunk更好的异步创建 |
| ------------------- | --------------------------- | ----------------------- |

2.react-redux - 用来 **链接 Redux 和 React组件** 的中间件

**配置基础环境**

1.使用 CRA 快速创建 React 项目

```powershell
npx creat-react-app react-redux
```

2.安装配套工具

```powershell
npm i @reduxjs/toolkit react-redux
```

3.启动项目

```powershell
npm run start
```

**整体路径熟悉**

1.Redux store 配置

配置counterStore模块

配置store并且组合counterStore模块

2.React组件

注入store(react-redux)

使用store中的数据

修改store中的数据

## Redux与React-实现counter

### **使用React Toolkit 创建 counterStore**

```javascript
// counterStore.js

import { createSlice } from '@reduxjs/toolkit'

const counterStore = creatSlice({
    name:'counter',
    //初始状态数据
    initialState:{
        count:0
    },
    //修改数据的方法
    reducer:{
        increment (state) {
        	state.count++
        },
        decrement (state) {
            state.count--                   
      	},                     
    }
})

//结构出创建action对象的函数 {actionCreater}
const { increment, decrement } = counterStore.action
//获取reducer函数
const counterReducer = counterStore.reducer
//导出创建action对象的函数和reducer函数
export { increment, decrement }
export default counterReducer
```

```javascript
// store/index.js
import { configureStore } from '@reduxjs/toolkit'

import counterReducer from "./modules/counterStore"

//创建根store组合子模块
const store = configureStore({
    reducer:{
        counter:counterReducer
    }
})
export default store
```

```react
// index.js
import store from './store'

import { Provider } from 'react-redux'
    
    
const root = ReactDOM.creatRoot(document.getElementById('root'))
root.render(
	<React.StrictMode>
    	<Provider store={store}>
        	<App />
        </Provider>
    </React.StrictMode>
)
```

### **React组件使用store的数据**

在React组件中使用store中的数据,需要用到一个 钩子函数 - `useSelector`,它的作用是把store中的数据映射到组件中

```react
import { useSelector } from 'react-redux'
function App () {
    const { count } = useSelector(state => state.counter)
	//counter子模块
    return (
    	<div className="App">
        	{ count }
        </div>
    )
}

```

### React组件中修改store中的数据

React组件中修改store中的数据需要借助另一个hook函数 - `useDispatch`, 它的作用是生成提交action对象的dispatch函数

```react
import { useDispatch, useSelector } from 'react-redux'
//导入创建action对象的方法
import { decrement, increment } from './store/modules/counterStore'
function App () {
    const { count } = useSelector(state => state.counter)
	//得到dispatch函数
    const dispatch = useDispatch()
    return (
        <button onClick={()=>dispatch(decrement())}></button>
    	<div className="App">
        	{ count }
        </div>
        <button onClick={()=>dispatch(increment())}></button>
    )
}

```

### React组件中提交action传参

在reducer的同步方法中**添加action对象参数**,在**调用actionCreater的时候传递参数**,参数会被传递到**action对象的payload属性**上

```javascript
// counterStore.js

import { createSlice } from '@reduxjs/toolkit'

const counterStore = creatSlice({
    name:'counter',
    //初始状态数据
    initialState:{
        count:0
    },
    //修改数据的方法
    reducer:{
        increment (state) {
        	state.count++
        },
        decrement (state) {
            state.count--                   
      	},
        addToNum(state,action){
            state.count = action.payload
        }
    }
})

//结构出创建action对象的函数 {actionCreater}
const { increment, decrement, addToNum } = counterStore.action
//获取reducer函数
const counterReducer = counterStore.reducer
//导出创建action对象的函数和reducer函数
export { increment, decrement, addToNum }
export default counterReducer
```

```react
// App.js
import { useDispatch, useSelector } from 'react-redux'
//导入创建action对象的方法
import { decrement, increment, addToNum } from './store/modules/counterStore'
function App () {
    const { count } = useSelector(state => state.counter)
	//得到dispatch函数
    const dispatch = useDispatch()
    return (
        <button onClick={()=>dispatch(decrement())}>-</button>
    	<div className="App">
        	{ count }
        </div>
        <button onClick={()=>dispatch(increment())}>+</button>
        <button onClick={()=>dispatch(addToNum(10))}>add to 10</button>
    )
}
```

### Redux与React异步状态操作

(1)创建store的写法保持不变,配置好同步修改状态的方法

(2)单独封装一个函数,在函数内部return一个新函数,在新函数中

1. 封装异步请求获取数据
2. 调用同步actionCreater传入异步数据生成的action对象,并使用dispatch提交

(3)组件中dispatch的写法保持不变

```javascript
// channelStore.js
import { createSlice } from "@reduxjs/toolkit"
import axios from 'axios'

const channelStore = createSlice({
    name:'channel'
    initialState;{
    	channelList:[]
	},
    reducer:{
        setChannels ( state, action ) {
            state.ChannelList = action.payload
        } 
    }
})

//异步请求部分
const { setChannels } = channelStor.action
const fetchChannelList = () => {
    return async (dispatch) => {
        const res = await axios.get('http://geek.itheima.net/v1_0/channels')
        dispatch(setChannels(res.data.channels))
    }
}
export { fetchChannelList }
export default channelReducer
```

```react
// App.js
import { useEffect } from 'react'
import { useDispatch, useSelector } from 'react-redux'
//导入创建action对象的方法
import { decrement, increment, addToNum } from './store/modules/counterStore'
import { fetchChannelList } from './store/modules/channelStore'
function App () {
    const { count } = useSelector(state => state.counter)
    const { channelList } = useSelector(state => state.channel)
	//得到dispatch函数
    const dispatch = useDispatch()
    //使用useEffect触发异步请求执行
    useEffect(()=>{
        dispatch(fetchChannelList)
    },[dispatch])
    return (
        <button onClick={()=>dispatch(decrement())}>-</button>
    	<div className="App">
        	{ count }
        </div>
        <button onClick={()=>dispatch(increment())}>+</button>
        <button onClick={()=>dispatch(addToNum(10))}>add to 10</button>
        <ul>
        	{ChannelList.map(item => <li key={item.id}>{item.name}</li>)}
        </ul>
    )
}
```

# ReactRouter

## 快速上手

**什么是前端路由**

一个路径path对应一个组件component当我们浏览器在中访问一个path的时候,path对应的组件会在页面中进行渲染

```javascript
const routes = [
    {
        path:'/about'
        component:About
    },
    {
        path:'/article'
        component:Article
    },
]
```

**创建路由开发环境**

1.创建项目并安装所有依赖

```powershell
npx create-react-app react-router-pro
npm i
```

2.安装最新的ReactRouter包

```powershell
npm i react-router-dom
```

3.启动项目

```powershell
npm run start
```

**快速开始**

需求:创建一个可以切换登录页和文章页的路由系统

```react
//index.js

import { createBrowserRouter, RouterProvider } from 'react-router-dom'

//1.创建router实例对象并且配置路由对应关系
const router = createBrowserRouter ([
    {
        path:'/login',
        element:<div>我是登录页</div>
    },
    {
        path:'/article'
        element:<div>我是文章页</div>
    }
])
const root = ReactDOM.creatRoot(document.getElementById('root'))
root.render(
	<React.StrictMode>
    	<RouterProvider router={router}></RouterProvider>
    </React.StrictMode>
)
```

## 抽象路由模块

```javascript
//router/index.js
import { createBrowserRouter } from 'react-router-dom'

//1.创建router实例对象并且配置路由对应关系
const router = createBrowserRouter ([
    {
        path:'/login',
        element:<div>我是登录页</div>
    },
    {
        path:'/article'
        element:<div>我是文章页</div>
    }
])

export default router
```

```react
import router from './router/index.js'

import { RouterProvider } from 'react-router-dom'



const root = ReactDOM.creatRoot(document.getElementById('root'))
root.render(
	<React.StrictMode>
    	<RouterProvider router={router}></RouterProvider>
    </React.StrictMode>
)

```

## 路由导航跳转

**什么是路由导航跳转**

路由系统中的多个路由之间需要进行**路由跳转**,并且在跳转的同时有可能需要**传递参数进行通信**

### 声明式导航

声明式导航是指通过在模板中通过`<Link/>`**组件描述出要跳转到哪里去**

```react
<Link to="/article">文章</Link>
```

语法说明:通过给组件的**to属性指定要调到路由的path**,组件会被渲染为浏览器支持的a链接,如果需要传参直接**通过字符串拼接的方式拼接参数**即可

### 编程式导航

编程式导航是指通过`useNavigate`钩子得到导航方法,然后通过**调用方法以命令式的形式**进行路由跳转

```react
import { useNavigate } from "react-router-dom"

const Login = () => {
    const navigate = useNavigate()
    return(
    	<div>
        	我是登录页
            <button onClick={() =>navigate('/article') }>跳转至文章</button>
        </div>
    )
}
```

语法说明:通过调用navigate方法传入地址path实现跳转

## 导航跳转传参

1.`searchParams`传参

```react
import { useNavigate } from "react-router-dom"
navigate('/article?id=1001&name=jack')
```

```react
import { useSearchParams } from "react-router-dom";
const [params] =useSearchParams()
let id = params.get('id')
```

2.`params`传参

```react
import { useNavigate } from "react-router-dom"
navigate('/article/1001')
```

```react
import { useParams } from "react-router-dom"
const params = useParams()
let id = params.id
```

```javascript
//修改路由配置
{
        path:'/article/:id'
        element:<div>我是文章页</div>
    }
```

# 别名路径配置

1.路径解析配置(webpack),把@/解析为src/

2.路径联系配置(VSCode),VSCode在输入@/时,自动联想出来对应src/下的子级目录

## 路径解析配置

CRA本身把webpack配置包装到了黑盒里无法直接修改,需要借助一个插件-`craco`

配置步骤:

1.安装craco

```powershell
npm i -D @craco/craco
```

2.项目根目录下创建配置文件

craco.config.js

3.配置文件中添加路径解析配置

```javascript
// 配置信息
const path = require('path')

module.exports = {
  // webpack 配置
  webpack: {
    // 配置别名
    alias: {
      // 约定：使用 @ 表示 src 文件所在路径
      '@': path.resolve(__dirname, 'src')
    }
  }
}

```

4.包文件中配置启动和打包命令

```json
// 将 start/build/test 三个命令修改为 craco 方式
"scripts": {
  "start": "craco start",
  "build": "craco build",
  "test": "craco test",
  "eject": "react-scripts eject"
},

```



## 联系路径配置

VSCode的联想配置,需要我们在项目目录下添加**jsconfig.json**文件,加入配置之后VSCode会自动读取配置帮助我们自动联想提示

配置步骤:

1.根目录下新增配置文件-jsconfig.json

2.添加路径提升配置

```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}

```

# useReducer

**作用**:和useState作用类似,用来管理**相对复杂**的数据状态

## 基础用法

1.定义一个reducer函数(根据不同的action返回不同的新状态)

```react
function reducer (state,action) {
    //	根据不同的action type 返回新的state
    switch (action.type) {
            case:'INC':
            	return state + 1
            case:'DEC':
            	return state - 1
        	default:
            	return state
    }
}
```

2.在组件中调用useReducer,并传入reducer函数和状态的初始值

```react
const [ state,dispatch ] = useReducer(reducer,0)
```

3.事件发生时,通过dispatch函数分派一个action对象(通知reducer要返回哪个新状态并且渲染UI)

```react
dispatch({ type: 'INC' })
```

## 分派action时传参

```react
dispatch({
    type:'SET'
    payload:100
})
```

```react
function reducer (state,action) {
    //	根据不同的action type 返回新的state
    switch (action.type) {
            case:'INC':
            	return state + 1
            case:'DEC':
            	return state - 1
            case;'SET':
            	return action.payload
        	default:
            	return state
}
```

# useMemo

**作用**:在组件每次重新渲染的时候缓存计算的结果(类似于计算属性)

```react
function App () {
    const [state1,setCount1] = useState(0)
    //result只会在count1发生改变时重新计算
    const result = useMemo(()=>{
        //返回计算得到的结果
        return fib(count1)
    },[count1])
    return(
    	<div>
        	<button onClick={()=>setCount1(count1+1)}></button>
        </div>
    )
}
```

# React.memo

**作用**:允许组件在Props没有改变的情况下跳过渲染

React组件默认的渲染机制,只要父组件重新渲染子组件就会重新渲染(会造成资源浪费)

## 基础语法

```react
import { memo } from "react"
const MemoComponent = memo(function SomeComponent(props){
    // ... 
})
                           
                           
```

说明:经过memo函数包裹生成的缓存组件只有在props发生变化的时候才会重新渲染

## props的比较机制

机制:在使用`memo`缓存组件之后,React会对**每一个prop**使用**Object.is**比较新值和老值,返回true,表示没有变化



prop是简单类型

Object.is(3,3) => true 没有变化



prop是引用类型(对象/数组)



Object.is([],[]) => false,React只关心引用是否变化

# useCallback

**作用**:在组件多次重新渲染的时候缓存函数

## 基础语法

```react
//没使用useCallback
const Input = memo(function Input ({onChange}){
    console.log('子组件重新渲染了')
    return(<input type="text" onChange={(e)=>onChange(e.target.value)}></input>)
})
                   
function App () {
    //传给子组件的函数
    const changeHandler = (value) => console.log(value)
    //触发父组件重新渲染的函数
    const [count,setCount] = useState(0)
    return(
    	<div classname="App">
            <Input onChange={changeHandler}></Input>
            <button onClick={()=>setCount(count+1)}>{count}</button>
        </div>
    )
}                   
```

```react
//使用useCallback
const Input = memo(function Input ({onChange}){
    console.log('子组件重新渲染了')
    return(<input type="text" onChange={(e)=>onChange(e.target.value)}></input>)
})
                   
function App () {
    //传给子组件的函数
    const changeHandler = useCallback((value) => console.log(value),[])
    //触发父组件重新渲染的函数
    const [count,setCount] = useState(0)
    return(
    	<div classname="App">
            <Input onChange={changeHandler}></Input>
            <button onClick={()=>setCount(count+1)}>{count}</button>
        </div>
    )
}                   
          
```

说明:使用useCallback包裹函数之后,函数可以保证在App**重新渲染的时候保持引用稳定**

# forwardRef

场景说明:父组件通过ref获取到子组件内部的input元素让其聚焦

```react
import { forwardRef, useRef } from "react"

const Son = forwardRef((props,ref)=>{
    return (
    	<input type="text" ref={ref}></input>
    )
})

function App () {
    const sonRef =useRef(null)
    const showRef = () => {
        console.log(sonRef)
    }
    return (
    <>
        <Son ref={sonRef}></Son>
        <button onClick={showRef}>focus</button>
    </>
    )
}

```

# useInperativeHandle

场景说明:父组件通过ref调用子组件内部的focus方法实现聚焦

```react
//子组件
const Input = forwardRef((props,ref)=>{
    const inputRef = useRef(null)
    //实现逻辑聚焦函数
    const focusHandler = () => {
        inputRef.current.focus()
    }
    //暴露函数给父组件调用
    useImperativeHandler(ref,() => {
        return {
            focusHandler
        }
    })
    return(
    	<input type="text" ref={ inputRef }></input>
    )
})
```

# Class类组件

## 类组件的基础结构

类组件就是通过**JS中的类来组织的代码**

```react
class Counter extends Component {
    //自定义状态变量
    state = {
        count: 0,
    }
    //事件回调
    clickHandler = () => {
        this.setState({
            count:this.state.count + 1
        })
    }
    
    //UI模板
    render () {
        return <button onClick={this.clickHandler}>{this.state.count}</button>
    }
}
```

1. 通过类属性`state`定义状态数据
2. 通过`setState`方法来修改数据
3. 通过`render`来写UI模板(JSX语法一致)

## 类组件生命周期函数

概念:组件从创建到销毁的**各个阶段自动执行的函数**就是生命周期函数

1. `componentDidMount`:组件挂载完毕自动执行 - 异步数据获取
2. `componentWillUnmount`:组件卸载时自动执行 - 清理副作用

```react
class Counter extends Component {
   	//生命周期函数
    //组件渲染完毕执行一次 发送网络请求
    componentDidMount () {
        console.log('组件渲染完毕了,请求发送起来')
        //开启定时器
        this.timer = setInterval(()=>{
            console.log('定时器运行中')
        })
    }
    //组件卸载的时候自动执行 副作用清理的工作 清除定时器 清除事件绑定
    componentWillUnmount () {
        console.log('组件被卸载了')
        
        clearInterval(this.timer)
    }
    //UI模板
    render () {
        return <div>I am son</div>
    }
}
```

## 类组件的组件通信说明

概念:类组件和Hooks编写的组件在组件通信上的**思路完全一致**

1. 父传子:通过prop绑定数据
2. 子传父:通过prop绑定父组件中的函数,子组件调用
3. 兄弟通信:状态提升,通过父组件做桥接

```react
//子组件
class Son extends Component {
    render () {
        //使用this.props.msg
        return <>
        	<div>我是子组件 {this.props.msg}</div>
        	<button onClick={()=>this.props.onGetMsg('我是子组件中的数据')}></button>
        </>
    }
}

//父组件
class Parent extends Component {
    state = {
        msg: 'this is parent msg'
    }
    
    getSonMsg = (sonMsg) => {
        console.log(sonMsg)
    }
    
    
    render () {
        return <div>我是父组件<Son msg={this.state.msg} onGetMsg={this.getSonMsg}></Son></div>
    }
}
```

# zustand

## 基础用法

```react
//zustand
import { create } from 'zustand'

//1.创建store

const useStore = create((set)=>{
    return {
        //状态数据
        count:0,
        //修改状态数据的方法
        inc:()=>{
            set((state)=>({count:state.count+1}))
        }
    }
})

//2.绑定store到组件

function App () {
    const { count, inc } = useStore()
    return (
    <>
    	<button onClick={inc}>{count}</button>    
    </>
    )
}
```

## 异步支持

对于异步的支持不需要特殊的操作,直接在函数中编写异步逻辑,最后只需要**调用set方法传入最新状态**即可

```react
//zustand
import { create } from 'zustand'

const useStore = create((set)=>{
    return {
        //状态数据
        channelList:[],
        //异步方法
        fetchChannelList:async()=>{
            const res = await fetch(URL)
            const jsonData = await res.json()
            //调用set方法更新状态
            set({
                channelList:jsonData.data.channels
            })
        }
    }
})


```

## 切片模式

场景:当单个store比较大时,可以采用**切片模式**进行模块拆分组合,类似于模块化

```react
//zustand
import { create } from 'zustand'

//创建counter相关切片
const createCounterStore = (set) => {
    return {
        count:0,
        setCount:()=>{
            set(state=>({ count:state.count + 1}))
        }
    }
}

//创建channel相关切片
const createChannelStore = (set)=>{
    return {
        //状态数据
        channelList:[],
        //异步方法
        fetchChannelList:async()=>{
            const res = await fetch(URL)
            const jsonData = await res.json()
            //调用set方法更新状态
            set({
                channelList:jsonData.data.channels
            })
        }
    }
}

//组合切片
const useStore = create((...a)=>({
    ...createCounterStore(..a)
    ...createChannelStore(..a)
}))
```

