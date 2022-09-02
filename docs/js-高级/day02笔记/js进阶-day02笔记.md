# 学习目标

> - [x] 能够说出不同情况下函数内 this 的指向
>
>   - 默认绑定：window
>     - fn()
>     - 定时器
>     - 延时器
>   - 隐式绑定：调用者
>     - 方法调用：obj.fn()
>     - 事件处理函数
>   - new绑定：实例对象
>     - new Person()
>   - 硬绑定：想让this指向谁，就指向谁
>     - call：调用函数并且改变this
>     - apply：调用函数并且改变this
>     - bind：返回一个新函数，并且规定死了该新函数的this指向
>
> - [x] 能够借用原型对象继承父类方法
>
>   ```js
>   Student.prototype = new Person()
>   ---------------------------------------------
>   Student.prototype = Object.create(Person.prototype)
>   ```
>
>   
>
> - [x] 能够借用构造函数继承父类属性
>
>   ```js
>   Person.call(this,name,age)
>   ```
>
>   
>
> - [ ] 
>
> - [ ] 能够说出类的本质
>
> - [ ] 能够说出类和对象的区别
>
> - [ ] 能够创建一个类并且实例化对象
>
> - [ ] 能够说出类里面constructor函数的作用
>
> - [ ] 能够说出什么是静态成员和实例成员
>
> - [ ] 能够说出类里面this的指向
>
> 。。。。。。



**理解上课的知识点......**



# this

## this的基本介绍

**this：** this是一个关键字，一般在函数中使用，但是this具体指向谁，一般由函数的调用方式决定

**之前遇到的this：**

- 注册事件：this指向事件源
- 构造函数：this指向创建的新对象

**问题：**

> 实际开发中会遇到不同情况下的this

```js
let obj = {
    name: 'zs',
    age: 18,
    sayHi: function () {
        console.log(this)
    }
}
obj.sayHi() // 

let temp = obj.sayHi
temp() // 
```



## this的不同情况

**绝大部分情况：**函数的this是无法通过定义函数的上下文就可以知道的，**需要通过调用才能够知道** 

![image-20210220133907898](./assets/image-20210220210918112.png)

> 来源: 你不知道的 javascript

**1、默认绑定：**this指向window

```js
// this的几种情况——》默认绑定——》指向window
// 1、fn()
// 2、定时器
// 3、延时器

// 1、fn()
function fn() {
    console.log(this)
}
fn()
window.fn()

// 2、定时器
setInterval(function () {
    console.log(this)
}, 1000)

// 3、延时器
setTimeout(function () {
    console.log(this)
}, 1000)
```

**2、隐式绑定：** this指向调用者

```js
// this的几种情况——》隐式绑定：指向调用者——》基本写法： 调用者.函数名()
// 1、对象方法调用
// 2、事件处理函数

// 1、对象方法调用
let obj = {
    name: 'zs',
    age: 18,
    fn: function () {
        console.log(this)
    },
    car: {
        desc: '玛莎拉蒂',
        run: function () {
            console.log(this)
        }
    }
}

obj.fn() // obj
obj.car.run() // obj.car 

// 2、事件处理函数
let btn = document.querySelector('button')
btn.addEventListener('click', function () {
    console.log(this)
})

// 其实就是让浏览器自动调用btn的点击事件
// btn.click()

// 判断this的口诀：谁调用this，this就是谁（new除外）
```

**判断this的口诀：**谁调用this，this就是谁（new除外）

**3、new绑定：**this指向当前创建实例

```js
// this的几种情况——》new绑定：指向创建的实例对象——》基本写法：new 构造函数
function Person() {
    console.log(this)
}
let p = new Person()
```

**4、硬绑定：** 想让this指向谁就是谁（待会介绍）

**小结：**

1. 默认绑定：指向window——》fn()、定时器、延时器
2. 隐式绑定：指向调用者——》obj.fn()、事件处理函数
3. new绑定：指向当前创建的实例——》new Person()



##### ヾ(๑╹◡╹)ﾉ" this相关面试题

```js
// 第一题：-----------------------------------------
function fn () {
    console.log(this)
}
fn() // 

// 第二题：---------------------------------------------------
let obj = {
    fn: function() {
        console.log(this)
    }
}
obj.fn() // 

let temp = obj.fn
temp() // 

// 第三题：---------------------------------------------------
function Cat () {
    console.log(this)
}
let c1 = Cat() // 
let c2 = new Cat() // 
console.log(c1, c2) // 

// 第四题：--------------------------------------------------------------
let obj = {
    a: {
        fn: function () {
            console.log(this)
        },
        b: 10,
    },
}
obj.a.fn() // 

let temp = obj.a.fn
temp() // 

// 第五题：-------------------------------------------------------------

function Person(theName, theAge) {
    this.name = theName
    this.age = theAge
}

Person.prototype.sayHello = function () {
    console.log(this)
    console.log('我叫' + this.name + '我今年, ' + this.age + '岁');
}

let per = new Person('小黑', 18)
per.sayHello() // 
```



# 练习题

##### ヾ(๑╹◡╹)ﾉ" 构造函数相关方法

```js
// 求A-B范围随机整数公式(可选):
// parseInt(Math.random() * (B - A + 1)) + A

// 练习: 定义ChuanTool构造函数, 属性接受2个数字(numA, numB), 定义2个方法(getMax, randomNum), 
// getMax方法返回numA和numB其中比较大的值, 另一个方法返回一个随机数(范围就是numA到numB, 假设numA是小于numB的) 
// 要求: 所有由ChuanTool构造函数new出来的对象都可以共享到getMax和randomNum方法.

// 定义2个实例对象, 分别调用返回打印结果
function ChuanTool(theNumA, theNumB) {

}

let obj1 = new ChuanTool(10, 20)  // { numA: 10, numB: 20 }
let obj2 = new ChuanTool(40, 80)  // { numA: 40, numB: 80 }

obj1.getMax() // 20
obj2.getMax() // 80
obj1.randomNum() // 10 - 20的随机数 
obj2.randomNum() // 40 - 80的随机数
```



# 昨日作业

```js
// 需求1: 尝试给现在系统的Array构造函数添加一个取最大值得函数, 确保下面代码正确
// 提示: 对象调用函数, 本身没有会去哪里找? 所以在调用之前可以在Array函数, 的什么位置上扩展添加方法呢?

/*这里应该补充什么代码呢?*/

let arr1 = [100,200,5];
console.log(arr1.getMax()); // 200

let arr2 = [5, 2, 1, 10, 3, 4];
console.log(arr2.getMax()); // 10

// 答案：----------------------------------------------------------------------
// 在原型对象上添加方法，可以供所有实例对象使用
Array.prototype.getMax = function () {
    // 获取当前实例数组——》因为调用是隐式绑定，所以通过this就可以获取当前实例数组
    // console.log(this)
    let max = this[0]
    for (let i = 0; i < this.length ; i++) {
        if (this[i] > max) {
            max = this[i]
        }
    }
    // console.log(max)
    return max
}

let arr1 = [100, 200, 5];
console.log(arr1.getMax()); // 200

let arr2 = [5, 2, 1, 10, 3, 4];
console.log(arr2.getMax()); // 10
```



```js
// 需求2: 给系统Date构造函数, 添加一个toMyString函数 - 调用函数, 得到今天日期YYYY年MM月DD日 HH:mm:ss 格式的时间
let date = new Date()
console.log(date.toMyString()) // YYYY年MM月DD日 HH:mm:ss格式

// 答案：----------------------------------------------------------------------------
// 为了每一个实例对象都可以使用到toMyString方法，需要把toMyString添加到原型对象上
Date.prototype.toMyString = function () {
    // 获取当前的日期对象
    // console.log(this)
    // 需要拼接成 YYYY年MM月DD日 HH:mm:ss 格式的时间——》获取日期的指定部分
    let year = this.getFullYear()
    let month = this.getMonth() + 1
    let day = this.getDate()
    let hours = this.getHours()
    let minutse = this.getMinutes()
    let seconds = this.getSeconds()
    let str = `${addZero(year)}年${addZero(month)}月${addZero(day)}日 ${addZero(hours)}:${addZero(minutse)}:${addZero(seconds)}`
    return str
}

// 补0函数
function addZero(num) {
    let result = num < 10 ? '0' + num : num
    return result
}

let date = new Date()
console.log(date.toMyString()) // YYYY年MM月DD日 HH:mm:ss格式
```



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" tab栏组件封装案例

##### 1、tab栏组件封装-静态结构

```html
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <style>
        .box {
            border: 1px solid #000;
            box-sizing: border-box;
        }

        .box * {
            box-sizing: border-box;
        }

        .box .header {
            width: 100%;
            height: 50px;
            display: flex;
            border-bottom: 1px solid #222;
        }

        .box .header span {
            transition: all 0.3s;
            background-color: #fff;
            line-height: 50px;
            text-align: center;
            cursor: pointer;
            font-size: 16px;
            border-right: 1px solid #000;
            flex: 1;
        }

        .box .header span.active,
        .box .header span:hover {
            background-color: #ccc;
        }

        .box .main {
            width: 100%;
        }

        .box .main div {
            width: 100%;
            text-align: center;
            font-size: 60px;
            font-weight: 800;
            display: none;
        }

        .box .main div.active {
            display: block;
        }
    </style>

    <body>
        <div class="box">
            <div class="header">
                <span class="active">tab1</span>
                <span>tab2</span>
                <span>tab3</span>
            </div>
            <div class="main">
                <div class="active">内容1</div>
                <div>内容2</div>
                <div>内容3</div>
            </div>
        </div>

        <script>

        </script>
    </body>

</html>
```

##### 2、tab栏组件封装-基于数据动态渲染

```js
// 实际开发中：
// 1、tab栏的个数是根据数据动态渲染的
// 2、tab栏的内容+切换盒子的内容也是根据数据动态渲染的

// tab栏数组
let headerArr = ['tab1', 'tab2', 'tab3']
// 内容数组
let contentArr = ['内容1', '内容1', '内容1']

// --------------------------------------初始化结构----------------------------
// 需求：基于数据，动态渲染上面的结构
// 1、找到box对象
// 2、创建header+content大盒子，并且添加类名，并且添加到页面中去
// 3、遍历对应数组，创建header中的子元素，并且添加内容，并且添加到header中去
// 4、遍历对应数组，创建content中的子元素，并且添加内容，并且添加到content中去
```

##### 3、tab栏组件封装-绑定事件

```js
// ---------------------------------注册事件-------------------------------------
// 需求：获取所有的span标签，给span注册事件，点击之后，让tab高亮并且切换content
// 1、找到所有的header中的span标签和content中的div标签
// 2、给所有的header中的span标签，注册点击事件
// 3、点击span之后，需要给当前的span和对应的div添加active类
```

##### 4、tab栏组件封装-构造函数封装铺垫

> 实际开发中，如果需要复用tab栏组件，可以封装

```js
// 需求：需要在页面中#box1和#box2中通过封装函数创建tab栏
// 构造函数是为了创建实例
// 需要的属性如下：
//  1、需要追加tab结构的元素——》el元素
//  2、需要渲染的header部分的内容——》headerArr内容
//  3、需要渲染的content部分的内容——》contentArr内容
// 需要实现的功能方法：
//  1、init：动态生成结构
//  2、addClick：给header的所有span注册点击事件
```

##### 5、tab栏组件封装-构造函数封装完成

**init方法的修改：**

1. 获取的 `box` 设置为 `this.el`
2. 设置的数据 `headerArr` 和 `contentArr` 设置为 `this.headerArr` 和 `this.contentArr` 

**addClick方法的修改：**

1. 查找所有的span和div时，需要限定范围，把 `document` 改成 `this.el`

​	

# this 相关 - 补充(硬绑定)

| 方式     | 代码                         | this指向   | 备注                                        |
| -------- | ---------------------------- | ---------- | ------------------------------------------- |
| 默认绑定 | fn() / 定时器/ 计时器        | window     | 指向window                                  |
| 隐式绑定 | 事件处理函数 / 函数方法调用  | 调用者     | 调用者.函数名(), 指向调用者                 |
| new绑定  | new 构造函数()               | 新对象     | 指向这个新的实例对象                        |
| 硬绑定   | 使用call / apply / bind 方法 | 传入的参数 | call和apply马上执行函数, bind会返回一个函数 |

## call方法

**功能：** 调用函数的同时，修改this的执行

**语法：** `函数名.call(this指向,参数1,参数2,参数3,.....)`

**作用：**

1. 调用函数
2. 修改this的指向

**应用场景：** 借用构造函数

```js
// 调用函数：----------------------------------------------------
function fn() {
    console.log(this)
}
fn() // window
fn.call() // 如果call没有指定this的指向，默认就是window

let obj = {
    name: 'zs',
    age: 18
}
fn.call(obj) // 如果call指定了this的指向，此时this就是指定的部分


// 应用场景：借用构造函数--------------------------------------------
function Person(name, age) {
    this.name = name
    this.age = age
}

let one = {
    desc: '我想要名字和年龄'
}
Person.call(one, '小明', 15)
console.log(one)
```

## apply方法

**功能：** 调用函数的同时，修改this指向

**语法：** `函数名.call(this指向,[参数1,参数2,参数3,......])`

**作用：**

1. 调用函数
2. 修改this的指向

**应用场景：** 快速求数组的最大值

```js
// 调用函数：---------------------------------------------------
function fn() {
    console.log(this)
}
fn()
fn.apply()

// 借用构造函数：------------------------------------------------
function Person(name, age) {
    this.name = name
    this.age = age
}

let obj = {
    desc: '我要名字和年龄'
}

// Person.call(obj,'张三',18)
Person.apply(obj, ['李四', 21]) // 将来工作中会有传参为参数列表的情况，参数数据本身就在数组中
console.log(obj)

// 实际场景：快速求出数组的最大值---------------------------------------
let arr = [1, 2, 3, 4, 5, 6, 7, 8]
let max = Math.max.apply(null, arr) // 利用apple传入的参数列表，调用max函数
console.log(max)
```

## bind方法

**功能：** 不会立即指向函数，而是得到一个新的函数，新函数中绑定死了this的执行

**语法：** `let newFn = fn.bind(this指向)`

**注意点：** 新函数和原函数函数体完全一致，只是this不同

```js
function fn() {
    console.log(this)
}

let obj = {
    name: 'zs',
}

let newFn = fn.bind(obj) // 创建一个新函数，新函数中绑定死了this为obj

newFn() // obj
fn() // window

let temp = newFn
temp() // obj

let obj2 = {
    fn: newFn
}
obj2.fn() // obj
```



# 继承

## 为什么要学习继承

**为什么要学习继承：**

- 开发中通过构造函数，可以定义类型，如：人类 
- 但是实际人类的具体类型有很多，如：老师、工人，这些细化的类型上有人类相同的属性和方法，如果由需要重复书写，代码跟冗余
- 学习继承，可以让多个构造函数之间建立关联，让代码更加便于管理和复用

**继承：**从别人那里，继承东西过来（如：房产、财产）

**代码层面的继承：** 继承一些属性和方法



## 原型继承-继承方法

**需要Student类型继承Person的方法：** `sayHi`

**原型继承：** 利用原型链，进行继承方法

```js
// 声明人类构造函数---------------------------------------------
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.sayHi = function () {
    console.log('hello')
}

// 声明学生构造函数---------------------------------------------
function Student(name, age, code) {
    this.name = name
    this.age = age
    this.code = code
}
// Student.prototype.sayHi = function () {
//   console.log('hello')
// }

// 让Person的原型和Student建立链接------------------------------
// 原型替换
// Student.prototype = Person.prototype // 这样会让后续给Student添加的方法都添加到Person的原型对象上
Student.prototype = new Person()

Student.prototype.read = function () {
    console.log('背书')
}

let stu2 = new Student('小明', 18, 101)
stu2.sayHi()
stu2.read()
```

##### (๑╹◡╹)ﾉ""" 画图演示原型继承

> 类似于换个老公，让自己的孩子可以继承家族的资源

![1656170999278](assets/1656170999278.png)

## 组合继承-继承属性和方法

**原型继承：** 只能继承方法

**组合继承：** 可以继承属性和方法

- 利用原型链，继承原型上的方法
- 利用借用构成函数 `call` ，实现实例的属性继承

```js
// 声明人类构造函数---------------------------------------------
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.sayHi = function () {
    console.log('hello')
}

// 声明学生构造函数---------------------------------------------
function Student(name, age, code) {
    // 借用父类构造函数，实例化属性
    // Person() // this指向window
    // 需要调用Person()函数的同时，把this指向当前实例——》当前构造函数中的this
    Person.call(this, name, age)

    // 实例化自己的属性
    this.code = code
}

// 让Person的原型和Student建立链接------------------------------
// 原型替换
Student.prototype = new Person()

let stu2 = new Student('小明', 18, 101)
stu2.sayHi()
```



## 寄生组合继承-继承实例上没有多余的属性和方法

**组合继承：** 用原型替换了需要继承的实例的方法，但是继承的实例中的属性和方法是不需要的，此时可以通过寄生组合式继承优化

**寄生组合式继承：** 利用 `Object.create()` 方法，对组合式继承进行了优化

**Object.create()：** 创建一个新对象，可以传参，会让新对象的 `__proto__` 指向传入的对象（传谁就认谁做干爹）

> 类似于找到的老公自己身上的个性太多了，让公公再生个干干净净的小儿子，嫁给小儿子

```js
function Person(name, age) {
    this.name = name
    this.age = age
}

Person.prototype.run = function () {
    console.log('会跑')
}

// 创建一个老师对象，继承Person的属性和方法
function Teacher(name, age, lesson) {
    // 借用父类构造函数，实现实例化
    Person.call(this, name, age)
    // 实例化自己的属性
    this.lesson = lesson
}

// 原型替换：替换原型为实例，虽然效果可以，但是实例上有无意义的属性
// Teacher.prototype = new Person()
// 使用Object.create()创建的新对象，可以传参，让新对象的__proto__指向传入的对象）——》传入谁就认谁做干爹
Teacher.prototype = Object.create(Person.prototype)

let teacher = new Teacher('小张', 18, '数学')
console.log(teacher)
teacher.run()
```

##### (๑╹◡╹)ﾉ""" 画图演示寄生组合式继承

![1656175917786](assets/1656175917786.png)

##### ヾ(๑╹◡╹)ﾉ" 继承组合式继承练习

```js
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.sayHi = function () {
    console.log('会打招呼')
}
// 工人: name age id / sayHi work
// 要求: name age / sayHi 从Person继承
```



## constructor属性（了解）

**constructor：** 原型对象中有一个属性 `constructor` 指向构造函数

```js
// 绘制原型 构造函数 实例的三角关系
// 原型对象上, 默认有一个属性 constructor 会指向对应的构造函数

function Person() {

}
let p = new Person()

console.log(Person.prototype.constructor === Person) // 
console.log(p.__proto__.constructor === Person) // 
console.log(p.__proto__.constructor === Person.prototype) // 
```

![1655831351806](assets/1655831351806.png)









































































# ES6

ES6 :  ECMAScript6, 第6代标准(ECMAScript 2015年发布的标准, 也叫ES2015)  跨时代的年份

> ES5:   ECMAScript5, 第5代标准(2009年发布的标准)
>
> 从ES6开始，每年都会更新一次，并且在新标准下，旧标准中的语法也都会保留，



## 基础认知

### 面向过程开发

分析解决问题所需要的步骤，然后用函数和基础代码，把步骤一步一步的实现

使用的时候代码一行一行执行即可

使用的时候再一个一个的依次调用就可以了

### 面向对象开发

面向对象把事物抽离出一个一个的对象，然后对象内部实现不同的功能

使用的时候通过对象调用内部的属性和方法完成功能

### 面向对象和过程区别

**面向过程开发：重在步骤，亲力亲为（普通员工思想）**

**比如：要拖地，普通员工要自己一步一步拖**

1.  拿到拖把
2. 洗拖把
3. 拖地
4. 再洗拖把
5. 放回拖把

**面向对象开发：重在对象的分工，对象内部完成对应功能，便于维护（老板思想）**

**比如：要拖地，老板要找个清洁员（对象），由这个对象完成即可**

1. 找个清洁员
2. 清洁员去拖地，清洁员.拖地()

**注意点：面向对象，其实就是对于面向过程的封装抽象**



### 类的概念

**请将以下事物分类：一共分成几类？**

- 一只叫大黄的狗
- 老王的豪华海景房
- 老张的哈士奇
- 小黑的劳斯莱斯
- 小芳的保时捷
- 小红的柴犬

**类的概念：** 一组 相同特征 和 行为 的事物抽象（类似于构造函数）

> 特征：属性（比如：年龄、姓名、性别）
>
> 行为：方法（比如：会跑、会跳）

**类的作用：** 定义一套模板，批量生产对象

> 类似于构造函数的思路，就是写法语法不同

**区别类和对象：**

- 柴犬
- 我家养的小阿柴
- 三文鱼
- 我餐桌上的三文鱼
- 笔记本电脑
- 我现在面前使用的笔记本电脑



## ES6-类class 

**类是一个关键字：class**

**语法：**

```js
class 类名 {
    
}
```

**注意点：**

1. 类名首字母大写
2. 类的定义，类名后面没有小括号
3. 创建实例，一样通过new

```js
// 定义类 (类似于之前的构造函数)
// class 类名 {}
class Person {

}
// 创建一个实例对象
let p = new Person()
console.log(p)
```



## ES6-给类class中设置构造函数和往原型上添加方法

**给类中设置构造函数：** `constructor` 

**给类中的原型上添加方法：** 直接在类名上添加属性或者方法

```js
class Person {
    // 在内部直接写构造函数
    constructor(name, age) {
        this.name = name
        this.age = age
    }

    // 给原型上加属性和方法
    sayHi() {
        console.log('打招呼')
    }

    jump() {
        console.log('会跳')
    }

    read() {
        console.log('读书')
    }
}

let p1 = new Person('zs', 19)
console.log(p1)
p1.sayHi()
p1.jump()
```

**注意点：** 类class语法，本质上就是语法糖，底层实现还是基于构造函数和原型



## ES6类-实例对象和静态成员-static

**实例成员：** 由构造函数创建出来的成员，能够访问的属性和方法

- 包含：对象本身，已经原型链中的所有属性和方法
- 实例成员访问语法：`实例对象.xxx` 、 `实例对象.xxx()` 

**静态成员：** 通过构造函数，直接访问的属性的方法

- 静态成员访问语法：`构造函数.xxx` 、 `构造函数.xxx()`

```js
// static关键字：被static修饰的成员, 就是静态成员, 会直接被添加到 类 的身上
// 静态成员：看到语法认识即可，使用场景不多，但是后期react类型校验中会遇到
class Person {
    static version = 'v1.1'
    static play() {
        console.log('会打麻将')
    }

    constructor(name, age) {
        this.name = name
        this.age = age
    }

    sayHi() {
        console.log('你好鸭')
    }
}

let p = new Person('zs',18)
// 实例成员
p.sayHi()
console.log(p.name)
console.log(p.age)
// 静态成员
console.log(Person.version)
Person.play()
```



## ES6类-this的指向问题

```js
class Person {
    static version = 'v1.1'
    static play() {
        console.log(this)
    }

    constructor(name, age) {
        console.log(this)
        this.name = name
        this.age = age
    }

    sayHi() {
        console.log(this)
    }
}

let p1 = new Person('zs', 18) // 实例p1

// 实例成员
p1.sayHi() // 实例p1

// 静态成员
Person.play() // Person

// 面试题-------------------------------------
// class Person {
//   static aa = 123
//   static getRandomNum() {
//     console.log(this)
//     return parseInt(Math.random() * 11)
//   }

//   constructor(name) {
//     console.log(this)
//     this.name = name
//   }
//   sayHello() {
//     console.log(this)
//   }
// }

// let p = new Person('zs') // 实例对象p
// p.sayHello() // 实例对象p
// console.log(Person.aa) // 123
// console.log(Person.getRandomNum()) // Person
```


