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

