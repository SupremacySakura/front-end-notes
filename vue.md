

# **Vue**是什么

概念:Vue是一个用于 **构建用户界面** **渐进式** *框架*

1. 构建用户界面:基于**数据**动态**渲染**界面
2. 渐进式:**循序渐进**的学习
3. 框架:一套完整的项目解决方案,**提升开发效率**

Vue的两种使用方式:

1. Vue核心包开发,场景:**局部**模块改造
2. Vue核心包&Vue插件 工程化开发,场景:**整站**开发

# 创建一个Vue实例

创建Vue实例,初始化渲染:

1. 准备容器

2. 引包(官网)-**开发版本**/生产版本

3. 创建Vue实例 new Vue()

4. 指定配置项→渲染数据:

   a.	el指定挂载点

   b.	data提供数据

```html
<body>
    <div id='app'>
        <!--这里将来会编写一些用于渲染的代码逻辑-->
        {{msg}}
    </div>
    
    
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        //一旦引入VueJS核心包,在全局环境,就有了Vue构造函数
        const app = new Vue({
            //通过el配置选择器,指定Vue管理的是哪个盒子
            el:'#app',
            //通过data提供数据
            data:{
                msg:'Hello黑马'
            }
        })
    </script>
    
</body>
```

# 插值表达式

插值表达式	{{}}

插值表达式是一种Vue的模板语法

1. **作用**:利用表达式进行插值,渲染到页面.	表达式:是可以被求值的代码,JS引擎会将其计算出一个结果
2. **语法**:{{表达式}}
3. 注意点:(1)使用的数据必须存在(data);(2)支持的是表达式,而非语句,比如:	if	for...;(3)不能在标签属性中使用{{}}插值	

```html
<h3>{{title}}</h3>
<p>{{nickname.toUpperCase()}}</p>
<p>{{age>=18?'成年':'未成年'}}</p>
<p>{{obj.name}}</p>
```

# Vue响应式特性

## 什么是响应式

**数据改变,视图自动更新**

使用Vue开发→专注于**业务核心逻辑**即可

## 如何访问或修改数据

data中的数据,最终会被添加到实例上

1. 访问数据:"实例.属性名"
2. 修改数据:"实例.属性名"="值"

# 指令

## 指令初识和v-html

### Vue指令

Vue会根据不同的**指令**,针对标签实现不同的**功能**

指令:带有**v-前缀**的特殊**标签属性**

```html
<div v-html='str'></div>
```

### v-html

作用:设置元素的**innerHTML**

语法:v-html="表达式"

## v-show和v-if

### v-show

1. 作用:控制元素显示隐藏
2. 语法:v-show="表达式"    表达式值**true显示**,**false隐藏**
3. 原理:**切换display:none**控制显示隐藏
4. 场景:频繁切换显示隐藏的场景

### v-if

1. 作用:控制元素显示隐藏(**条件渲染**)
2. 语法:v-if="表达式"    表达式值**true显示**,**false隐藏**
3. 原理:基于条件判断,是否**创建**或**移除**元素节点
4. 场景:要么显示,要么隐藏,不频繁的切换场景

## 指令v-else和v-else-if

1. 作用:辅助v-if 进行判断渲染
2. 语法:v-else    v-else-if="表达式"
3. 注意:需要紧挨着v-if一起使用

eg.

```html
<div id="app">
    <p v-if="gender === 1">性别:男</p>
    <p v-else>性别:女</p>
    <hr>
    <p v-if="score>=90">成绩评定A:奖励电脑一台</p>
    <p v-else-if="score>=70">成绩评定B:奖励周末</p>
    <p v-else-if="score>=60">成绩评定C:奖励零食</p>
    <p v-else>成绩评定D:惩罚一周不能玩手机</p>
</div>
```

## 指令v-on

### 内联语句

1. 作用:注册事件=**添加监听**＋**提供处理逻辑**
2. 语法:v-on:事件名="内联语句"	v-on:事件名="methods中的函数名"
3. 简写:**@事件名**

```html
<button v-on:click="count++">
    按钮
</button>
```

```html
<button @click="count++">
    按钮
</button>
```

### methods处理函数

```html
<button @click="fn">
    -
</button>
```

```javascript
const app = new Vue({
    el:"#app",
    data:{
        //提供数据
        count:100
    },
    methods:{
        //提供处理逻辑函数
        fn(){
            console.log('提供逻辑代码')
        }
    }
})
```

### 调用传参

```html
<button @click="fn(参数1,参数2)">
    按钮
</button>
```

```javascript
const app = new Vue({
    el:"#app",
    methods:{
        fn(a,b){
            console.log('这是一个fn函数')
        }
    }
})
```

## 指令v-bind

1. 作用:动态的设置html的**标签属性**→src,url,title...
2. 语法:v-bind:**属性名**="表达式"
3. 注意:简写形式**:属性名="表达式"**

```html
<div id="app">
    <img v-bind:src='url'>
</div>
```

```javascript
const app = new Vue({
    el:"#app",
    data:{
        url:'图片路径'
    }
})
```

### v-bind操作class

v-bind对于样式控制的增强-操作class

语法:	**:class="对象/数组"**

1.**对象**→键就是类名,值是布尔值.如果值为**true**,有这个类,否则没有这个类

```html
<div class="box" :class="{类名1:布尔值,类名2:布尔值}"></div>
```

适用场景:一个类名,来回切换

2.**数组**→数组中所有的类,都会添加到盒子上,本质就是一个**class列表**

```html
<div class="box" :class="[类名1,类名2,类名3]"></div>
```

适用场景:批量添加或删除类

### v-bind操作style

语法:	:style="**样式对象**"

```html
<div class="box" :style="{class属性名:class属性值,class属性名2:class属性值}"></div>
```

适用场景:某个具体属性的动态设置

## 指令v-for

1. 作用:基于**数据**循环,**多次**渲染整个数据→**数组**,对象,数字...
2. 遍历数组语法:v-for="(item,index) in 数组",item:每一项,index:下标

``` html
<p v-for="...">
    我是一个内容
</p>
```

```html
<p>
    我是一个内容
</p>
<p>
    我是一个内容
</p>
<p>
    我是一个内容
</p>
```

### v-for中的key

**key作用:**

给元素添加**唯一标识**,便于Vue进行列表项的**正确排序复用**.

**注意点:**

1. key的值只能是**字符串**或**数字类型**
2. key的值必须具有**唯一性**
3. 推荐使用**id**作为key(唯一),不推荐使用**index**作为key(会变化,不对应)

```html
<li v-for="(item,index) in xxx" :key="唯一值"></li>
```

## 指令v-model

1. 作用:给**表单元素**使用,**双向数据绑定**→可以快速**获取或设置**表单元素内容
   1. 数据变化→视图自动更新
   2. **视图**变化→**数据**自动更新
2. 语法:v-model='变量'

### v-model应用于其他表单元素

常见的表单元素都可以用v-model绑定关联→快速**获取**或**设置**表单元素的值,它会根据控件类型自动选取正确的方法来更新元素

- 输入框 input:text→value
- 文本域 textarea→value
- 复选框 input:checkbox→checked
- 单选框 input:redio→checked
- 下拉菜单 select→value
- ...

# 指令的修饰符

指令修饰符

通过"**.**"指明一些指令**后缀**,不同**后缀**封装了不同的处理操作→简化代码

1. 按键修饰符:**@keyup.enter**→键盘回车监听
2. v-model修饰符:**v-model.trim**→去除首位空格;**v-model.number**→转数字
3. 事件修饰符:@事件名.stop→阻止冒泡;@事件名.prevent→阻止默认行为

# computed计算属性

**计算属性**

**概念**:基于**现有的数据**,计算出来的**新属性**.**依赖**的数据变化,**自动**重新计算

**语法**:

1. 声明在**computed配置项**,一个计算属性对应一个函数
2. 使用起来和普通属性一样使用{{**计算属性名**}}

```javascript
data:{
    list:[
        {id:1,name:'篮球',num:1},
        {id:2,name:'玩具',num:2},
        {id:3,name:'铅笔',num:5},
    ]
},
    computed:{
        计算属性名(){
            基于现有数据,编写求值逻辑
            return 结果
        }
    },
```

## computed计算属性vs methods方法

**computed 计算属性:**

**作用**:封装了一段对于**数据**的处理,求得一个结果.

**语法:**

1. 卸载**computed**配置项中
2. 作为属性,直接使用→**this.计算属性**    {{计算属性}}

**methods方法:**

**作用**:给实例提供一个**方法**,调用以处理**业务逻辑**

**语法:**

1. 写在**methods**配置项中
2. 作为方法,需要调用→**this.方法名()**    {{**方法名()**}}    @事件名="**方法名**"

**缓存特性(提升性能)**:

计算属性会对计算出来的**结果缓存**,再次使用直接读取缓存,

依赖项变化了,会**自动**重新计算→并**再次缓存**

## 计算属性完整写法

计算属性默认的简写,只能读取访问,**不能"修改"**

如果要**"修改"**→需要写计算属性的**完整写法**

```javascript
computed:{
    计算属性名:{
        get(){
            一段代码逻辑(计算逻辑)
            return 结果
        },
        set(修改的值){
            一段代码逻辑(修改逻辑)
        } 
    }
}
```

# watch

**watch侦听器(监视器)**

作用:**监视数据变化**,执行一些业务逻辑或异步操作.

语法:

1. **简单写法→简单数据类型,直接监视**
2. 完整写法→添加额外配置项

``` javascript
data:{
    words:'苹果'
    obj:{
        words:'苹果'
    }
},
    watch:{
        //该方法会在数据变化时,触发执行
        数据属性名(newValue,oldValue){
            一些业务逻辑或异步操作
        },
            '对象.属性名'(newValue,oldValue){
                一些业务逻辑或异步操作
            }
    }
```

完整写法→添加额外配置项

1. deep:true对复杂类型进行深度监视
2. immediate:true初始化立刻执行一次handler方法

``` javascript
data:{
    obj:{
        words:'苹果',
        lang:'Italy'
    },
},
    watch:{
        //watch完整写法
        数据属性名:{
            deep:true,
                immediate:true,
                handler(newValue){
                console.log(newValue)
            }
        }
    }
```

# 生命周期和生命周期的四个阶段

思考:什么时候可以发送**初始化渲染请求**?(越早越好)什么时候可以开始**操作dom**?(至少dom得渲染出来)

Vue生命周期:一个Vue实例从**创建**到**销毁**的整个过程

生命周期的四个阶段:

1. 创建
2. 挂载
3. 更新
4. 销毁

|    before Create    |      created       |   before Mount    | mounted |       before Update        | updated |             before Destroy              | destroyed |
| :-----------------: | :----------------: | :---------------: | :-----: | :------------------------: | :-----: | :-------------------------------------: | :-------: |
| 创建阶段,响应式数据 |                    | 挂载阶段,渲染模板 |         | 更新阶段,修改数据,更新视图 |         |            销毁阶段,销毁实例            |           |
|                     | 发送初始化渲染请求 |                   | 操作dom |                            |         | 释放Vue以外的资源(消除定时器,延时器...) |           |

# 工程化开发和脚手架

**工程化开发**&**脚手架Vue CLI**

**基本介绍:**

Vue CLI 是Vue官方提供的一个**全局命令工具**

可帮助我们**快速创建**一个开发Vue项目的**标准化基础架子**.[集成了webpack配置]

**好处:**

1. 开箱即用,零配置
2. 内置babel等工具
3. 标准化

**使用步骤:**

1. 全局安装(一次):**yarn global add @vue/cli** 或 **npm i @vue/cli -g**
2. 查看Vue版本:**vue --version**
3. 创建项目架子:vue create project-name(项目名-不能用中文)
4. 启动项目:**yarn serve** 或 **npm run serve**(找package.json)

**脚手架目录文件介绍&项目运行流程**

|                   |                                                 |
| ----------------- | ----------------------------------------------- |
| --node.modules    | 第三方包文件夹                                  |
| --public          | 放html文件的地方                                |
| ----favicon.ico   | 网站图标                                        |
| ----index.html    | index.html模板文件                              |
| --src             | 源代码目录→以后写代码的文件夹                   |
| ----assets        | 静态资源目录→存放图片,字体等                    |
| ----components    | 组件目录→存放通用组件                           |
| ----App.vue       | App根组件→项目运行看到的内容就在这里编写        |
| ----main.js       | 入口文件→打包或运行,第一个执行的文件            |
| --.gitignore      | git忽视文件                                     |
| --babel.config.js | babel配置文件                                   |
| --jsconfig.json   | js配置文件                                      |
| --package.json    | 项目配置文件→包含项目名,版本号,scripts,依赖包等 |
| --README.md       | 项目说明文档                                    |
| --vue.config.js   | vue-cli配置文件                                 |
| --yarn.lock       | yarn锁文件,由yarn自动生成,锁定安装版本          |

```JavaScript
//文件核心作用,导入App.vue,基于App.vue创建结构渲染index.html
//1.导入Vue核心包
import Vue from 'vue'

//2.导入App.vue根组件
import App form './App.vue'

//提示:当前属于什么环境(生产环境/开发环境)
Vue.config.productionTip = false

//3.Vue实例化,提供render方法→基于App.vue创建的结构渲染index.html
new Vue({
    render:h => h(App),
}).$mount('#app')
//el:'#app',作用:和$mount('选择器')作用一致,用于指定Vue所管理容器
//render:h => h(App),render:(createElement)=>{
//			return createElement(App)
//}
```

# 组件化开发和根组件

**组件化**:一个页面可以拆分成**一个个组件**,每个组件都有着自己独立的**结构,样式,行为**.

​		好处:便于**维护**,利于**复用**→提升**开发效率**

​		组件分类:普通组件,根组件

**根组件**:整个应用最上层的组件,包含所有普通小组件

## App.vue文件(单文件组件)的三个组成部分

1. **语法高亮插件:**Vetur
2. **三部分组成**
   - template:结构(有且只有一个根元素)
   - script:js逻辑
   - style:样式(可支持less,需要装包)
3. **让组件支持less**
   - style标签,lang='less'开启less功能
   - 装包: **yarn add less less-loader**

# 普通组件的注册使用

## 局部注册

**注册组件的两种方式:**

1. **局部注册:只能在注册的组件内使用**
   - 创建vue文件(三个组成部分)
   - 在使用的组件内导入并注册
2. 全局注册:所有的组件内都能使用

**使用:**

当成html标签使用**<组件名></组件名>**

**注意:**

组件名规范→大驼峰命名法,如HmHeader

```vue
//App.vue

//导入需要注册的组件
//import 组件对象 from '.vue文件路径'
import HmHeader from './components/HmHeader'

export default {
    //局部注册
    components:{
        '组件名':组件对象,
        HmHeader:HmHeader
    }
}
```

## 全局注册

**注册组件的两种方式:**

1. 局部注册:只能在注册的组件内使用
2. **全局注册:所有的组件内都能使用**
   - 创建.vue文件(三个组成部分)
   - **main.js**中进行全局注册

**使用:**

当成html标签使用**<组件名></组件名>**

**注意:**

组件名规范→大驼峰命名法,如HmHeader

```javascript
//main.js

//导入需要全局注册的组件
import HmButton form '/components/HmButton'

//调用 Vue.component进行全局注册
//Vue.component('组件名',组件对象)
Vue.component('HmButton',HmButton)
```

**技巧:**

一般使用**局部注册**,如果发现确实是**通用组件**,再抽离到全局

# scoped样式冲突

**<style>**

全局样式(默认):影响所有组件

局部样式:scoped下样式,只作用与当前组件

**<script>**

el根实例独有,data是一个函数,其他配置项一致

**scoped原理?**

1. 当前组件内标签都被添加data-v-hash值的属性
2. css选择器都被添加[data-v-hash值]的属性选择器

最终效果:必须是当前组件的元素,才会有这个自定义属性,才会被这个样式作用到

# data是一个函数

一个组件的data选项必须是一个**函数**→保证每个组件实例,维护**独立**的一份数据对象

每次创建新的组件实例,都会新执行一次data函数,得到一个新对象

```vue
data () {
    return {
        count:100,
    }
},
```

# 组件通信

**什么是组件通信**

组件通信,就是指**组件与组件**之间的数据传递.

- 组件的数据是独立的,无法直接访问其他组件的数据
- 想用其他组件的数据→组件通信

## 父与子之间的组件通信

父子通信流程:

1. 父组件通过**props**将数据传递给子组件
2. 子组件利用**$emit**通知父组件更新

### 父→子

父组件通过**props**将数据传递给子组件

```vue
//父组件
<template>
<Son :title="myTitle"></Son>
</template>


<script>
    import Son form './components/Son.vue'
    export default {
        data(){
            return {
                myTitle:'学前端,来黑马'
            }
        }
    }
</script>
```

```vue
//子组件
<template>
<div>
我是Son组件{{title}}    
</div>
</template>


<script>
   props:['title']
</script>
```

#### prop

prop定义:**组件上**注册的一些**自定义属性**

prop作用:向子组件传递数据

特点:

- 可以传递**任意数量**的prop
- 可以传递**任意类型**的prop

```vue
//父组件
<template>
	<div>
    	<UserInfo
        	:username="username"
            :age="age"
            :isSingle="isSingle"      
            :car="car"
            :hobby="hobby"      
         ></UserInfo>
	</div>
</template>


<script>
    import UesrInfo form './components/UesrInfo.vue'
    export default {
        data(){
            return {
              username:'小帅',
              age:28,
              isSingle:true,
              car:{
                  brand:'宝马',
              },
              hobby:['篮球','足球','羽毛球']
            }
        }
    }
</script>
```

```vue
//子组件
<template>
<div class="userinfo">
	<h3>我是个人信息组件</h3>
    <div>
        姓名:{{username}}
        年纪:{{age}}
        是否单身:{{isSingle}}
        座驾:{{car.brand}}
        兴趣爱好:{{hobby.jion(',')}}
    </div>
</div>
</template>


<script>
   props:['username','age','isSingle','car','hobby']
</script>
```

##### prop校验

```vue
props:{
	校验的属性名:类型 //Number String Boolen...
},
```

```vue
props:{
	校验的属性名:{
		type:类型, //Number String Boolen...
		required:true,//是否必填
		default:默认值,//默认值
		validator(value){
			//自定义校验逻辑
			return 是否通过校验
		}
	}
}
```

##### prop&data,单向数据流

共同点:都可以给组件提供数据

区别:

- data的数据是**自己**的→随便改
- prop的数据是**外部**的→不能直接改,要遵循**单向数据流**

单向数据流:父级prop的数据更新,会向下流动,影响子组件.这个数据流动是单向的.

**口诀:谁的数据谁负责**

### 子→父

```vue
//父组件
<template>
<!-- 2.父组件监听事件 -->
<Son :title="myTitle" @changeTitle='changeTitle'></Son>
</template>


<script>
    import Son form './components/Son.vue'
    export default {
        data(){
            return {
                myTitle:'学前端,来黑马'
            }
        },
        methods:{
            //3.提供处理函数,形参中获取参数
            changeTitle(newTitle){
                this.myTitle=newTitle
            }
        }
    }
</script>
```

```vue
//子组件
<template>
<div>
	我是Son组件{{title}}
    <button @click="handleClick">修改title</button>
</div>
</template>


<script>
   props:['title'],
   methods:{
       handleClick(){
           //1.$emit触发事件,给父组件发送消息通知
           this.$emit('changeTitle','传智教育')
       }
   }
</script>
```

## 非父子关系之间的组件通信

### provide&inject

provide&inject作用:**跨层级**共享数据

1.父组件provide提供数据

```vue
export default {
	provide(){
		return {
			//普通类型[非响应式]
			color:this.color
			//复杂类型[响应式]
			userInfo:this.userInfo
		}
	}
}
```

2.子/孙组件inject取值使用

```vue
export default {
	inject:['color','userInfo'],
	created(){
		console.log(this.color,this.userInfo)
	}
}
```



### event bus

作用:非父子组件之间,进行简易的消息传递.(复杂场景→vuex)

1.创建一个都能访问到的事件总线(空vue实例)→utils/EventBus.js

```javascript
import Vue from 'vue'
const Bus = new Vue()
export default Bus
```

2.A组件(接收方),监听**Bus实例**的事件

```vue
created () {
	Bus.$on('sendMsg',(msg) => {
		this.msg = msg
	})
}
```

3.B组件(发送方),触发Bus实例的事件

```vue
Bus.$emit('sendMsg','这是一个消息')
```



## 通用方案

### vuex

1.是什么:

vuex是一个**状态管理工具**,状态就是数据.

vuex是一个插件,可以帮我们**管理vue通用的数据(多组件共享的数据)**

2.场景:

- 某个状态在**很多个组件**来使用(个人信息)
- 多个组件**共同维护**一份数据(购物车)

3.优势:

- 共同维护一份数据,**数据集中化管理**
- **响应式变化**
- 操作简洁(vuex提供了一些辅助函数)

#### 创建一个新仓库

1. yarn add vuex@3(安装vuex)
2. 新建store/index.js专门存放vuex(新建vuex模块文件)
3. Vue.use(Vuex),创建仓库new Vuex.Store()
4. 在main.js中导入挂载到vue实例上(main.js挂载)	

#### 核心概念-state 状态

1.提供数据:

```javascript
//创建仓库
const store = new Vuex.Store({
    //state状态,即数据,类似于vue组件中的data
    //区别:
    //1.data是组件自己的数据
    //2.state是所有组件共享的数据
    state:{
        count:101
    }
})
```

2.使用数据

- 通过store直接访问

```text
获取 store
(1) this.$store
(2) import 导入 store

模板中:{{$store.state.xxx}}
组件逻辑中:this.$store.state.xxx
JS模块中:store.state.xxx
```

- **通过辅助函数(简化)**

mapState是辅助函数,帮助我们把store中的数据自动映射到组件的计算属性中

1. import { mapState } from 'vuex'
2. mapState(['count'])
3. computed:{...mapState(['count'])}

#### 核心概念-mutations

vuex同样遵循单向数据流,组件中不能直接修改仓库数据

通过strict:true可以开启严格模式

state的数据只能通过mutations修改

**基础使用**:

1.定义mutations对象,对象中存放修改state的方法

```javascript
const store = new Vuex.Store({
    state:{
        count:0
    },
    //定义mutations
    mutations:{
        //第一个参数是当前store的state属性
        addCount(state){
            state.count += 1
        }
    }
})
```

2.组件中提交调用mutations

```vue
this.$store.commit('addCount')
```

**传参使用:**

1.提供mutations函数

```javascript
const store = new Vuex.Store({
    state:{
        count:0
    },
    //定义mutations
    mutations:{
        //第一个参数是当前store的state属性
        addCount(state,n){
            state.count += n
        }
    }
})
```

2.页面提交调用mutation

```vue
this.$store.commit('addCount',10)
```

**注:**提交参数最多只能有一个,如果有多个参数,包装成一个对象提交

**辅助函数:mapMutations**

```javascript
  mutations:{
        //第一个参数是当前store的state属性
        addCount(state,n){
            state.count += n
        }
    }
```

```vue
import { mapMutations } from 'vuex'

methods:{
...mapMutations(['addCount'])
}
```

```vue
this.addCount(10)
```

#### 核心概念-actions

处理异步操作

需求:一秒钟之后,修改state的count成666

说明:**mutations必须是同步的(便于监测数据变化,记录调试)**

```javascript
mutations:{
    changeCount (state,newCount){
        state.count = newCount
    }
}
```

1.提供action方法

```javascript
action:{
    setAsyncCount (context,num){
        //一秒钟后,给一个数,去修改num
        setTimeout(()=>{
            context.commit('changeCount',num)
        },1000)
    }
}
```

2.页面中dispatch调用

```vue
this.$store.dispatch('setAsyncCount',666)
```

**辅助函数:mapActions**

```
action:{
    setAsyncCount (context,num){
        //一秒钟后,给一个数,去修改num
        setTimeout(()=>{
            context.commit('changeCount',num)
        },1000)
    }
}
```

```vue
import { mapActions } from 'vuex'

methods:{
...mapActions([' setAsyncCount'])
}
```

```vue
this.setAsyncCount(666)
```

#### 核心概念-getters

类似于计算属性

说明:除了state之外,有时我们还需要从state中派生出一些状态,这些状态是依赖state的,此时会用到getters

例如:state中定义了list,为1-10的数组,组件中,需要显示所有大于5的数据

```javascript
state:{
list:[1,2,3,4,5,6,7,8,9,10]
}
```

1.定义getters

```javascript
getters:{
    //注意:
    //(1)getters函数的第一个参数是state
    //(2)getters函数必须有返回值
    filterList(state){
        return state.list.filter(item=>item>5)
    }
}
```

2.访问getters

- 通过store访问getters

```vue
{{ $store.getters.filterList }}
```

- 通过**辅助函数mapGetters**映射

```vue
computed:{
...mapGetters(['filterList'])
},
```

```vue
{{ filterList }}
```

#### 核心概念-模块module

仓库分模块,避免store对象变得臃肿

**模块拆分:**

user模块:store/modules/user.js

```javascript
const state = {
    
}
const mutations = {}
const actions = {}
const getters = {}
export default {
    state,
    mutations,
    actions,
    getters
}
```

```javascript
import user from './modules/user'
const store = new Vuex.Store({
	modules:{
        user
    }
})
```

##### 模块-state

使用模块中的数据:

1. 直接用过模块名访问**$store.state.模块名.xxx**

2. 通过mapState映射

   默认根级别的映射 **mapState(['xxx'])**

   子模块的映射 **mapState('模块名',['xxx'])** - 需要开启命名空间

```javascript
export default {
    namespaced:true
    state,
    mutations,
    actions,
    getters
}
```

##### 模块-mutations

注意:模块中的mutations和actions会被挂载到全局,**需要开启命名空间**,才会被挂载到子模块.

1. 直接用过模块名访问**$store.commit('模块/xxx',额外参数)**

2. 通过mapMutations映射

   默认根级别的映射 **mapMutations(['xxx'])**

   子模块的映射 **mapMutations('模块名',['xxx'])** - 需要开启命名空间

##### 模块-getters

1. 直接用过模块名访问**$store.getters['模块名'/xxx]**

2. 通过mapGetters映射

   默认根级别的映射 **mapGetters(['xxx'])**

   子模块的映射 **mapGetters('模块名',['xxx'])** - 需要开启命名空间

##### 模块-actions

1. 直接用过模块名访问**$store.dispatch('模块/xxx',额外参数)**

2. 通过mapActions映射

   默认根级别的映射 **mapActions(['xxx'])**

   子模块的映射 **mapActions('模块名',['xxx'])** - 需要开启命名空间

# 路由

## VueRouter的使用

5个基础步骤(固定)

(1)下载:下载VueRouter模块到当前工程,版本3.6.5

```powershell
yarn add vue-router@3.6.5
```

(2)引入

```javascript
import VueRouter from 'vue-router'
```

(3)安装注册

```javascript
Vue.use(VueRouter)
```

(4)创建路由对象

```javascript
const router = new VueRouter()
```

(5)注入,将路由对象注入到new Vue实例中,建立关联

```javascript
new Vue({
	render:h => h(APp),
    router
}).$mount('#app')
```

2个核心步骤

(1)创建需要的组件(views目录),配置路由规则

```javascript
import Find from './views/Find.vue'
import My from './views/My.vue'
import Friend from './views/Friend.vue'

const router = new VueRouter({
    routes:[
        { path: './find',component: Find },
        { path: './my',component: My },
        { path: './friend',component: Friend },
    ]
})
```

(2)配置导航,配置路由出口(路径匹配的组件显示的位置)

```vue
<div>
    <a href="#/find">发现音乐</a>
    <a href="#/my">我的音乐</a>
    <a href="#/friend">朋友</a>
</div>
<div>
    <router-view></router-view>
</div>
```

**补充:**

组件分为**页面组件**和**复用组件**,便于维护

页面组件→views文件夹→配合路由,页面展示

复用组件→components文件夹→封装复用

## 路由的封装抽离

**原因**:所有的路由配置都堆在main.js中,不便于维护

**目标**:将路由模块抽离出来

**步骤**:

(1)在根目录新建router文件夹

(2)在文件夹中创建index.js文件

(3)配置index.js文件

```javascript
import Find from './views/Find.vue'
import My from './views/My.vue'
import Friend from './views/Friend.vue'
import VueRouter from vue-router
Vue.use(VueRouter)

const router = new VueRouter({
    routes:[
        { path: './find',component: Find },
        { path: './my',component: My },
        { path: './friend',component: Friend },
    ]
})
```

(4)配制main.js文件

```javascript
import router from './router/index.js'

new Vue({
    render:h => h(App)
    router	//简写,完整写法为 router:router
}).$mount('#app')
```

**补充**:基于**@**指代**src目录**,从src目录出发找组件

## 声明式导航

### 导航链接

需求:实现导航高亮效果

vue-router提供了一个全局组件router-link(取代a标签)

**作用**:

(1)**能跳转**,配置to属性指定路径(**必须**).本质还是a标签,**to无需#**

(2**)能高亮**,默认就会提供**高亮类名**,可以直接设置高亮样式

```vue
<div>
    <router-link to="/find">发现音乐</router-link>
    <router-link to="/my">我的音乐</router-link>
    <router-link to="/part">朋友</router-link>
</div>
```

### 两个类名

#### 使用类名

router-link会自动给当前导航添加两个高亮类名

(1)router-link-active 模糊匹配(用得到)

to="/my"可以匹配	/my	/my/b	/my/a	...

(2)router-link-exact-active 精确匹配

to="/my"可以匹配	/my

#### 定制类名

```javascript
const router = new VueRouter({
    routes:[...]
    linkActiveClass:"类名1"	//模糊匹配自定义类名
    linkExactActiveClass:"类名2"	//精确匹配自定义类名
})
```

### 跳转传参

目标:在跳转路由时,进行传值

#### 查询参数传参

(1)语法格式如下

- to="/path**?参数名=值**"

(2)对应页面组件接收传递过来的值

- $route.query.参数名

#### 动态路由传参

(1)配置动态路由

```javascript
const router = new VueRouter({
    routes:[
        ...,
        {
        	path:'/search/:word',
        	component:Search
        }
    ]
})
```

(2)配置导航链接

- to="/path/参数值"

(3)对应页面组件接收传递过来的值

- $route.params.参数名

##### 动态路由参数可选符

问题:配了路由path:"/search/:word",在未传参时会未匹配到组件,显示空白

原因: /search/:word 表示,必须要传参数.如果不传参数,也希望匹配,可以加个可选符"**?**"

```javascript
const router = new VueRouter({
    routes:[
        ...,
        {
        	path:'/search/:word?',
        	component:Search
        }
    ]
})
```



#### 两种传参的区别

(1)查询参数传参(比较适合传**多个参数**)

(2)动态路由传参(**优雅简洁**,传**单个参数**比较方便)

## Vue路由重定向

**问题**:网页打开,url默认是/路径,未匹配到组件时,会出现空白

**说明**:重定向→匹配path后,强制跳转path路径

语法:{path:匹配路径,redirect:重定向到的路径}

```javascript
const router = new VueRouter({
    routes:[
        ...,
        { path:'/',redirect:'/home' },
        {
        	path:'/search/:word?',
        	component:Search
        }
    ]
})
```

## Vue路由404

**作用**:当路径找不到匹配时,给个提示

**位置**:配置在路由后

**语法**:path:"*"(任意路径)-前面不匹配就命中最后这个

```javascript
import NotFind from '@/views/NotFind'

const router = new VueRouter({
    routes:[
        { path:'/',redirect:'/home' },
        { path:'/home',component:Home },
        { path:'/search/:words?',component:Search },
        { path:'*',component:NotFind }
    ]
})
```

## Vue路由模式设置

问题:路由的路径看起来不自然,有#能否切换成真正的路径形式?

- hash路由(默认)    例如:http://localhost:8080/#/home
- history路由(常用)    例如:http://localhost:8080/home    (以后上线需要服务器支持)

## 编程式导航

### 基本跳转

问题:点击按钮跳转如何实现?

编程式导航:用JS代码来实现跳转

两种语法:

1. path路径跳转(简易方便)

   ```javascript
   this.$router.push('路由路径')
   
   this.$router.push({
       path;'路由路径'
   })
   ```

2. **name命名跳转(适合path路径长的场景)**

   ```javascript
   this.$router.push({
       name:'路由名'
   })
   ```

   ```javascript
   { name:'路由名',path;'/path/xxx',component:xxx},
   ```

   

### 路由传参

问题:点击搜索按钮,跳转需要传参如何实现

两种传参方式:查询参数+动态路由传参

两种跳转方式:对于两种传参方式都支持:

#### path路径跳转传参

1. query传参

   ```javascript
   this.$router.push('/路径?参数名1=参数值1&参数名2=参数值2')
   
   this.$router.push({
       path:'/路径',
       query:{
           参数名1:'参数值1',
           参数名2:'参数值2'
       }
   })
   ```

2. 动态路由传参

   ```javascript
   this.$router.push('/路径/参数值')
   
   this.$router.push({
       path:'/路径/参数值'
   })
   ```

   获取值:$route.params.参数名(动态路由传参需要配置路由)

#### name命名路由跳转传参

1. query传参

   ```javascript
   this.$router.push({
       name:'路由名字',
       query:{
           参数名1;'参数值1',
           参数名2;'参数值2'
       }
   })
   ```

2. 动态路由传参

   ```javascript
   this.$router.push({
       name:'路由名字',
       params:{
           参数名:'参数值'
       }
   })
   ```

   
