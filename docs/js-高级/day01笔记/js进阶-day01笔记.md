# 学习目标

>- [ ] 能够说出new的执行过程
>- [ ] 能够说出什么是原型(prototype)以及原型的主要作用
>- [ ] 能够画出构造函数、实例、原型对象三者之间的关系
>- [ ] 能够根据原型链说出JavaScript 的对象成员的查找机制
>- [ ] 能够说出不同情况下函数内 this 的指向
>
>。。。。。。



**理解上课的知识点......**

# js进阶-阶段介绍

> js基础部分学习js的基本语法
>
> js高级学习js高级用法和思想

**主体内容：**

- 构造函数的作用
- 构造函数、原型对象、实例对象之间的关系
- 封装自己的插件，如：`new Tab() ` 
- 类的概念、继承的概念、实例化的概念
- 高阶函数
  - 递归函数
  - 闭包
- 深拷贝浅拷贝
- ES6新增的语法使用

**课程安排：**

- 前2天学习, 为了面试, 更深层次的理解JS
- 后2天学习, 为了学习更多的属性和方法



# 构造函数-批量创建对象

> 实际开发中，需要同时创建多个对象——》批量创建对象
>
> 比如：一个注册页面，很多用户注册，每一个用户，储存到js中就是一个对象

## 工厂函数-批量创建对象（了解）

> 工厂函数：把创建对象的过程，封装成函数，就是工厂函数

```js
function createPerson(name, age, desc) {
    let obj = new Object()
    obj.name = name
    obj.age = age
    obj.desc = desc
    return obj
}

// 用户1
let zs = createPerson('zs', 18, '法外狂徒')
console.log(zs)

// 用户2
let ls = createPerson('ls', 21, '检察官')
console.log(ls)

// 用户3
let zl = createPerson('zl', 30, '法官')
console.log(zl)
```

**缺点：**

- 工厂函数内部需要手动创建对象，还需要手动return（麻烦）
- 创建出来的对象都是Object类型，不够具体

## 构造函数-批量创建对象

> 构造函数创建对象可以解决工厂函数的问题

**语法：**

```js
构造函数必须配合new一起使用

创建构造函数：
function 首字母大写函数名() {
    
}

使用：
let 变量名 = new 大写函数名()
```

**示例：**

```js
// 自定义构造函数
function Student(name, age, desc) {
    this.name = name
    this.age = age
    this.desc = desc
}

let stu1 = new Student('张三', 18, '法外狂徒')
console.log(stu1)

let stu2 = new Student('小明', 20, '喜欢小花')
console.log(stu2)
```

**new做的四件事情：**

1. 帮你创建出一个空对象
2. 把构造函数中的this指向了这个空对象
3. 执行构造函数中的代码，通过this可以找到这个空对象，从而添加属性和方法
4. 自动 `return this` 创建好的对象

**构造函数比工厂函数的优势：**

1. 不需要手动声明对象和返回对象
2. 有具体的类型，类型就是当前的构造函数名称



# 原型

## 给实例对象添加方法

### 直接在构造函数中创建（不推荐）

**示例：**

```js
// 问题: 存在内存浪费问题, 通用的函数, 被创建了很多次, 每个对象, 都有自己独立的函数
function Dog(name, age) {
    this.name = name
    this.age = age
    this.lookHouse = function () {
        console.log('会看家')
    }
}

let dog1 = new Dog('二哈', 3)
console.log(dog1)
dog1.lookHouse()

let dog2 = new Dog('阿柴', 4)
console.log(dog2)
dog2.lookHouse()

console.log(dog1.lookHouse === dog2.lookHouse) // false
```

##### (๑╹◡╹)ﾉ""" 画图演示：01-给实例添加方法的问题

**缺点：**每创建一个实例对象，都会创建一个新的函数，很浪费内存

![1655312752525](assets/1655312752525.png)

### 在外部声明函数作为公共方法（不推荐）

> 既然在构造函数中添加方法会浪费空间，那么如果把函数声明在外部，多次使用是否可行呢？

**示例：**

```js
// 在外部声明一个公共的方法，可以解决内存浪费问题——》但是方法多了之后，不好管理
let lookHouse = function () {
    console.log('会看家')   
}

function Dog(name, age) {
    this.name = name
    this.age = age
    this.lookHouse = lookHouse
}

let dog1 = new Dog('二哈', 3)
console.log(dog1)
dog1.lookHouse()

let dog2 = new Dog('阿柴', 4)
console.log(dog2)
dog2.lookHouse()

console.log(dog1.lookHouse === dog2.lookHouse) // true
```

##### (๑╹◡╹)ﾉ""" 画图演示：02-给实例添加公共的方法

**缺点：**当公共方法过多的时候，不方便管理

![1655312927393](assets/1655312927393.png)

### 通过 `prototype` 原型属性设置（推荐）

**原型对象的作用：** 可以集中管理实例们的公共方法

**使用方法：** 把所有的公共方法都通往函数的原型对象上加

**prototype的介绍：**

- 函数本质也是一个对象，也有属性，可以添加属性
- 函数身上有一个内置属性： `prototype` ，对应的属性值就是一个对象（称之为：原型对象）
- 这个prototype属性是js内置的，不需要自己设置，直接使用

**prototype的作用：**

- 通过构造函数创建出来的所有实例对象，都可以共享访问到原型对象的方法或者属性

**示例：**

```js
// 构造函数
function Dog() {

}

// 给函数的prototype属性（原型上添加方法）
Dog.prototype.eat = function () {
    console.log('喜欢干饭！')
}

Dog.prototype.lookHouse = function () {
    console.log('会看家')
}

// 实例对象：通过构造函数new出来的对象，就是实例对象，简称实例
let dog1 = new Dog()
let dog2 = new Dog()

dog1.eat()
dog2.eat()

console.log(dog1.eat === dog2.eat) // true
```

##### (๑╹◡╹)ﾉ""" 画图演示：03-prototype实例对象的介绍

![1655314044810](assets/1655314044810.png)



## `__proto__` 隐式原型

**`__proto__` 介绍：** 每个实例对象都有 `__proto__` 属性，并且该属性就指向构造函数的原型对象

**`__proto__` 作用：** 能够让实例，方便的访问到原型对象，共享到原型里面的方法

**示例：**

```js
// 需求: 给Person构造函数的原型对象上, 添加方法
function Person() {

}

Person.prototype.jump = function () {
    console.log('跳舞')
}

let p1 = new Person()

console.log(p1)
console.log(p1.__proto__)
console.log(Person.prototype)
console.log(p1.__proto__ === Person.prototype)
```

##### (๑╹◡╹)ﾉ""" 画图演示：04-__proto__隐式原型

![1655315348550](assets/1655315348550.png)



## 对象属性赋值规则

**对象属性的访问规则：**

1. 如果对象自己身上有，就用自己的
2. 如果对象自己身上没有，就用原型对象的

**面试题：**

```js
function Person(username, age) {
    this.username = username
    this.age = age
}

Person.username = '小红'
Person.height = 170
Person.prototype.jump = function () {
    console.log('跳舞')
}
Person.prototype.username = '小明'
Person.prototype.weight = 140

let p1 = new Person('小芳', 18)

console.log(p1.username) // 
console.log(p1.age) // 
console.log(p1.jump) // 
console.log(p1.weight) // 
console.log(p1.height) // 
```

##### ヾ(๑╹◡╹)ﾉ" 绘制构造函数+实例+原型对象的关系图

```js
// 绘制构造函数, 实例, 原型对象的关系图
// 需求: 小鸟构造函数, 属性: name age, 方法: fly sing

function Bird(name, age) {
    this.name = name
    this.age = age
}

Bird.dance = function () {
    console.log('蹦迪')
}

Bird.prototype.fly = function () {
    console.log('飞')
}

Bird.prototype.sing = function () {
    console.log('唱歌')
}

let bird1 = new Bird('小红', 18)
console.log(bird1.name)
console.log(bird1.age)
console.log(bird1.fly)
console.log(bird1.sing)
console.log(bird1.dance)
```

##### (๑╹◡╹)ﾉ""" 画图演示：05-绘制构造函数+实例+原型对象三者关系图

![1655318266466](assets/1655318266466.png)

## ------------

## 原型链

**原型链：** 实例可以通过 `__proto__` ，一级一级的往上找到的这层链式关系，就是原型链

**作用：** 研究原型链，可以知道当前实例可以有哪些可以用的属性和方法

**示例：**

```js
// 构造函数
function Person() {

}

// 给原型添加方法 ——》 所有的实例都可以共享访问
Person.prototype.sing = function () {
    console.log("学习唱歌")
}

let zs = new Person()

// zs调用一个看似不存在的方法
console.log(zs.toString())
console.log(zs)
console.log(zs.__proto__)
console.log(zs.__proto__.__proto__)
console.log(zs.__proto__.__proto__.__proto__)
```

##### (๑╹◡╹)ﾉ""" 画图演示：06-原型链的介绍

![1655391443817](assets/1655391443817.png)

##### ヾ(๑╹◡╹)ﾉ" 绘制数组的原型链

##### (๑╹◡╹)ﾉ""" 07-绘制数组的原型链

```js
// 1. 思考1: 创建出来的每个数组, 都能调用 push 方法, 为什么?
// 2. 思考2：我们研究原型，原型链的目的是什么？ =>  研究出实例, 到底有哪些属性和方法可以访问到
// 3. 课外小练习: 绘制完整的 date实例 原型链

let arr = new Array()
arr.push(123)
console.log(arr)
console.log(arr.__proto__)
console.log(arr.__proto__.__proto__)
console.log(arr.__proto__.__proto__.__proto__)
console.log(arr.__proto__.__proto__ === Object.prototype)
```



**总结：**

- 为什么要有构造函数——》批量创建对象
- 为什么需要原型对象（prototype）？——》让所有实例，共享方法，节省内存
- 为什么需要有隐式原型（`__proto__`）？——》让对象，方便的调用更多的属性和方法

**问题：**

1. 为什么所有的日期对象都有getFullYear,getMonth,getDate...等方法 

   > 定义在 Date.prototype 中, 只需要定义一次

2. 为什么所有的数组都有push,pop,join,sort...等方法  

   > 定义在 Array.prototype 中, 只需要定义一次

3.  为什么所有的数组, 对象, 字符串,数字 都可以使用toString

   > 都是因为有我们的原型, 原型链



## instanceof的使用

> 实际开发中，需要更加准确的判断数据的类型

**判断数据类型：**

- `typeof 数据` ：仅能用于判断简单类型，如果是复杂数据类型结果都是 `object` ，无法准确判断
- `实例 instanceof 构造函数` ：看构造函数的原型，在不在实例的原型链上
  - 如果构造函数的原型在当前实例的原型链上，此时就可以用当前构造函数原型上的方法
  - 返回值：布尔值

**typeof 示例：**

```js
// typeof 仅用于判断简单数据类型, 如果是复杂数据类型就不行了
console.log(typeof 1) // 
console.log(typeof true) // 
console.log(typeof 'abc') // 
console.log(typeof undefined) // 
console.log(typeof null) // 
console.log(typeof [])  // 
console.log(typeof {})  // 
function Person () {}
let p = new Person()
console.log(typeof p)  //
```

**instanceof示例：**

```js
function Person() { }
let p = new Person()
let arr = []
let obj = {}

// 判断是否是Person类型
console.log(p instanceof Person) // 
console.log(arr instanceof Person) // 
console.log(obj instanceof Person) // 

// 判断是否是Array类型
console.log(p instanceof Array) // 
console.log(arr instanceof Array) // 
console.log(obj instanceof Array) // 

// 判断是否是Object类型
console.log(p instanceof Object) // 
console.log(arr instanceof Object) // 
console.log(obj instanceof Object) // 
```

**注意点：**

1. 如果instanceof的结果为true，那么构造函数原型上的方法，实例可以访问到
2. 如果要用instanceof来判断类型，一般会有更具体的构造函数，而不是使用object



##### ヾ(๑╹◡╹)ﾉ" 类型判断练习题

##### 判断是否是数组，如果是数组可以内部添加内容

```js
// 请正确的往每个小数组里, 添加一个数字666, 保证代码不错 [{}, [], {}, []],使用循环判断
// 重点: 判断是否是数组, 是数组才往里面加
// 思路:
// 1. 封装一个方法, 判断数据类型
// 2. 调用方法判断, 添加
let arr = [{}, [], {}, []]
```



##### ヾ(๑╹◡╹)ﾉ" 封装一个判断类型的函数

> 考虑复用，将来很多地方，都要进行判断类型

```js
// 需求：封装一个判断类型的函数，函数传入实参，会返回该实参的数据类型
// 返回结果：
// 简单数据类型：number、string、boolean、undefined、null
// 复杂数据类型：array、function、object

function getType() {
    // 1、先判断是不是简单数据类型：number、string、boolean、undefined、null、
    // 2、不是简单数据类型，在判断是不是：null、object、array

}


console.log(getType(1)) // number
console.log(getType('abc')) // string
console.log(getType(true)) // boolean
console.log(getType(undefined)) // undefined
console.log(getType(null)) // null
console.log(getType([])) // array
console.log(getType({})) // object
```



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

![image-20210220133907898](./assets/image-20210220133907898.png)

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

**4、硬绑定：** 想让this指向谁就是谁（后续介绍）



**小结：**

1. 默认绑定：指向window——》fn()、定时器、延时器
2. 隐式绑定：指向调用者——》obj.fn()、事件处理函数
3. new绑定：指向当前创建的实例——》new Person()
4. 硬绑定：想让this指向谁就是谁——》明天介绍



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



# 经验值 

## 问题：对构造函数进行实例化有报错

* 描述：准备好构造函数，进行实例化操作获取对象，出现报错：

![1597491998063](./assets/1597491998063-1599123264329.png)

* 分析：

  * 控制台有报错的话，直接找到报错的位置进行分析；

  ```js
  let person_1 = New Star("zhangs", 18);
  ```

  * 报错分析：意外？哪里意外了？

  ```
  Unexpected identifier：意外的标识符
  ```

  * 我们说构造函数的函数名一般情况下大写，但是进行实例化的时候，其前面的关键字可不是大写；

* 解决：`new Star("zhangs", 18);`

* 总结：语法记忆一定要清晰，不要张冠李戴；



**测试：**下面实例化正确的是？

```js
function Star(name, age) {
    this.name = name;
    this.age = age;
}

A new Star(1,2);
B newStar(1,2);
C New Star(1,2);
D Star new(1,2);
```



## 问题：构造函数的原型对象上设置方法，实例化对象调用时报错

* 描述：原型对象上设置方法sing，实例化p1调用时有报错找不到该函数；

![1597492618949](./assets/1597492618949-1599123264330.png)

* 分析：

  * 报错提醒在44行，查看44处代码：`p1.sing();`
  * p1只是个实例化对象，如果实例化对象报错找不到sing这个方法，那么意味着其构造函数的原型对象上该方法设置有问题
  * 打印`p1.__proto__`：发现其`__proto__`对象上此时是一个名为sing的函数方法；

  ![1597492743546](assets/1597492743546-1599123264330.png)

  * `__proto__`和 `构造函数的prototype` 在内存上共用同一个堆地址，于是找到 `prototype`

  ```js
  Star.prototype = function sing() {
      console.log(1);
  }
  ```

  * prototype默认为构造函数的原型对象，是一个对象，上面的代码对这个属性名重新赋值为函数，所以会报错；

* 解决：prototype默认为构造函数的原型对象，原型对象上添加新的方法为：

```js
Star.prototype.sing = function() {
    console.log(1);
}
```

* 总结：各语法都有基本的规则和用法；同学们在使用的过程中应该记忆一些核心的规则；


**测试：**下面在构造函数**Star**的原型对象上进行设置方法，正确的是？

```js
A new Star.prototype.sing = function(){};
B Star.__proto__.sing = function(){};
C Star.prototype.star = function(){};
D Star.__prototype__.sing = function(){};
```

# 今日作业

```js
// 需求1: 尝试给现在系统的Array构造函数添加一个取最大值得函数, 确保下面代码正确
// 提示: 对象调用函数, 本身没有会去哪里找? 所以在调用之前可以在Array函数, 的什么位置上扩展添加方法呢?

/*这里应该补充什么代码呢?*/

let arr1 = [100,200,5];
console.log(arr1.getMax()); // 200

let arr2 = [5, 2, 1, 10, 3, 4];
console.log(arr2.getMax()); // 10

// 需求2: 给系统Date构造函数, 添加一个toMyString函数 - 调用函数, 得到今天日期YYYY年MM月DD日 HH:mm:ss 格式的时间
let date = new Date()
console.log(date.toMyString()) // YYYY年MM月DD日 HH:mm:ss格式
```