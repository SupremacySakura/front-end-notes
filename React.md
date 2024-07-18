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
