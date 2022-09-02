# 学习目标

> - [ ] 能够说出类的本质
>
> - [ ] 能够说出类和对象的区别
> 
>- [ ] 能够创建一个类并且实例化对象
> 
>- [ ] 能够说出类里面constructor函数的作用
> 
> - [ ] 能够说出什么是静态成员和实例成员
>
> - [ ] 能够说出类里面this的指向
>
> - [ ] 能够使用extends关键字实现类的继承
>   
> - [ ] 能够说出super关键字的作用
> - [ ] 能够使用forEach、filter遍历数组
> - [ ] 能够说出什么是递归函数
> - [ ] 能够说出什么是闭包以及它的主要作用
> 
>。。。。。。

**理解上课的知识点......**



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

![1656170999278](../../../../../../%E5%BE%80%E5%B1%8A%E6%8E%88%E8%AF%BE/%E4%B8%8A%E6%B5%B7-%E5%B0%B1%E4%B8%9A102%E6%9C%9F%EF%BC%88%E7%9B%B4%E6%92%AD%EF%BC%89/04-js%E8%BF%9B%E9%98%B6/day02/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/%E7%AC%94%E8%AE%B0/assets/1656170999278.png)

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

![1656175917786](../../../../../../%E5%BE%80%E5%B1%8A%E6%8E%88%E8%AF%BE/%E4%B8%8A%E6%B5%B7-%E5%B0%B1%E4%B8%9A102%E6%9C%9F%EF%BC%88%E7%9B%B4%E6%92%AD%EF%BC%89/04-js%E8%BF%9B%E9%98%B6/day02/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/%E7%AC%94%E8%AE%B0/assets/1656175917786.png)

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

![1655831351806](../../../../../../%E5%BE%80%E5%B1%8A%E6%8E%88%E8%AF%BE/%E4%B8%8A%E6%B5%B7-%E5%B0%B1%E4%B8%9A102%E6%9C%9F%EF%BC%88%E7%9B%B4%E6%92%AD%EF%BC%89/04-js%E8%BF%9B%E9%98%B6/day02/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/%E7%AC%94%E8%AE%B0/assets/1655831351806.png)



# ES6-类相关 

ES6 :  ECMAScript6, 第6代标准(ECMAScript 2015年发布的标准, 也叫ES2015)  跨时代的年份

> ES5:   ECMAScript5, 第5代标准(2009年发布的标准)
>
> 从ES6开始，每年都会更新一次，并且在新标准下，旧标准中的语法也都会保留，



ES6——》ES2015

ES7——》ES2016

ES8 ——》ES2017

......

ES13——》ES2022



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

1. 拿到拖把
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



## ES6类-给类class中设置构造函数和往原型上添加方法

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



## ES6类-实例成员和静态成员-static（了解）

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



## ES6类-继承-extends

子类可以通过 `extends` 继承父类，把父类的属性和方法，添加到子类的对象上，底层原理还是寄生组合式继承

**寄生组合式继承：**

- 属性继承原理：使用 `call()` 来借调父类构造函数

- 方法继承原理：使用`prototype` 原型链，继承到父类上的方法

  ```js
  // Animal 动物——》name、age、sing()
  // Bird 鸟 ——》name、age、color、fly
  function Animal(name, age) {
      this.name = name
      this.age = age
  }
  Animal.prototype.sing = function () {
      console.log('唱歌')
  }
  
  function Bird(name, age, color) {
      //  借用构造函数
      Animal.call(this, name, age)
      this.color = color
  }
  
  Bird.prototype = Object.create(Animal.prototype)
  Bird.prototype.fly = function () {
      console.log('会飞')
  }
  
  let b1 = new Bird('百灵鸟', 18, 'red')
  console.log(b1)
  b1.sing()
  b1.fly()
  ```

**extends实现类的方法继承：**

```js
// Animal 动物——》sing()
// Bird 鸟 ——》fly
class Animal {
    sing() {
        console.log('唱歌')
    }
}

// Bird 继承 Animal的方法
class Bird extends Animal {
    fly() {
        console.log('会飞')
    }
}

let b2 = new Bird()
b2.sing()
```



## ES6类-继承-子类super

**子类中super的功能：**

1. **子类继承父类的属性：**如果需要借助 `extends` 继承父类的属性，此时需要在子类的构造函数中使用关键字 `super` 借调

   ```js
   class Person {
       constructor(name, age) {
           this.name = name
           this.age = age
       }
       eat() {
           console.log('能吃')
       }
   }
   
   class Student extends Person {
       constructor(name, age, code) {
           // 借用父类构造函数
           // 之前用的是call方法
           // 现在class语法中用的是super()——》固定语法
           // 注意点：一旦用了extends语法，就必须在子类的构造函数中使用super()
           super(name, age)
           // 添加自己独有的属性
           this.code = code
       }
   
       study() {
           console.log('热爱学习')
       }
   }
   
   let stu = new Student('小红', 18, 10086)
   console.log(stu)
   stu.eat()
   stu.study()
   ```

2. **子类中使用父类的方法：** 子类中可以通过super访问到父类中的函数

   ```js
   class Person {
       constructor(name, age) {
           this.name = name
           this.age = age
       }
       eat() {
           console.log('能吃')
       }
   }
   
   class Student extends Person {
       constructor(name, age, code) {
           // 借用父类构造函数
           // 现在class语法中用的是super()——》固定语法
           super(name, age)
           // 添加自己独有的属性
           this.code = code
       }
   
       study() {
           console.log('热爱学习')
           // 现在想吃饭，调用父类的eat方法---------------------------
           super.eat() // 固定语法，用的很少
       }
   }
   
   let stu = new Student('小红', 18, 10086)
   console.log(stu)
   stu.study()
   ```

**注意点：** 一旦用了extends语法，就必须在子类的构造函数中使用 `super()`

##### ヾ(๑╹◡╹)ﾉ" tab栏组件封装-通过class语法

> 把之前写好的tab栏组件封装，改写成class语法的写法

```js
// tab栏数组
let headerArr1 = ['tab1', 'tab2', 'tab3']
// 内容数组
let contentArr1 = ['内容1', '内容2', '内容3']

let headerArr2 = ['头条', '推荐']
let contentArr2 = ['内容1', '内容2']

// 封装成类
class MyTab {
    // 构造函数
    constructor(el, headerArr, contentArr) {
        this.el = document.querySelector(el)
        this.headerArr = headerArr
        this.contentArr = contentArr
        // 创建实例的时候，就直接初始化和注册事件
        this.init()
        this.addClick()
    }

    // 添加方法
    init() {
        let box = this.el
        // 1、创建大盒子
        let headerDiv = document.createElement('div')
        headerDiv.classList.add('header')
        box.appendChild(headerDiv)

        let contentDiv = document.createElement('div')
        contentDiv.classList.add('main')
        box.appendChild(contentDiv)

        // 2、创建子元素
        // 创建tab栏的子元素
        for (let i = 0; i < this.headerArr.length; i++) {
            let span = document.createElement('span')
            let div = document.createElement('div')
            if (i === 0) {
                span.classList.add('active')
                div.classList.add('active')
            }
            span.innerHTML = this.headerArr[i]
            div.innerHTML = this.contentArr[i]
            headerDiv.appendChild(span)
            contentDiv.appendChild(div)
        }
    }

    addClick() {
        let spanList = this.el.querySelectorAll('.header span')
        let divList = this.el.querySelectorAll('.main div')

        // 遍历spanList，给每一个span注册点击事件
        for (let i = 0; i < spanList.length; i++) {
            spanList[i].addEventListener('click', function () {

                // 排他
                for (let i = 0; i < spanList.length; i++) {
                    spanList[i].classList.remove('active')
                    divList[i].classList.remove('active')
                }

                // 给自己添加active类
                spanList[i].classList.add('active')
                divList[i].classList.add('active')

            })
        }
    }
}

let tab1 = new MyTab('#box1', headerArr1, contentArr1)
let tab2 = new MyTab('#box2', headerArr2, contentArr2)
```



# ES6-新增数组方法（重点）

## ES5新增的数组方法

| 对象调用的方法                                               | 作用                            | 返回值       |
| ------------------------------------------------------------ | ------------------------------- | ------------ |
| Array.**forEach**(function(item, index, array){})            | **遍历**                        | 无           |
| Array.**map**(function(item, index, array){})                | **遍历&收集返回的项**           | **新数组**   |
| Array.**filter**(function(item, index, array){ return 条件 }) | **过滤&保留return true的项**    | **新数组**   |
| Array.**reduce**(function(sum, item, index, array) {}, 0)    | **遍历&累计求和**               | **累计结果** |
| Array.**every**(function(item, index, array){ return 条件})  | **遍历&判断是否都满足条件**     | **布尔值**   |
| Array.**some**(function(item, index, array){return 条件})    | **遍历&判断是否有某个满足条件** | **布尔值**   |
| Array.**from**(伪数组)                                       | **伪数组转真数组**              | **真数组**   |

## ES6新增的数组方法

| 对象调用的方法                                             | 作用     | 返回值                   |
| ---------------------------------------------------------- | -------- | ------------------------ |
| array.**find**(function(item, index) { return 条件 })      | 遍历查找 | **找到的项 / undefined** |
| array.**findIndex**(function(item, index) { return 条件 }) | 遍历查找 | **下标 / -1**            |

```js
let arr = [1, 5, 7, 3, 10, 2, 4]
// 1. forEach可以用于遍历一个数组, 每个元素都会执行一次函数
arr.forEach(function(item, index) {
  console.log(item, index)
})

// 2. map() 映射, 遍历数组, 收集每次函数return的结果 - 返回全新数组
let resultArr = arr.map(function(item, index) {
  return item * item
})
console.log(resultArr)

// 3. filter() - 过滤 - 遍历数组, 收集return true的结果, 返回一个新数组
let result2Arr = arr.filter(function(item, index) {
  return item > 5
})
console.log(result2Arr)

// 4. reduce 累加运算 - 遍历数组,需要返回累加的值, 可以进行累加操作
// arr.reduce(function(sum, item, index) { .. }, 起始累加值)
let result3 = arr.reduce(function(sum, item, index) {
  return sum + item
}, 0)
console.log(result3)

// 5. every 每个
// 作用: 遍历一个数组, 每个元素都会执行一次函数, 必须每次执行都返回true, 最终才会返回true
let flag = arr.every(function(item, index) {
  return item > 0
})
console.log(flag)

// 6. some 某个
// 作用: 遍历一个数组, 每个元素都会执行一次函数, 只要有一次执行返回true, 结果就是true
let flag2 = arr.some(function(item, index) {
  return item > 8
})
console.log(flag2)

// 7. Array.from(伪数组) 作用: 将伪数组转换成真数组
let divs = document.querySelectorAll('div')
Array.from(divs).some(function (item, index) {
  if (item.className === 'active') {
    return true
  } else {
    return false
  }
})

// -----------------------------------------------------------
// 8. find 找第一个符合条件的项, 没找到会返回 undefined
let arr2 = [
  { name: 'zs', score: 100 },
  { name: 'ls', score: 99 },
  { name: 'zs', score: 100 }
]
let obj = arr2.find(function(item, index) {
  return item.score === 100
})
console.log(obj)

// 9. findIndex 找第一个符合条件项的下标, 没找到会返回 -1
let index = arr2.findIndex(function(item, index) {
  return item.score === 101
})
console.log(index)
```



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 综合案例：数组操作练习

```js
// 以下是武将信息列表
let list = [
    // wu: 武力    zhi:智力
    { id: 1, name: '张飞', wu: 97, zhi: 10 },
    { id: 2, name: '诸葛亮', wu: 55, zhi: 99 },
    { id: 3, name: '赵云', wu: 97, zhi: 66 },
    { id: 4, name: '周瑜', wu: 80, zhi: 98 },
    { id: 5, name: '吕布', wu: 100, zhi: 8 },
    { id: 6, name: '司马懿', wu: 30, zhi: 98 }
]

// 需求1：求出数组中共所有英雄的武力平均值（求和reduce，再算平均值）
// 需求2：得到一个数组，只保留英雄的名字（遍历每一项并且储存每一项中的值map）
// 需求3：得到一个新数组，只保留武力值超过90的英雄（filter）
// 需求4：判断数组中所有英雄的武力是否都超过60，最终结果为：全是猛将 or 还有弱鸡（every）
// 需求5：删除数组中所有智力低于60的英雄（过滤filter，保留所有智力大于60的武将）
// 需求6：查找id为4的英雄（find）
// 需求7：找到name为吕布的英雄的下标
```



# 函数补充（了解）

## 递归函数

**递归函数：** 在函数内部，自己调用自己，就是递归

**递归函数的两个条件：**

1. 必须在内部，自己调用自己
2. 必须要有出口，必须要有结束条件，否则会出现死递归

![1656272639864](assets/1656272639864.png)

```js
let count = 0
function fn() {
    count++
    console.log('哈哈')
    if (count < 5) {
        fn()
    }
}
fn()
```

##### ヾ(๑╹◡╹)ﾉ" 递归练习：通过递归，求出1~100之间所有的数的和

##### (๑╹◡╹)ﾉ""" 绘图演示

```jsx
// 需求：通过递归，求出1~100之间所有数的和
// 递归：化归思想，将复杂的问题简单化
// 封装：求出 1~n 的和

// getSum(n) = getSum(n-1) + n
// getSum(100) = getSum(99) + 100
//               getSum(99) = getSum(98) + 99
//                            getSum(98) = getSum(97) + 98
// ......
//                                  getSum(2) = getSum(1) + 2
//                                                1
function getSum(n) {
    if (n === 1) {
        return 1
    }
    return getSum(n - 1) + n
}

let result = getSum(100)
console.log(result)

```

![1656272663114](assets/1656272663114.png)

## 闭包

### 闭包的前置认知

函数执行时，会为函数内部的局部变量，开辟储存空间，并在函数执行完成后，释放这块内存空间

**垃圾回收机制（了解）：**

1. 引用计数：IE使用，已经废弃

2. 标记计数：chrome等主流浏览器采用的垃圾回收机制

   - 从全局出发，开始巡查，如果一个内存空间访问不到，就认为该内存空间是垃圾空间，可以被释放
   - 是否可以释放看：是否可以访问到

   ```js
   function fn() {
       let num = 10
       let obj = {
           name: 'zs',
           age: 18
       }
       return obj
   }
   let result1 = fn()
   let result2 = fn()
   ```

### 闭包的介绍

**需求：定义一个计数器函数，统计函数调用的次数**

```js
let num = 0
function count() {
    num++
}
count()
count()
count()
count()

num = 2000
count()
console.log(num)
```

**问题：** 全局变量，因为是全局的，所以哪都能改，容易被别人修改到！不安全

**解决方法：** 闭包——》闭包可以实现数据私有，实现数据缓存（全局变量——》局部变量）

**闭包的含义：** 内层函数，引用外层函数的变量，就可以形成闭包

##### (๑╹◡╹)ﾉ""" 绘图演示

```js
function fn() {
    let num = 0
    function count() {
        num++
        console.log(num)
    }
    return count
}

let resultFn = fn()
resultFn()
resultFn()
```

![1656312863432](assets/1656312863432.png)

##### ヾ(๑╹◡╹)ﾉ" 闭包练习：定义一个计数器，初始值为100，每点击一次按钮，就调用一次计数，实现充币一元

- 用全局变量money储存总数，可以，但是因为可以在任意位置范围，很可能被修改
- 用闭包形成数据私有，让money不会被随意访问，并且完成数据缓存

```jsx
<button id="btn1">充钱1元</button>
<button id="btn2">消费1元</button>
<button id="btn3">关机</button>

<script>
    // 找对象, 找按钮
    let btn1 = document.querySelector('#btn1')
    let btn2 = document.querySelector('#btn2')
    let btn3 = document.querySelector('#btn3')

    // 闭包练习：定义一个计数器，初始值为100，每点击一次按钮，就调用一次计数，实现充币一元
    function GameStart() {
        let money = 0

        // 添加1元
        function add() {
            money++
            console.log(`投币1元，投币成功，余额: ${money}`)
        }

        // 消费1元
        function play() {
            money--
            console.log(`消费1元，消费成功，余额: ${money}`)
        }

        return {
            add: add,
            play: play
        }
    }

    let game = GameStart() // 获取的是一个对象，对象上有需要的方法

    btn1.addEventListener('click', function () {
        game.add()
    })

    btn2.addEventListener('click', function () {
        game.play()
    })

    btn3.addEventListener('click', function () {
        // 释放闭包内存空间
        game = null
    })

</script>
```



# 今日作业

```js
// 思考下面这行代码, 请说出最后的结果 (考察, item是形参, 如果是简单类型的形参的修改, 不会影响到原来值)
let arr = [5, 6, 7, 8];
arr.forEach(function(item){
   item = item + 1;
})
console.log(arr);

let arr2 = [
    { name: 'zs', age: 18 },
    { name: 'zs', age: 20 },
]
arr2.forEach(function(item) {
    item.age = item.age + 1
})
console.log(arr2)
```



```jsx
// 给定一个数组
let studentList = [
  { id: 1, name: '小明', score: 97 },
  { id: 2, name: '小王', score: 55 },
  { id: 3, name: '小刘', score: 85 },
  { id: 4, name: '小刘', score: 80 }
]

1. 请用reduce, 求和后, 算出学生们的平均成绩
2. 请用some判断, 整个班级是否不及格的同学? (60分以下) 
3. 请用find找出, 整个班级中不及格的那一位同学
4. 请用filter筛选出及格的好学生们
```

