# 鸿蒙软件开发

## TS基础

(1)TypeScript在JavaScript的基础上加入了静态类型检查功能,因此每一个变量都有固定的**数据类型**.

```typescript
let msg : string = 'hello world'
//let,声明变量的关键词,const则表示常量
//msg,变量名,自定义
//string,变量的数据类型
```

```typescript
// string : 字符串, 可以用单引号或者双引号
let msg:string = 'hello world'
//number:数值,整数,浮点数都可以
let age:number = 21
//boolean:布尔
let finished:boolean = true
//any:不确定类型,可以使任意类型
let a:any = 'jack'
a = 21
//union:联合类型,可以是多个指定类型中的一种
let u:string|number|boolean = 'rose'
u = 18
//Object:对象
let p = {name:'Jack',age:21}
console.log(p.name)
console.log(p.age)
//Array:数组,元素可以是任意其他类型
let names:Array<string> = ['Jack','Rose']
let ages:number[] = =[21,18]
console.log(names[0])
```

**注意:**

数据类型的首字母是小写,大写会报错

(2)TypeScript与大多数开发语言类似,支持基于if-else和switch的**条件控制.**

```typescript
// 定义数字
let num:number = 21

//判断是否是偶数
if(num % 2 === 0){
    console.log(num + '是偶数')
}else{
    console.lo(num + '是奇数')
}

//判断是否是正数
if(num > 0){
    console.lo(num + '是正数')
}else if(num < 0){
    console.lo(num + '是负数')
}else{
    console.lo(num + '为0')
}
```

**注意:**

在TypeScript中,空字符串,数字0,null,undefined都被认为是false,其他值都为true

```typescript
let grade:string = 'A'
switch(grade){
    case 'A':{
        console.log('优秀')
        break
    }
    case 'B':{
        console.log('合格')
        break
    }
    case 'C':{
        console.log('不合格')
        break
    }
    default:{
        console.log('非法输入')
        break
    }
}
```

(3)TypeScript支持for和while**循环**,并且为一些内置类型如Array等提供了快捷迭代语法

```typescript
//普通for
for(let i = 1 ; i <= 10 ; i++){
    console.log('点赞'+i+'次')
}
//while
let i = 1
while(i <= 10){
    console.log('点赞'+i+'次')
    i++
}
```

```typescript
//定义数组
let names:string[] = ['Jack','Rose']

//for in 迭代器,遍历得到数组角标
for(const i in names){
    console.log(i+':'+names[i])
}

//for of 迭代器,直接得到元素
for(const name of names){
    console.log(name)
}
```

(4)TypeScript通常利用function关键词声明**函数**,并且支持可选参数,默认参数,箭头函数等特殊语法

```typescript
//无返回值函数,返回值void可以省略
function sayHello(name:string):void{
    console.log('你好'+name+'!')
}
sayHello()

//有返回值函数
function sum(x:number,y:number):number{
    return x + y
}
let result = sum(21,18)
console.log('21 + 18 ='+result)

//箭头函数
let sayHi = (name:string)=>{
    console.log('你好'+name+'!')
}
sayHi('Rose')
```

```typescript
//可选参数,在参数名后加 ?,表示该参数是可选的,在参数后可加默认值
function sayHello(name?:string='陌生人'){
	console.log('你好'+name+'!')
}
```

(5)应用复杂时,我们可以把通用功能抽取到单独的ts文件中,每个文件都是一个**模块(module)**.模块可以互相加载,提高代码复用性.

```typescript
//定义矩形类,并通过export导出
export class Rectangle {
    //成员变量
    public width:number
    public length:number
    //构造函数
    constructor(width:number,length:number){
        this.width=width
        this.length=length
    }
}

//定义工具方法,求矩形面积,并通过export导出
export function area(rec:Rectangle):number{
    return rec.width*rec.length
}
```

```typescript
//通过import语法导入,from后面写文件地址
import {Rectangle,area} from '../Rectangle'

//创建Rectangle对象
let r = new Rectangle(10,20)

//调用area方法
console.log('面积为:'+area(r))
```

## ArkTS入门

```ArkTS
@Entry
@Component
struct Index {
	@State message :string = 'Hello world'
	build(){
		Row(){
			Column(){
				Text(this.message)
					.fontSize(50)
					.fontWeight(FontWeight.Bold)
					.onclick(()=>{
					//处理事件
					})
			}
            .width('100%')
		}
		.height('100%')
	}
}
```

```txt
装饰器:用来装饰类结构,方法,变量
@Entry:标记当前组件是入口组件
@Component:标记自定义组件
@State:标记该变量是状态变量,值变化时会触发UI刷新

自定义组件:可复用的UI组件

build(){}:UI描述,其内部以声明方式描述UI结构

内置组件:ArkUI提供的组件

容器组件:用来完成页面的布局,例如Row,Column

基础组件:自带样式和功能的页面元素,如Text

.onclick(()=>{}):事件方法,设置组件的事件回调

.width,.height:属性方法,设置组件的UI样式
```

## Image

**1.声明Image组件并设置图片源:**

​	Image(src:string|PixelMap|Resource)

(1)string格式,通常用来加载网络图片,需要申请网络访问权限:ohos.permission.INTERNET

```ArkTS
Image('https://xxx.png')
```

(2)PixelMap格式,可以加载像素图,通常在图片编辑中

```ArkTS
Image(pixelMapObject)
```

(3)Resource格式,加载本地图片,推荐使用

```ArkTS
//图片保存在media文件夹中
Image($r('app.media.mate60'))
//图片保存在rawfile文件夹中
Image($rawfile('mate60.png'))
```

**2.添加图片属性**

```ArkTS
Image($r('app.media.icon'))
	.width(100)//宽度
	.height(120)//高度
	.borderRadius//边框圆角
	.interpolation(ImageInterpolation.High)//图片差值
```

## Text

**1.声明Text组件并设置文本内容**

​	Text(content?:string|Resource)

(1)string格式,直接填写文本内容

```ArkTS
Text('图片宽度')
```

(2)Resource格式,读取本地资源文件

```ArkTS
Text('app.string.width_label')
//文件保存在base的string.json,各种语言下的string.json
```

```json
//配置文件
{
    "string":[
        {
            "name":"width_label",
            "value":"Image Width"
        }
    ]
}
```

**2.添加文本属性**

```ArkTS
Text('注册账号')
	.lineHeight(32)//行高
	.fontSize(20)//字体大小
	.fontColor('#ff1876f8')//字体颜色
	.fontWeight(FontWeight.Medium)//字体粗细,范围是100-900,默认400
```

## TextInput

**1.声明TextInput组件:**

​	TextInput({placeholder?:ResourceStr,text?:ResourceStr})

(1)placeholder:输入框无文本时的提示文本

```ArkTS
TextInput({placeholder:'请输入账号或手机号'})
```

(2)text:输入框当前的文本内容

```
TextInput({text:'itcast'})
```

**2.添加属性和事件**

```ArkTS
TextInput({text:'当前输入文本'})
	.width(150)//宽
	.height(30)//高
	.backgroundColor('#FFF')//背景色
	.type(InputType.Password)//输入框类型
	.onchange(value=>{
	//value是用户输入的文本内容
	})				
```

补充:

输入框类型

| 名称        | 描述                                                |
| ----------- | --------------------------------------------------- |
| Normal      | 基本输入模式,支持输入数字,字母,下划线,空格,特殊字符 |
| Password    | 密码输入模式,支持输入数字,字母,下划线,空格,特殊字符 |
| Email       | 邮箱地址输入模式,支持数字,字母,下划线,以及@字符     |
| Number      | 纯数字输入模式                                      |
| PhoneNumber | 电话号码输入模式,支持数字,+,-,*,#,长度不限          |

## Button

**1.声明Button组件,label是按钮文件**

​	Button(label?:ResourceStr)

(1)文字型按钮

```ArkTS
Button('点我')
```

(2)自定义按钮,在Button内嵌套其他组件

```ArkTS
Button(){
	Image($r('app.media.search')).width.margin(10)
}
```

**2.添加属性和事件**

```ArkTS
Button('点我')
	.width(100)
	.height(30)
	.type(ButtonType.Normal)//按钮类型
	.onClick(()=>{
	//处理点击事件
	})
```

补充:

按钮类型

| 名称    | 描述                             |
| ------- | -------------------------------- |
| Capsule | 胶囊型按钮(圆角默认为高度的一半) |
| Circle  | 圆形按钮                         |
| Normal  | 普通按钮(默认不带圆角)           |

## Slider

​	Slider(options?:SliderOptions)

```ArkTS
//滑动条
Slider({
	min:0,//最小值
	max:100,//最大值
	value:40,//当前值
	step:10,//滑动步长
	style:SliderStyle.OutSet,//Inset
	direction:Axis.Horizontal,//Vertical
	reverse:false
})
	.width('90%')
	.showTips(true)//是否展示Value百分比提示
	.blockColor('#36d')
	.onChange(value=>{
	//value就是当前滑块值
	})
```

## Column和Row

1.Column为纵向布局容器,主轴垂直,交叉轴水平;Row为横向布局容器,主轴水平,交叉轴垂直

2.属性方法

| 属性方法名     | 说明                             | 参数                                                        |
| -------------- | -------------------------------- | ----------------------------------------------------------- |
| justifyContent | 设置子元素在主轴方向的对其格式   | FlexAlign枚举                                               |
| alignItems     | 设置子元素在交叉轴方向的对齐格式 | Row容器使用VerticalAlign枚举;Column容器使用HorizonAlign枚举 |

补充:

枚举

| Start | Center | End  | SpaceBetween | SpaceAround | SpaceEvent |
| ----- | ------ | ---- | ------------ | ----------- | ---------- |

## 循环控制

```ArkTS
//商品数据
private items = [
	{name:'华为Mate60',image:'1.jpg',price:6999},
	{name:'华为Mate60',image:'1.jpg',price:6999},
	{name:'华为Mate60',image:'1.jpg',price:6999},
	{name:'华为Mate60',image:'1.jpg',price:6999},
	{name:'华为Mate60',image:'1.jpg',price:6999},
	{name:'华为Mate60',image:'1.jpg',price:6999}
]

ForEach(
	arr:Array,//要遍历的数组
	//页面组件生成函数
	(item:any,index?:number)=>{
		Row(){
			Image(item.Image)
			Column(){
				Text(item.name)
				Text(item.price)
			}
		}
	},
	keyGenerator?:(item:any,index?:number):string=>{
		//键生成函数,为数组每一项生成一个唯一标识,组件是否重新渲染的判断标准,类似与Vue中的':key'
	}
)
```

## List

列表(List)是一种复杂容器,具备下列特点:

1. 列表项(ListItem)数量过多超出屏幕后,会自动提供滚动功能
2. 列表项(ListItem)既可以纵向排列,也可以横向排列

```ArkTS
List({space}){
	ForEach([1,2,3,4],item => {
		ListItem(){
			//列表内容,只能包含一个根组件
			Text('ListItem')
		}
	})
}
	.width('100%')
	.listDirection(Axis.Vertical)//列表方向,默认纵向(垂直)
	.layoutWeight(1)//使列表占据剩余部分
```

## 自定义组件

### 自定义组件

```ArkTS
@Component
struct Header {
	private title: ResourceStr
	build(){
		//标题部分
		Row(){
		// code ...
		}
	}
}
```

```ArkTS
@Entry
@Component
struct ItemPage {
	build(){
	Column(){
		//标题部分
		Header({title:'商品列表'})
	}
	}
}
```

**解释:**

1. **@Component**修饰器用于修饰一个**组件**
2. **@Entry**修饰器用于修饰一个单独的**页面**
3. 自定义组件中可以传值,详见组件通信

### 自定义构建函数

**1.全局定义**

```ArkTS
//全局自定义构建函数
@Builder function XxxBuilder(){
	//UI描述
}
```

**2.局部定义**

```ArkTS
@Component
struct XxxComponent{
	//组件内自定义构建函数
	@Builder YyyBuilder(){
	//UI描述
	}
	build(){
		XxxBuilder()
		this.YyyBuilder()
	}
}
```

**补充:**

1. 全局定义需要加function,局部定义不需要
2. 全局定义调用不加this,直接调用,局部定义需要加

### 自定义样式函数

#### @Styles

**1.全局定义**

```ArkTS
//全局公共样式
@Styles function fillScreen(){
	.width('100%')
	.height('100%')
}
```

**2.局部定义**

```ArkTS
@Entry
@Component
struct XxxPage {
	//组件内公共样式
	@Styles normalBackground(){
		.backgroundColor('#EFEFEF')
		.padding(14)
	}
	build(){
		Row(){}
		.fillScreen()
		.normalBackground()
	}
}
```

**补充:**

1. 全局定义需要加function,局部定义不需要
2. 不论全局定义还是局部定义,调用都是直接调用
3. @Styles修饰器定义的样式函数只能包含通用属性

#### @Extend

@Extend修饰器,仅可定义在全局,可以设置组件特有属性

```ArkTS
@Extend(Text) function priceText(){
	.fontColor('#F36')
	.fontSize(18)
}
```

## 状态管理

### @Prop和@Link

|                    | @Prop                                                        | @Link                                                        |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 同步类型           | 单向同步                                                     | 双向同步                                                     |
| 允许装饰的变量类型 | @Prop只支持:string,number,boolean,enum类型;                       父组件对象类型,子组件是对象属性;                                                 不可以是数组,any | 父子类型一致:string,number,boolean.enum.object,class.以及他们的数组;                   数组中元素的增,删,替换会引起刷新;                                                                                   嵌套类型以及数组中的对象属性无法触发视图更新 |
| 初始化方式         | 不允许子组件初始化                                           | 父组件传递,禁止子组件初始化                                  |

### @Provide和@Consume

@Provide和@Comsume可以跨组件提供类似于@State和@Link的双向同步

### @ObjectLink和@Observed

@ObjectLink和@Observed装饰器用于在涉及**嵌套对象**或**数组元素为对象**的场景中进行数据双向同步

```ArkTS
@Observed
class Person {
	name:string
	age:number
	gf:Person
	constructor(name:string,age:number,gf?:Person){
		this.name=name
		this.age=age
		this.gf=gf
	}
}
```

```ArkTS
@Component
struct Child {
	@ObjectLink p:Person
	build(){
		Column(){
			Text(`${this.p.name}:${this.p.age}`)
		}
	}
}
```

```ArkTS
@Entry
@Component
struct Person {
	@State p : Person = new Person('Jack',21,new Person('Rose',19))
	@State gfs :Person[]={
		new Person('罗斯',18),
		new Person('露西',19),
	}
	build(){
		Column(){
			Child({p:this.p.gf})
				.onClick(()=>this.p.gf.age++)
				Text('=====女友列表=====')
				forEach(
				this.gfs,
				p=>{
				Text(`${p.name}:${p.age}`.onClick(()=>p.age++))
				}
				)
		}
	}
}
```

**补充:**

1. 把包含需要监视的嵌套对象(或数组对象)提取出在一个单独的组件里,父组件仍用@State,子组件用@ObjectLink
2. 在父组件中把数据传入子组件

## 页面路由

页面路由是指在应用程序中实现不同页面之间的跳转和数据的传递

1.页面栈的最大容量上限为32个页面,使用router.clear()方法可以清空页面栈,释放内存

2.Router有两种页面跳转模式,分别是:

​	(1).router.pushUrl():目标页不会替换当前页,而是压入页面栈,因此可以用router.back()返回当前页

​	(2).router.replaceUrl():目标页替换当前页,当前页会被销毁并释放资源,并且无法返回当前页

3.Router有两种页面实例模式,分别是:

​	(1).Standard:标准实例模式.每次跳转都会新建一个目标页并压入栈顶.默认就是这种模式

​	(2).Single:单实例模式,如果目标页已经在栈中,则离栈顶最近的同Url页面会被移动到栈顶并且重新加载

```ArkTS
// 1.首先要导入HarmonyOS提供的Router模块:
	import router from '@ohos.router'
```

```ArkTS
//2.然后利用router实现跳转,返回等操作
	router.pushUrl({
		url:'pages/ImagePage',
		params:{id:1}
	},
	router.RouterMode.Single,
	err => {
		if(err){
			console.log('路由失败')	
		}
	}
)
//RouterOptions
// - url :目标页面的路径
// - params : 传递的参数,可选

//页面模式:RouterMode枚举

//异常想用回调函数,错误码
// - 100001:内部错误,可能是渲染失败
// - 100002:路由地址错误
// - 100003:路由栈中页面超过32
```

```ArkTS
//获取传递过来的参数
params: any = router.getParams()

//返回上一页
router.back()

//返回指定页,并携带参数
router.back({
		url:'pages/Index',
		params:{id:10}
	}
)
```

