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

   