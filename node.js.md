# Node.js

## 什么是Node.js

**定义**:Node.js是一个跨平台**JavaScript**运行环境,使开发者可以搭建服务器端的JavaScript应用程序

**作用**:使用Node.js编写服务器端程序

- 编写数据接口,提供网络资源浏览功能等等
- **前端工程化**:为后续学习Vue和React等框架做铺垫



**什么是前端工程化**:

前端工程化:开发项目直到上线,过程中集成所有的**工具和技术**

Node.js是前端工程化的基础(因为Node.js可以主动读取前端代码的内容)



**Node.js与浏览器环境中JS最大的区别**:

Node.js环境中没有BOM和DOM



**Node.js如何执行代码**:

在VSCode终端中输入:**node xxx.js** 回车即可执行(注意路径)



**Node.js为何能执行JS?**

首先:浏览器能执行JS代码,依靠的是内核中的V8引擎(C++程序)

其次:Node.js是基于Chrome V8引擎进行封装(运行环境)

区别:都支持ECMAScript标准语法,Node.js有独立的API

注意:Node.js环境中没有DOM和BOM等

## fs模块-读写文件

模块:类似插件,封装了**方法/属性**

fs模块:封装了与本机系统文件进行交互的,方法/属性

语法:

1. 加载fs模块对象
2. 写入文件内容
3. 读取文件内容

```javascript
const fs = require('fs')//fs是模块表示符,模块的名字
```

```javascript
fs.writeFile('文件路径','写入内容',err=>{
	//写入后的回调函数
})
```

```javascript
fs.readFile('文件路径',(err,data)=>{
//读取后的回调函数
//data是文件内容的Buffer数据流
})
```

## path模块-路径处理

问题:Node.js代码中,相对路径是根据终端所在路径来查找的,可能无法找到你想要的文件

建议:在Node.js代码中,使用**绝对路径**

补充:**__dirname**内置变量(获取当前模块目录-绝对路径)

- windows：D:\备课代码\3-B站课程\03_Node.js与webpack\03-code\03
- mac:/User/xxx/Desktop/备课代码/3-B站课程/03_Node.js与webpack/03-code/03

注意:**path.join()**会使用特定于平台的分隔符作为定界符,将所有给定的路径片段链接在一起

```javascript
path.join('03','dist/js','index.js')
//windows:'03\dist\js\index.js'
//mac:'03/dist/js/index.js'
```

语法:

1. 加载path模块

   ```javascript
   const path = require('path')
   ```

2. 使用path.join方法,拼接路径

   ```javascript
   path.join('路径1','路径2',...)
   ```

   

## URL中的端口号

URL:统一资源定位符,简称网址,用于访问服务器里的资源

端口号:标记服务器里不同功能的**服务程序**

端口号范围:0-65535之间的任意整数

| http | ://  | hmajax.itheima.net | :    | 80     | /api/province |
| ---- | ---- | ------------------ | ---- | ------ | ------------- |
| 协议 |      | 域名               |      | 端口号 | 资源路径      |

注意:http协议,**默认**访问**80**端口

### 常见的服务程序

**Web服务程序**:用于提供网上信息浏览功能

注意:0-1023和一些特定的端口号被占用,我们自己编写的服务程序请避开使用

## http模块---创建Web服务

需求:创建Web服务并响应内容给浏览器

步骤:

1. 加载**http模块**,创建Web服务对象
2. 监听**request**请求事件,设置响应体和响应头
3. 配置**端口号**并**启动**Web服务
4. 浏览器请求 http://localhost:3030 测试 (localhost:固定代表本机的域名)

```javascript
//1.加载http模块,创建Web服务对象
const http =require('http')
const server = http.createServer()
//2.监听request请求事件,设置响应体和响应头
server.on('request',(req,res) => {
//设置响应头:内容类型,普通文本:编码格式为utf-8
    res.setHeader('Content-Type','text/plain;charset=utf-8')
    res.end('你好,欢迎使用node.js创建的web服务')
})
//3.配置端口号并启动Web服务
server.listen(3000,() => {
    console.log('web服务已启动')
})
```

## Node.js模块化

**什么是模块化?**

**定义**:CommonJS模块是为Node.js打包JavaScript代码的原始方式,Node.js还支持浏览器和其他JavaScript运行时使用的ECMAScript模块标准.**在Node.js中,每个文件都被视为一个单独的模块**

概念:项目是由很多模块文件组成的

好处:提高代码复用性,按需加载,**独立作用域**

使用:需要标准语法**导出**和**导入**进行使用

### CommonJS标准

需求:定义utils.js模块,封装基地址和求数组综合函数

使用:

1. **导出:module.exports = {}**
2. **导入:require('模块名或路径')**

模块名或路径:

- 内置模块:直接写名字(例如:fs,path,http)
- 自定义模块:写模块文件名路径(例如:./utils.js)

```javascript
const baseURL = 'http://hmajax.itheima.net'
const getArraySum = arr => arr.reduce((sum,val) => sum+=val,0)

module.exports = {
    对外属性名1:baseURL,
    对外属性名2:getArraySum
}
```

