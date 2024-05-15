# 数组解构

## 解构赋值

```javascript
const [max,min,avg]=[100,60,80]
console.log(max)//最大值100
console.log(min)//最小值60
console.log(avg)//平均值80
```

### 基本语法

1.赋值运算符=左侧的[]用于批量声明变量，右侧数组的单元值将被赋值给左侧变量

2.变量的顺序对应数组单元值的位置依次进行赋值操作

## 数组解构

### 基本语法

典型应用：交换两个变量

```javascript
let a=1
let b=3;//分号必须加
[b,a]=[a,b]
```

**防止有undefined传递单元值的情况，可以设置默认值**

```javascript
const [a='手机',b='华为']=['小米']
```

按需导入，忽略某些返回值

```javascript
const [a,,c,d]=['小米','华为','苹果','格力']
```

# 对象解构

## 基本语法

1.赋值运算符=左侧的[]用于批量声明变量，右侧数组的单元值将被赋值给左侧变量

2.对象属性的值将被赋值给与属性名**相同**的值

3.注意解构的变量名不要和外面的变量名冲突否则报错

4.对象中找不到与变量名一致的属性时变量值为undefined

```javascript
const user={
    name:'小明',
    age:18
};
//批量声明变量 name age
//同时将数组单元值 小明 18 依次给变量 name age
const [name,age]=user
```

*对象解构的变量名 可以重新改名 旧变量名：新变量名*

```javascript
const {uname:username,age}={uname:'pink老师',age:18}
```

*多级对象解构*

```javascript
const {name,family:{mother,father,sister}}=pig
```

# forEach遍历数组

## 作用

遍历数组

## 语法

```javascript
const arr=['red','green','pink']
arr.forEach (function(item,index){//item：当前数组元素,index:当前元素索引号
    console.log(item)//red green pink
    console.log(index)//索引号
})
```

# 构造函数

自己定义构造函数创建对象

1.1 创建对象的三种方式

​	1.利用对象字面量创建对象

```javascript
const o = {
    name:'佩奇'
}
```

​	2.利用 new Object 创建对象

```javascript
const o = new Object({name:'佩奇'})
```

​	3.利用构造函数创建对象

​		使用场景：快速创建多个类似的对象

```javascript
function Pig(name,age,gender){//注意：这里函数名必须以大写字母开头
	this.name=name
    this.age=age
    this.gender=gender
}
//创建佩奇对象
const Peppa = new Pig('佩奇'，6,'女')
```

​		**说明**

​		1）使用new关键词调用函数的行为被称为实例化

​		2）实例化构造函数没有参数时可以省略括号（）

​		3）构造函数内部无需写return，返回值即为新创建的对象

​		4）构造函数内部的return返回的值无效

​		5）new Object（） new Date（）也是实例化构造对象

# 实例成员与静态成员

## 实例成员

通过构造函数创建的对象称为实例对象，实例对象中的属性和方法称为实例成员

​	**说明**

​	1.为构造函数传入参数，创建结构相同但值不同的对象

​	2.构造函数创建的实例对象彼此独立互不影响

## 静态成员

构造函数的属性和方法被称为静态成员（静态属性和静态方法）

```javascript
//eg.构造函数
function Person(name,age){
    //省略实例成员
}
//静态属性
Person.eyes=2
Person/arms=2
//静态方法
Person.walk=function(){
    console,log('^_^人人都会走路')
}
//this指向
```

## 实例方法

### Array

|  方法   | 作用     | 说明                                       |
| :-----: | -------- | ------------------------------------------ |
| forEach | 遍历数组 | 不返回数组，经常用于查找和遍历数组元素     |
| filter  | 过滤数组 | 返回新数组，返回的是筛选满足条件的数组元素 |
|   map   | 迭代数组 | 返回新数组，返回的是处理之后的数组元素     |
| reduce  | 累计器   | 返回累计处理的结果，经常用于求和等         |

#### reduce

##### 语法

```javascript
//arr.reduce(function(){},起始值)
//arr.reduce(function(上一次的值，当前值),初始值)
//如果有初始值，则把初始值加一次进去
```

#### 数组常见方法-其他方法

1.join，数组元素拼接为字符串，**返回字符串**

2.find，查找元素，返回符合测试条件的第一个数组元素值，如果没有符合条件的则返回**undefined**

3.every,检测数组所有元素是否都符合指定条件，**如果所有元素都能通过检测，返回true，否则返回false**

4.some，检测数组中的元素是否满足指定条件，**如果数组中有元素满足条件，返回true，否则返回false**

5.concat,合并两个数组，返回新数组

6.sort,对原数组单元值排序

7.splice,删除或替换原数组单元

8.reverse，反转数组

9.findindex，查找元素的索引值

#### 伪数组变真数组

```javascript
//Array.from()
```

### String

#### 常见实例方法

1.length,**用来获取字符串的长度**

2.split('分隔符')，**用来将字符串拆分为数组**

3.substring(需要截取的第一个字符的索引[,结束的索引]),**用于字符串截取**

4.startsWith(检测字符串[,检测位置索引号]),检测是否以某字符开头

5.includes(搜索的字符串[,检测位置索引号]),判断一个字符串是否包含在另一个字符串中，根据情况返回一个true或false

6.toUpperCase,用于将字母转换为大写

7.toLowerCase，用于将字母转换为小写

8.indexOf,检测是否包含某字符

9.endsWith,检测是否以某字符结尾

10.replace,用于替换字符串，支持正则匹配

11.match,用于查找字符串，支持正则匹配

# 原型

- 构造函数通过原型分配的函数是所有对象**共享的**

- javaScript规定，**每一个构造函数都有一个prototype属性**，指向另一个对象，所以我们也成为原型对象

- 这个对象可以挂载函数，对象实例化不会多次创建原型上函数，节约内存

- **我们可以把那些不变的方法，直接定义在prototype对象上，这样所有的对象的实例就可以共享这些方法**

- **构造函数和原型对象中的this都指向实例化的对象**

  ```javascript
  let that
  function Star(uname){
      that=this
      //console.log(this)
      this.uname=uname
  }
  //实例对象ldh
  //构造函数里面的this就是 实例对象 ldh
  const ldh =new Star('刘德华')
  console.log(that===ldh)
  
  ```

## constructor属性

每个原型对象里面都有个constructor属性（constructor构造函数）

**作用：**该属性**指向**该原型对象的**构造函数**，**简单理解，就是指向我的爸爸，我是有爸爸的孩子**

```javascript
console.log(Star.prototype)
Star.prototype = {
    //重新指回创造这个原型对象的 构造函数
    constructor:Star,
    sing:function(){
        console.log('唱歌')
    },
    dance:function(){
        console.log('跳舞')
    }，
}

```

## 对象原型

**对象都会有一个\_\_proto\_\_**指向构造函数的prototype原型对象,之所以我们对象可以使用构造函数prototype原型对象的属性和方法，就是因为对象有\_\_proto\_\_原型的存在

**注意：**

- _\_proto__是JS非标准属性
- [[prototype]]和\__proto__意义相同
- 用来表明当前实例对象指向哪个原型对象prototype
- \__proto__对象原型里面也有一个constructor属性，**指向创建该实例对象的构造函数**

## 原型继承

```javascript
//继续抽取 公共的部分放在原型上
const Person = {
    eyes:2,
    head:1
}
//女人 构造函数 继承 想要 继承 Person
function Woman(){
    
}
//Woman 通过原型来继承 Person
Woman.prototype = Person
//指回原来的构造函数
Woman.prototype.constructor = Woman
const red = new Woman()
console.log(red)
console.log(Woman.prototype)
//男人 构造函数 继承 想要 继承 Person
function Man(){
    
}
cosnt pink = new Man()
```

```javascript
//构造函数 new 出来的对象 结构一样，但是对象不一样
function Person(){
    this.eyes = 2
    this .head = 1
}
//女人 构造函数 继承 想要 继承 Person
function Woman(){
    
}
//Woman 通过原型来继承 Person
Woman.prototype = new Person()//{eyes:2,head:1}
//指回原来的构造函数
Woman.prototype.constructor = Woman

// 给女人添加一个方法 生孩子
Woman.prototype.baby = function(){
    console.log('宝贝')
}
const red = new Woman()
console.log(red)
```

子类的原型=new 父类

## 原型链

 基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对象的链状关系称为原型链

### 查找规则

1. 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性
2. 如果没有就查找它的原型（也就是\__proto__指向的prototype原型对象)
3. 如果还没有就查找原型对象的原型（Object的原型对象）
4. 以此类推一直找到Object为止(null)
5. \__proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者是一条路线
6. 可以使用instanceof运算符用于检测构造函数的prototype属性是否出现在某个实例对象的原型链上

# 深浅拷贝

## 浅拷贝

首先浅拷贝和深拷贝只针对引用类型

浅拷贝:拷贝的是地址

**常见方法**

1. 拷贝对象：Object.assgin()	|	展开运算符{...obj}拷贝对象
2. 拷贝数组：Array.prototype.concat()|[...arr]

```javascript
const obj = {
    uname:'pink'
}
const o = {...obj}
console.log(o)//{uname:'pink'}
o.uname = 'red'
console.log(o)//{uname:'red'}
console.log (obj)//{uname:'pink'}
```

```javascript
const pink = {
    name:'pink老师',
    age:18
}
const red = {}
Object.assign(red,pink)
console.log(red)//{uname:'pink老师'，age:18}
red.name = 'red老师'
console.log(red)//{name:'red老师',age:18}
//不会影响pink对象
console.log(pink)//{name:'pink老师'，age：18}
//但是还是有问题:多层应用类型会出错
```

## 深拷贝

深拷贝:拷贝的是对象,不是地址

### 常见方法

1. 通过递归实现深拷贝
2. lodash/cloneDeep
3. 通过JSON.stringfy()实现

#### 函数递归：

**如果一个函数在内部调用其本身，那么这个函数就是递归函数**

- 简单理解：函数内部自己调用自己，那么这个函数就是递归函数
- 递归函数的作用和循环效果类似
- 由于递归很容易发生“栈溢出”错误（stack overflow），所以**必须要加退出条件return**

```javascript
const o = {}
//拷贝函数
function deepCopy(newObj,oldObj){
    for(let k in oldObj)
        //处理数组问题
        if(oldObj[k] instanceof Array){
            newObj[k]=[]
            deepCopy(newobj[k],oldObj[k])
        } 
        //处理对象问题
        else if(oldObj[k] instanceof Object){
            newObj[k]={}
            deepCopy(newobj[k],oldObj[k])
        } else {
            // k 属性名 uname age	oldObj[k] 属性值 18
            newObj[k] = oldObj[k]
        }
}
deepCopy(o,obj)
```

```javascript
<script src = "./lodash.min.js"></script>
<script>
    const obj = {
        uname:'pink',
        age:18,
        hobby:['乒乓球','足球'],
        family:{
            baby:'小pink'
        }
    }
    const o =_.cloneDeep(obj)
    console.log(o)
    o.family.baby = '老pink'
    console.log(obj)
</script>
```

```javascript
 const obj = {
        uname:'pink',
        age:18,
        hobby:['乒乓球','足球'],
        family:{
            baby:'小pink'
        }
    }
 //把对象转换为JSON字符串
 //console.log(JSON.stringify(obj))
 const o = JSON.parse(JSON.stringify(obj))
 console.log(o)
 o.family.baby = '123'
 console.log(obj)
```

# 异常处理

## throw 抛异常

异常处理是预估代码执行过程中可能发生的错误，然后最大程度的避免错误的发生导致整个程序无法继续运行

```javascript
function counter(x,y){
    if(!x||!y){
        // throw '参数不能为空'
        throw new Errow('参数不能为空')
    }
}
counter()
```

**总结**

1. throw抛出异常信息，程序也会终止运行
2. throw后面跟的是错误提示信息
3. Error对象配合throw使用，能够设置更详细的错误信息

## try/catch捕获错误信息

我们可以通过try / catch 捕获错误信息 (浏览器提供的错误信息) 	try 试试	catch 拦住	finally 最后

```javascript
function(){
    try{
        //查找 DOM 节点
        const p =document.querySelector('.p')
        p.style.color = 'red'
    } catch(error){
        //try 代码段中执行有错误时，会执行 catch 代码段
        //查看错误信息
        console.log(error.message)
        //终止代码运行
        return
    }
    finally {
        alert('执行')
    }
    console.log('如果出现错误，我的语句不会执行')
}
foo()

```

**总结**

1. try...catch用于捕获错误信息
2. 将预估可能发生错误的代码写在try代码段中
3. 如果try代码段中出现错误后，会执行catch代码段，并截获到错误信息
4. finally不管是否有错误，都会执行

# 普通函数和箭头函数的this指向

## this指向-普通函数

普通函数的调用方式决定了this的值，即**谁调用this的值就指向谁**

普通函数没有明确调用时this的值为window，严格模式下没有调用者是this的值指向undefined

```javascript
'use strict'
function fn(){
    console.log(this)	//undefined
}
fn()
```

## this指向-箭头函数

箭头函数中的this与普通函数完全不同，也不受调用方式的影响，事实上**箭头函数中并不存在this！**

1. 箭头函数会默认帮我们绑定外层this的值，所以在箭头函数中this的值和外层的this是一样的
2. 箭头函数中this引用的就是最近作用域中的this
3. 向外层作用域中，一层层查找this，知道this的定义

**总结**

1. 函数内不存在this，沿用上一级的
2. 不适用于：构造函数，原型函数，dom事件函数
3. 适用于:需要使用上层this的地方
4. 使用正确的话，它会在很多地方带来方便，后面我们会大量使用慢慢体会

## 改变this

### call

#### 语法

```javascript
fun.call(thisArg,arg1,arg2)
//thisArg:在fun函数运行时指定的this值
//arg1,arg2:传递的其他参数
//返回值就是函数的返回值，因为它就是调用函数
```

### apply

#### 语法

```javascript
fun.apply(thisArg,[argArray])
//thisArg:在fun函数运行时指定的this值
//[argArray]:传递的值必须包含在数组里面
//返回值就是函数的返回值，因为它就是调用函数
//因此apply主要跟数组有关系，比如用Math。max()求数组的最大值
```

### bind

bind()方法不会调用函数，但是能改变this的指向

#### 语法

```javascript
fun.bind(thisArg,arg1,arg2,...)
//thisArg:在fun函数运行时指定的this值
//arg1,arg2:传递的其他参数
//返回由指定的this值和初始化参数改造的原函数拷贝(新函数)
//因此当我们只想改变this指向,并且不想调用这个函数的时候,可以使用bind,比如改变定时器内部的this指向
```

### 总结

#### 相同

都可以改变函数内部this的指向

#### 区别

call和apply会调用函数,并且改变函数内部的this指向

call和apply传递的参数不一样,call传递的是arg1,arg2...形式,apply必须数组形式[arg]

bind不会调用函数

#### 主要应用场景

call 调用函数并且可以传递参数

apply经常跟数组有关系,比如借助数学对象实现数组最大值最小值

bind不调用函数,但是还想改变this指向,比如改变定时器内部的this指向

# 防抖动

单位时间内，频繁触发事件,**只执行最后一次**

## 使用场景

搜索框搜索输入.只需要用户最后一次输入完,再发送请求

手机号,邮箱验证输入检测

## 实现方式

1. lodash提供防抖处理
2. 手写一个防抖函数来处理

### lodash

1. 引入lodash库
2. _.debounce(函数,延时时长ms)

### 手写

```javascript
//1.声明定时器变量
//2.事件触发的时候都要先判断是否有定时器，如果有先清楚以前的定时器
//3.如果没有定时器,则开启定时器,存入定时器变量里面
//4.定时器里面写函数调用
function debounce(fn,t){
    let timer
    //return 返回一个匿名函数
    return function(){
        //2,3,4
        if(timer)clearTimeout(timer)
        timer = setTimeout(function(){
            fn()//加小括号调用fn函数
        },t)
    }
}
box.addEventListener('mousemove',debounce(mouseMove,500))
```

# 节流

单位时间内,频繁触发事件,只执行一次

```javascript
//节流的核心就是利用定时器(setTimeout)来实现
//1.声明一个定时器变量
//2.当鼠标每次滑动都先判断是否有定时器了，如果有定时器则不开启新的定时器
//3.如果没有定时器,则开启定时器,记得存到定时器变量里
//3.1定时器里面调用执行的函数
//3.2定时器里面要把定时器清空
function throttle(fn,t){
    let timer = null
    return function(){
        if(!timer) {
            timer = setTimeout(function(){
                fn()
                //清空定时器
                timer = null 
            },t)
        }
    }
}
box.addEventListener('mousemove',throttle(mouseMove,500))
```

