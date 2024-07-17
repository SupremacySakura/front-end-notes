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

## useState基础使用

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

## useState修改状态的规则

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

