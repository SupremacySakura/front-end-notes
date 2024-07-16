# Vue2

## **Vue**是什么

概念:Vue是一个用于 **构建用户界面** **渐进式** *框架*

1. 构建用户界面:基于**数据**动态**渲染**界面
2. 渐进式:**循序渐进**的学习
3. 框架:一套完整的项目解决方案,**提升开发效率**

Vue的两种使用方式:

1. Vue核心包开发,场景:**局部**模块改造
2. Vue核心包&Vue插件 工程化开发,场景:**整站**开发

## 创建一个Vue实例

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

## 插值表达式

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

## Vue响应式特性

### 什么是响应式

**数据改变,视图自动更新**

使用Vue开发→专注于**业务核心逻辑**即可

### 如何访问或修改数据

data中的数据,最终会被添加到实例上

1. 访问数据:"实例.属性名"
2. 修改数据:"实例.属性名"="值"

## 指令

### 指令初识和v-html

#### Vue指令

Vue会根据不同的**指令**,针对标签实现不同的**功能**

指令:带有**v-前缀**的特殊**标签属性**

```html
<div v-html='str'></div>
```

#### v-html

作用:设置元素的**innerHTML**

语法:v-html="表达式"

### v-show和v-if

#### v-show

1. 作用:控制元素显示隐藏
2. 语法:v-show="表达式"    表达式值**true显示**,**false隐藏**
3. 原理:**切换display:none**控制显示隐藏
4. 场景:频繁切换显示隐藏的场景

#### v-if

1. 作用:控制元素显示隐藏(**条件渲染**)
2. 语法:v-if="表达式"    表达式值**true显示**,**false隐藏**
3. 原理:基于条件判断,是否**创建**或**移除**元素节点
4. 场景:要么显示,要么隐藏,不频繁的切换场景

### 指令v-else和v-else-if

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

### 指令v-on

#### 内联语句

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

#### methods处理函数

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

#### 调用传参

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

### 指令v-bind

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

#### v-bind操作class

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

#### v-bind操作style

语法:	:style="**样式对象**"

```html
<div class="box" :style="{class属性名:class属性值,class属性名2:class属性值}"></div>
```

适用场景:某个具体属性的动态设置

### 指令v-for

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

#### v-for中的key

**key作用:**

给元素添加**唯一标识**,便于Vue进行列表项的**正确排序复用**.

**注意点:**

1. key的值只能是**字符串**或**数字类型**
2. key的值必须具有**唯一性**
3. 推荐使用**id**作为key(唯一),不推荐使用**index**作为key(会变化,不对应)

```html
<li v-for="(item,index) in xxx" :key="唯一值"></li>
```

### 指令v-model

1. 作用:给**表单元素**使用,**双向数据绑定**→可以快速**获取或设置**表单元素内容
   1. 数据变化→视图自动更新
   2. **视图**变化→**数据**自动更新
2. 语法:v-model='变量'

#### v-model应用于其他表单元素

常见的表单元素都可以用v-model绑定关联→快速**获取**或**设置**表单元素的值,它会根据控件类型自动选取正确的方法来更新元素

- 输入框 input:text→value
- 文本域 textarea→value
- 复选框 input:checkbox→checked
- 单选框 input:redio→checked
- 下拉菜单 select→value
- ...

#### v-model原理

**原理**:v-model本质上是一个**语法糖**.例如应用在输入框上,就是**value属性**和**input事件**的合写.

作用:提供数据的双向绑定

1. 数据变,视图跟着变**:value**
2. 视图变,数据跟着变**@input**

注意:**$event**用在模板中,获取事件的形参

```vue
<template>
	<div>
		<input v-model="msg" type="text">
        <input :value="msg" @input="msg=$event.target.value">
    </div>
</template>
```

#### 表单类组件封装&简化v-model简化代码

(1).表单类组件**封装**

1. **父传子**:数据 应该是父组件**props**传递过来的,v-model**拆解**绑定数据
2. **子传父**:监听输入,子传父传值给父组件修改

```vue
//父组件
<BaseSelect :cityId="selectId" @事件名="selectId=$event"></BaseSelect>
```

```vue
//子组件
<select :value="cityId" @change="handleChange">
    
</select>
```

```vue
//子组件
props:{
	cityId:string
}
```

```vue
methods:{
	handleChange(e){
		this.$emit('事件名',e.target.value)
	}
}
```

#### .sync修饰符

**作用**:可以实现**子组件**与**父组件数据**的**双向绑定**,简化代码

**特点**:prop属性名,可以**自定义**,并非固定为**value**

**场景**:封装弹框类的基础组件,**visible属性** true为显示 false为隐藏

**本质**:就是 **:属性名 **和 **@update:属性名** 合写

```vue
//父组件
<BaseDialog :visible.sync="isShow"></BaseDialog>
-------------------------------------------------
<BaseDialog :value="isShow" @update:visible="siShow=$event"></BaseDialog>
```

```vue
//子组件
props:{
	visible:Boolean
},
this.$emit('update:visible',false)
```

### 指令的修饰符

指令修饰符

通过"**.**"指明一些指令**后缀**,不同**后缀**封装了不同的处理操作→简化代码

1. 按键修饰符:**@keyup.enter**→键盘回车监听
2. v-model修饰符:**v-model.trim**→去除首位空格;**v-model.number**→转数字
3. 事件修饰符:@事件名.stop→阻止冒泡;@事件名.prevent→阻止默认行为

### 自定义指令

#### 全局自定义指令

Vue2:

```vue
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素挂载到 DOM 中时...
  inserted(el) {
    // 聚焦元素
    el.focus()
  }
})
```

Vue3:

```vue
const app = Vue.createApp({})
// 注册一个全局自定义指令 `v-focus`
app.directive('focus', {
  // 当被绑定的元素挂载到 DOM 中时...
  inserted(el) {
    // 聚焦元素
    el.focus()
  }
})
```

#### 局部自定义指令

```vue
directives: {
  focus: {
    // 指令的定义
    inserted(el) {
      el.focus();
    }
  }
}
```

##### 钩子函数

- `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新。
- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。
- `unbind`：只调用一次，指令与元素解绑时调用。

##### 钩子函数参数

- `el`：指令所绑定的元素，可以用来直接操作 DOM。

- `binding`：一个对象，包含以下 property：

  - `name`：指令名，不包括 `v-` 前缀。

  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。

  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。

  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。

  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。

  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。

- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-接口) 来了解更多详情。
- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。



## computed计算属性

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

### computed计算属性vs methods方法

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

### 计算属性完整写法

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

## watch

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

## 生命周期和生命周期的四个阶段

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

## 工程化开发和脚手架

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

## 组件化开发和根组件

**组件化**:一个页面可以拆分成**一个个组件**,每个组件都有着自己独立的**结构,样式,行为**.

​		好处:便于**维护**,利于**复用**→提升**开发效率**

​		组件分类:普通组件,根组件

**根组件**:整个应用最上层的组件,包含所有普通小组件

### App.vue文件(单文件组件)的三个组成部分

1. **语法高亮插件:**Vetur
2. **三部分组成**
   - template:结构(有且只有一个根元素)
   - script:js逻辑
   - style:样式(可支持less,需要装包)
3. **让组件支持less**
   - style标签,lang='less'开启less功能
   - 装包: **yarn add less less-loader**

## 普通组件的注册使用

### 局部注册

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

### 全局注册

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



## scoped样式冲突

**<style>**

全局样式(默认):影响所有组件

局部样式:scoped下样式,只作用与当前组件

**<script>**

el根实例独有,data是一个函数,其他配置项一致

**scoped原理?**

1. 当前组件内标签都被添加data-v-hash值的属性
2. css选择器都被添加[data-v-hash值]的属性选择器

最终效果:必须是当前组件的元素,才会有这个自定义属性,才会被这个样式作用到

## data是一个函数

一个组件的data选项必须是一个**函数**→保证每个组件实例,维护**独立**的一份数据对象

每次创建新的组件实例,都会新执行一次data函数,得到一个新对象

```vue
data () {
    return {
        count:100,
    }
},
```

## 组件通信

**什么是组件通信**

组件通信,就是指**组件与组件**之间的数据传递.

- 组件的数据是独立的,无法直接访问其他组件的数据
- 想用其他组件的数据→组件通信

### 父与子之间的组件通信

父子通信流程:

1. 父组件通过**props**将数据传递给子组件
2. 子组件利用**$emit**通知父组件更新

#### 父→子

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

##### prop

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

###### prop校验

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

###### prop&data,单向数据流

共同点:都可以给组件提供数据

区别:

- data的数据是**自己**的→随便改
- prop的数据是**外部**的→不能直接改,要遵循**单向数据流**

单向数据流:父级prop的数据更新,会向下流动,影响子组件.这个数据流动是单向的.

**口诀:谁的数据谁负责**

#### 子→父

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

### 非父子关系之间的组件通信

#### provide&inject

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



#### event bus

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



### 通用方案

#### vuex

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

##### 创建一个新仓库

1. yarn add vuex@3(安装vuex)
2. 新建store/index.js专门存放vuex(新建vuex模块文件)
3. Vue.use(Vuex),创建仓库new Vuex.Store()
4. 在main.js中导入挂载到vue实例上(main.js挂载)	

##### 核心概念-state 状态

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

##### 核心概念-mutations

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

##### 核心概念-actions

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

##### 核心概念-getters

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

##### 核心概念-模块module

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

## ref与$refs

**作用**:利用ref和$refs可以用于**获取dom元素**,或**组件实例**

**特点**:查找范围→**当前组件内(更精确稳定)**

(1)获取dom:

1.目标标签 - 添加ref属性

```vue
<div ref="chartRef">
    我是渲染图表的容器
</div>
```

2.恰当时机,通过this.$refs.xxx,获取目标标签

```vue
mounted(){
	console.log(this.$refs.chartRef)
}
```

(2)获取组件

1.目标组件 - 添加ref属性

```vue
<BaseForm ref="baseForm"></BaseForm>
```

2.恰当时机,通过this.$refs.xxx,获取目标组件,就可以调用组件对象里面的方法

```vue
this.$refs.baseForm.组件方法()
```

## 异步更新与$nextTick

**$nextTick**:**等DOM更新后**,才会触发执行此方法里的函数体

语法:this.$nextTick(函数体)

```vue
methods:{
	handleEdit:(){
		//1.显示输入框(异步dom更新)
		this.isShowEdit = true
		//2.让输入框聚焦
		this.$nextTick(()=>{
			console.log(this.$refs.inp)
			this.$refs.inp.focus()
		})
	}
}
```

**总结**:

1. Vue是异步更新DOM的
2. 想要在DOM更新完成之后做某件事,可以用`$nextTick`

## 插槽

### 默认插槽

作用:让组件内部的一些**结构**支持**自定义**

插槽基本语法:

1. 组件内需要定制的结构部分,改用`<slot></slot>`站位
2. 使用组件时,在标签内部传入结构替换slot

### 后备内容(默认值)

**插槽后备内容**:封装组件时,可以为预留的`<slot>`插槽提供**后备内容**(默认内容)

**语法**:在`<slot>`标签内容,放置内容,作为默认内容

**效果**:

- 外部使用组件时,不传东西,则slot会显示后备内容
- 外部使用组件时,传东西了,在slot整体会被替换掉

### 具名插槽

需求:一个组件内部有多处结构,需要外部传入标签,进行定制

默认插槽:一个的定制位置

**具名插槽简化语法**:

1.多个slot使用name属性区分名字

```vue
<div>
    <slot name="head"></slot>
</div>
<div>
    <slot name="body"></slot>
</div>
<div>
    <slot name="footer"></slot>
</div>
```

2.template配合v-slot:名字来分发对应标签

```vue
<MyDialog>
	<template #head>
    	大标题
    </template>
	<template #body>
    	内容
    </template>
	<template #footer>
    	底部
    </template>
</MyDialog>
```

3.**`v-slot:插槽名`**可以简化为**`#插槽名`**

### 作用域插槽

作用域插槽:定义slot插槽的同时,是可以传递值的,给插槽上可以绑定数据,将来使用组件时可以用.

**基本使用步骤**:

1.给slot标签,以添加属性的方式传值

```vue
<slot :id="item.id" msg="测试文本"></slot>
```

2.所有添加的属性,都会被收集到一个对象中

```vue
{id:3,msg:'测试文本'}
```

3.在template,通过`#插槽名="obj"`接收,默认插槽名为**default**

```vue
<MyTable :list="list">
	<template #default="obj">
    	<button @click="del(obj.id)">
            删除
        </button>
    </template>

</MyTable>
```



## 路由

### VueRouter的使用

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

### 路由的封装抽离

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

### 声明式导航

#### 导航链接

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

#### 两个类名

##### 使用类名

router-link会自动给当前导航添加两个高亮类名

(1)router-link-active 模糊匹配(用得到)

to="/my"可以匹配	/my	/my/b	/my/a	...

(2)router-link-exact-active 精确匹配

to="/my"可以匹配	/my

##### 定制类名

```javascript
const router = new VueRouter({
    routes:[...]
    linkActiveClass:"类名1"	//模糊匹配自定义类名
    linkExactActiveClass:"类名2"	//精确匹配自定义类名
})
```

#### 跳转传参

目标:在跳转路由时,进行传值

##### 查询参数传参

(1)语法格式如下

- to="/path**?参数名=值**"

(2)对应页面组件接收传递过来的值

- $route.query.参数名

###### 动态路由传参

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

###### 动态路由参数可选符

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



##### 两种传参的区别

(1)查询参数传参(比较适合传**多个参数**)

(2)动态路由传参(**优雅简洁**,传**单个参数**比较方便)

### Vue路由重定向

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

### Vue路由404

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

### Vue路由模式设置

问题:路由的路径看起来不自然,有#能否切换成真正的路径形式?

- hash路由(默认)    例如:http://localhost:8080/#/home
- history路由(常用)    例如:http://localhost:8080/home    (以后上线需要服务器支持)

### 编程式导航

#### 基本跳转

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

   

#### 路由传参

问题:点击搜索按钮,跳转需要传参如何实现

两种传参方式:查询参数+动态路由传参

两种跳转方式:对于两种传参方式都支持:

##### path路径跳转传参

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

##### name命名路由跳转传参

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

   

### 路由重复跳转报错问题解决

```javascript
//router/index.js
// 需要重写VueRouter.prototype原型对象身上的push|replace方法
// 先把VueRouter.prototype身上的push|replace方法进行保存一份
const originPush = VueRouter.prototype.push
const originReplace = VueRouter.prototype.replace
// 重写VueRouter.prototype身上的push方法了
VueRouter.prototype.push = function (location, resolve, reject) {
  // 第一个形参：路由跳转的配置对象（query|params）
  // 第二个参数：undefined|箭头函数（成功的回调）
  // 第三个参数:undefined|箭头函数（失败的回调）
  if (resolve && reject) {
    // push方法传递第二个参数|第三个参数（箭头函数）
    // originPush：利用call修改上下文，变为(路由组件.$router)这个对象，第二参数：配置对象、第三、第四个参数：成功和失败回调函数
    originPush.call(this, location, resolve, reject)
  } else {
    originPush.call(this, location, () => { }, () => { })
  }
}
// 重写VueRouter.prototype身上的replace方法了
VueRouter.prototype.replace = function (location, resolve, reject) {
  if (resolve && reject) {
    originReplace.call(this, location, resolve, reject)
  } else {
    originReplace.call(this, location, () => { }, () => { })
  }
}

```



## ESlint代码规范

**目标:认识代码规范**

代码规范:一套写代码的约定的规则,例如:"赋值符号左右是否需要空格","一句话结束是否需要加;"

老话说:"没有规矩不成方圆"→正规的团队需要统一的编码风格

JavaScript Standard Style 规范说明 *http://standardjs.com/rules-zhcn.html*

### 代码规范错误

ESlint会提示

**两种解决方案:**

1. **手动修正**:根据错误提示一项一项手动修正错误,如果不认识报错是什么意思,可以前往ESlint规则表查询错误原因
2. **自动修正**:基于VSCode插件ESlint高亮错误,并通过配置自动帮我们修复错误

注意:在VSCode中,插件无法帮你去除多余的逗号,但是可以帮你去除分号.也就是说,插件无法帮你一键去除所有错误,部分错误仍需手动修正

**自动修复配置**:

```javascript
// 当保存的时候,ESlint自动帮我们修复错误
"editor.codeActionsOnSave":{
    "source.fixAll":true
},
// 保存代码,不自动格式化
    "editor.formatOnSave":false
```

## json-server

**目标**:基于json-server工具,准备后端接口服务环境

1. 安装全局工具json-server(全局工具仅需要安装一次)(官网:*https://json-server.dev/*)    **yarn global add json-server** 或 **npm i json-server -g**
2. 代码根据目录新建一个db目录
3. 将资料index.json移入db目录
4. 进入db目录,执行命令,启动后端接口服务    json-server index.json
5. 访问接口测试

## 打包发布

**目标:明确打包的作用**

说明:vue脚手架只是开发过程中,协助开发的工具,当真正开发完了=>脚手架不参与上线

打包的作用:

1. 将多个文件压缩合成一个文件
2. 语法降级
3. less sass ts 语法解析
4. ....

打包后,可以生成,浏览器能够直接运行的网页=>需要上线的源码

### 命令

**说明**:vue脚手架工具已经提供了打包命令,直接使用即可

**命令**:yarn build

**结果**:在项目根目录会自动创建一个文件夹dist,dist中的文件就是打包后的文件,只需要放到服务器即可

**配置**:默认情况下,需要放到服务器根目录打开,如果希望双击运行,需要配置publicPath配成相对路径

```javascript
// vue.config.js
module.exports = defineConfig({
    publicPath:'./',
    transpileDependencies:true
})
```

### 路由懒加载

**目标:配置路由懒加载,实现打包优化**

**说明**:当打包构建应用时,JavaScript包会变得非常大,影响页面加载.如果我们能把不同路由对应的组件分割成不同的代码块,然后当路由**被访问时才加载对应组件**,这样就更加**高效**了

步骤1:异步组件改造

```javascript
//router
const ProDetail = ()=>import('@/views/prodetail') //改造后的
import Pay from '@/views/pay'//改造前的
...
```

步骤2:路由中应用

```javascript
const router = new VueRouter({
    routes:[
        { path:'/prodetail/:id',component: ProDetail },
        { path:'/pay',component: Pay },
        ...
    ]
})
```

# Vue3

## Vue3的优势

**更容易维护**:

1. 组合式API
2. 更好的TypeScript支持

**更快的速度**:

1. 重写diff算法
2. 模块编译优化
3. 更高效的组件初始化

**更小的体积**:

1. 良好的TreeShaking
2. 按需引入

**更优的数据响应式**:

1. Proxy

## 创建Vue3项目

(1).**前提环境条件**

​	**已安装16.0或更高版本的Node.js**

​	使用	node -v	查看版本

(2).**创建一个Vue应用**

​	**npm init vue@latest**

​	这一指令将会安装并执行create-vue

## 项目目录和关键文件

关键文件:

1. vite.config.js - 项目的配置文件 **基于vite的配置**
2. package.json - 项目包文件 **核心依赖变成了Vue3.x和vite**
3. main.js - 入口文件 **createApp函数创建应用实例**
4. app.vue - 根组件 **SFC单文件组件 script-template-style**
   - 变化一:脚本script和模板template顺序调整
   - 模板template不再要求唯一根元素
   - 脚本script添加setup标识支持组合式API
5. index.html - 单页入口 **提供id为app的挂载点**

## 组合式API

### setup选项

<script setup> 语法糖

**原始复杂写法**:

```vue
<script>
export default {
    setup(){
        //数据
        const message = 'this is message'
        //函数
        const logMessage = () => {
            console.log(message)
        }
        return {
            message,
            logMessage
        }
    }
}
</script>
```

**语法糖写法**:

```vue
<script setup>
//数据
    const message = 'this is message'
//函数
    const logMessage = () => {
        console.log(message)
    }
</script>
```

**setup选项中写代码特点**:

```vue
<template>
	<!-- 使用数据和方法 --!>
	{{ message }}
	<button @click="logMessage">
		log message
	</button>
</template>
```

**注意**:

setup

1. 执行时机,比beforeCreate还要早
2. setup函数中,获取不到this(this是undefined)
3. 数据 和 函数,需要在setup 最后 return,才能在模板中应用
4. 通过 setup 语法糖能够简化代码

### reactive()和ref()

对比:

1. reactive和ref函数的共同作用
   - **用函数调用的方式生成响应式数据**
2. reactive vs ref
   - **reactive不能处理简单类型数据**
   - ref参数类型支持更好但是必须通过.value访问修改
   - ref函数的内部实现依赖reactive函数
3. 在实际工作中推荐使用哪个
   - **推荐使用ref函数,更加灵活统一**

#### reactive()

**作用**:接受对象类型数据的参数传入并返回一个响应式的对象

**核心步骤**:

1. 从vue包中**导入 reactive 函数**
2. 在 <script setup> 中**执行 reactive 函数**并传入**类型为对象**的初始值,并使用变量接收返回的值

```vue
<script setup>
//导入
    import { reactive } from 'vue'
// 执行函数 传入参数 变量接收
	const state = reactive(对象类型数据)
</script>
```

#### ref()

**作用**:接收**简单类型或者对象类型**的数据并返回一个**响应式的对象**

**核心步骤**:

1. 从vue包中**导入 ref 函数**
2. 在 <script setup> 中**执行 ref 函数**并传入初始值,并使用**变量接收**返回的值

```vue
<script setup>
//导入
    import { ref } from 'vue'
// 执行函数 传入参数 变量接收
	const count = ref(简单类型或者复杂类型数据)
</script>
```

**注意**:ref:

1. 脚本中访问数据,需要通过.value
2. 在template中,.value不需要加

### computed计算属性函数

计算属性的基本思想和Vue2的完全一致,组合式API下的计算属性**只是修改了写法**



核心步骤:

1. **导入**computed函数
2. **执行函数**在回调参数中**return基于响应式数据做计算的值**,用变量接收

```vue
<script setup>
//导入
    import { computed } from 'vue'
// 执行函数 变量接收 在回调参数中return计算值
    const computedState = computed(() => {
        return 基于响应式数据做计算后的值
    })
</script>
```

**注意**:

1. 计算属性中不应该有"副作用"→比如**异步请求/修改dom**
2. 避免直接修改计算属性的值→**计算属性应该是只读的,特殊情况下可以配置 get set**

### watch

#### 基础使用 - 侦听单个数据

1. 导入watch函数
2. 执行watch函数传入要侦听的响应式数据(ref对象)和回调函数

```vue
<script setup>
//导入
    import { watch , fef } from 'vue'
    const count = ref(0)
//调用 watch 侦听变化
    watch(count,(newValue,oldValue) => {
        console.log(`count发生了变化,老值为${oldValue},新值为${newValue}`)
    })
</script>
```

#### 基础使用 - 侦听多个数据

```vue
<script setup>
//导入
    import { watch , fef } from 'vue'
    const count = ref(0)
    const name = ref('ls')
//调用 watch 侦听变化
    watch(
        [count,name],
        ([newCount,newName],[oldCount,oldName]) => {
        console.log(`count发生了变化,老值为${[oldCount,oldName]},新值为${[newCount,newName]}`)
    })
</script>
```

#### immediate和deep

说明:

(1).**immediate**:在侦听器创建是**立刻触发回调**,响应式数据变化后继续执行回调

```vue
<script setup>
//导入
    import { watch , fef } from 'vue'
    const count = ref(0)
//调用 watch 侦听变化
    watch(count,(newValue,oldValue) => {
        console.log(`count发生了变化,老值为${oldValue},新值为${newValue}`)
    },{
        immediate:true
    })
</script>
```

(2).**deep**:对数据进行深度监听,复杂数据类型必须深度监听才能成功

```vue
<script setup>
//导入
    import { watch , fef } from 'vue'
    const count = ref({
        number1:0,
        number2:2
    })
//调用 watch 侦听变化
    watch(count,(newValue,oldValue) => {
        console.log(`count发生了变化,老值为${oldValue},新值为${newValue}`)
    },{
        deep:true
    })
</script>
```

#### 精确侦听对象的某个属性

需求:在不开启deep的前提下,侦听age的变化,只有age变化时才执行回调

```vue
const info = ref({
	name:'cp',
	age:18
})

watch(
	() => info.value.age
	(newValue,oldValue) => console.log('age发送了变化')
)
```



### 生命周期函数API

|      选项式API       |    组合式API    |
| :------------------: | :-------------: |
| beforeCreate/created |      setup      |
|     beforeMount      |  onBeforeMount  |
|       mounted        |    onMounted    |
|     beforeUpdate     | onBeforeUpdate  |
|       updated        |    onUpdated    |
|    beforeUnmount     | onBeforeUnmount |
|      unmounted       |   onUnmounted   |

```vue
<script setup>
import { onMounted } from 'vue'
    onMounted(() => {
        console.log('mounted生命周期函数-逻辑1')
    })
     onMounted(() => {
        console.log('mounted生命周期函数-逻辑2')
    })
</script>
```

### 组合式API下的父子通信

#### 组合式API下的父传子

基本思想:

1. 父组件中给**子组件绑定属性**
2. 子组件内部通过**props选项接收**

```vue
<script setup>
//引入子组件
    import sonComVue from './son-com.vue'
</script>
<template>
<!-- 1.绑定属性 message --!>
<sonComVue message='this is app mess' />
</template>
```

```vue
<script setup>
// 2.通过definProps "编译器宏" 接收子组件传递的数据
    const props = defineProps({
        message:String
    })
</script>
<template>
	{{ message }}
</template>
```

#### 组合式API下的子传父

基本思想:

1. 父组件中给**子组件标签通过@绑定事件**
2. 子组件内部通过**emit方法触发事件**

```vue
<script setup>
//引入子组件
    import sonComVue from './son-com.vue'
    const getMessage = (msg) => {
        console.log(msg)
    }
</script>
<template>
<!-- 1.绑定自定义事件 message --!>
<sonComVue message='this is app mess' @get-message="getMessage" />
</template>
```

```vue
<script setup>
// 2.通过definEmits编译器宏生成emit方法
    const props = defineProps({
        message:String
    })
    const emit = defineEmits(['get-message'])
    const sendMsg = () => {
        // 3.触发自定义事件并传递参数
        emit('get-message',"this is son's msg")
    }
</script>
<template>
	{{ message }}
	<button @click="sendMsg">
        sendMsg
    </button>
</template>
```

### 模板引用和defineExpose宏函数

#### 模板引用

概念:通过**ref标识**获取真实的**dom对象或者组件实例对象**

时机:**组件挂载完毕**

```vue
<script setup>
import { ref } from 'vue'
//1.调用ref函数得到refduix
    const h1Ref = ref(null)
</script>

<template>
	<!-- 2.通过ref标识绑定ref对象 --!>
	<h1 ref="h1Ref">我是dom标签</h1>
</template>
```

#### defineExpose()

默认情况下在<script setup>语法糖下**组件内部的属性和方法是不开放**给父组件访问的,可以通过defineExpose编译宏**指定哪些属性和方法允许访问**

```vue
<script setup>
import { ref } from 'vue'
const testMessage = ref('this is test msg')
defineExpose({
    testMessage
})
</script>
```

### provide & inject

#### 跨层传递普通数据

1. 顶层组件通过**provide函数提供**数据
2. 底层组件通过**inject函数获取**数据

顶层组件

```vue
provide('key','顶层组件中的数据')
```

底层组件

```vue
const message = inject('key')
```

#### 跨层传递方法

顶层组件可以向底层组件传递方法,**底层组件调用方法修改顶层组件中的数据**

```vue
const setCount = () => {
	count.value++
}
provide('setCount-key',setCount)
```

```vue
const setCount = inject('setCount-key')
```

### Vue3.3新特性 - defineOptions

背景说明:

有<script setup>之前,如果要定义 props,emits 可以轻而易举的添加一个与setup平级的属性.但是用了<script setup>之后,就没法这么干了,因为setup属性已经没有了,自然无法添加与其平级的属性.

为了解决这一问题,引入了defineProps 与 defineEmits 这两个宏,单这只解决了 props 与 emits 这两个属性.如果我们要定义组件的name或其他自定义的属性,还是得回到最原始的用法------在添加一个普通的<script>标签.这样就会存在两个<script>标签,显然这并不合理.

所以在Vue3.3中新引入了 defineOptions 宏.顾名思义,主要用来定义 Options API 的选项.可以提包费defineOptions定义任意的选项,props,emits,slots除外(因为这些可以使用defineXXX来做到)

```vue
<script setup>
defineOptions({
    name:'Foo',
    inheritAttrs:false
    // ... 更多自定义属性
})
</script>
```

### Vue3.3新特性 - defineModel

在Vue3中,自定义组件上使用v-model,相当于传递一个modelValue属性,同时触发update:modelValue事件

```vue
<child v-model="isVisible"></child>
//相当于
<child :modelValue="isVisible" @update:modelValue="isVisible=$event"></child>
```

我们需要先定义props,再定义emit.其中有许多重复的代码.如果需要修改此值,还需要手动调用emit函数,这显然过于复杂,所以我们引入defineModel来简化我们的代码.

```vue
<script setup>
const modelValue = defineModel()
modelValue.value++
</script>
```

## Pinia

### 什么是Pinia

Pinia是Vue的最新的**状态管理工具**,是Vuex的**替代品**

1. 提供更加简单的API(去掉了Mutations)
2. 提供符合,组合式风格的API(和Vue3新语法统一)
3. 去掉了modules的概念,每一个store都是一个独立的模块
4. 配合TypeScript更加友好,提供可靠的类型判断

### 手动添加Pinia到Vue项目

1. 使用Vite创建一个空的Vue3项目

   npm create vue@latest

2. **按照官方文档**安装Pinia到项目中

   *https://pinia.vuejs.org/zh/getting-started.html*

### Pinia的基本语法

```javascript
export const useCounterStore = defineStore('counter',() => {
    //声明数据 state - count
    const count = ref(100)
    
    // 声明操作数据的方法 action (普通函数)
    const addCount = () => count.value++
    const subCount = () => count.value--
    // 异步函数
    const fetchUserPreferences = async () => {
        const res = await axios.get('/AllCarbonAccounting/passAuditOrNot')
    }
    //声明基于数据派生的计算属性 getters (computed)
    const double =computed(() => count.value*2)
    
    return {
        count,
        addCount,
        subCount,
        double
    }
})
```

### storeToRefs方法

Pinia的数据直接结构,数据会丢失响应式,所以引入storeToRefs方法,处理数据

```vue
const { count, msg } = storeToRefs(counterStore)
```

### 持久化插件

1. 安装插件 pinia-plugin-persistedstate 

   npm i pinia-plugin-persistedstate

2. main.js使用

3. store仓库中,persist:true开启

   ```
   import persist from 'pinia-plugin-persistedstate'
   //...
   app.use(createPinia().use(persist))
   ```

   

## Router

### 基础使用

**router/index.ts**

```ts
import { createRouter, createWebHistory } from 'vue-router'
//导入页面
import Home from '@/views/TheHomePage.vue'
import Article from '@/views/TheArticlePage.vue'

export const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/home',
      name: 'home',
      component: Home
    },
    {
      path: '/article',
      name: 'article',
      component: Article
    },
    {
      path:'/',redirect:'/home'
    }

  ]
})
```

**main.ts**

```ts
import { createApp } from 'vue'
import {router} from './router/index'
import App from './App.vue'


const app = createApp(App)

app.use(router)
app.mount('#app')

```

**App.vue**

```vue
<script setup lang="ts">
import { RouterView } from 'vue-router'
import TheTab from '@/components/TheTab.vue'
</script>

<template>
  <header>
    <TheTab></TheTab>
  </header>
  <RouterView></RouterView>

</template>

<style scoped>

</style>

```

**TheTab.vue**

```vue
<script setup lang="ts">
//导入useRouter函数
import { useRouter } from 'vue-router'
const router = useRouter()

//导航栏
//导航列表类
class tabListClass {
    id:number //导航ID
    label:string //导航名
    src:string //跳转地址
    constructor(id:number,label:string,src:string){
        this.id=id
        this.label=label
        this.src=src
    }
}
//导航列表数组
const tabList = [
    new tabListClass(0 , '文章' , 'article' ),
    new tabListClass(1 , '主页' , 'home' ),
    ]
//跳转页面函数
const turnToPage = (src:string)=>{
    router.push(src)
}
</script>

<template>
    <div>
        <div v-for="item in tabList" :key="item.id" @click="turnToPage(item.src)">{{ item.label }}</div>
        
    </div>
</template>

<style scoped></style>

```

