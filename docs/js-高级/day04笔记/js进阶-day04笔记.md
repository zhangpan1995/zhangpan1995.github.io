# 学习目标

> - [ ] 能够说出什么是递归函数
> - [ ] 能够说出什么是闭包以及它的主要作用
> - [ ] 能够说出let/const/var的区别
> - [ ] 能够使用数组解构、对象解构
> - [ ] 能够使用箭头函数
> - [ ] 能够使用set数据结构
> 
>。。。。。。

**理解上课的知识点......**



# 函数补充（了解）

## 递归函数

**递归函数：** 在函数内部，自己调用自己，就是递归

**递归函数的两个条件：**

1. 必须在内部，自己调用自己
2. 必须要有出口，必须要有结束条件，否则会出现死递归

![1656272639864](./assets/1656272639864.png)

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

![1656437029543](assets/1656437029543.png)

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

![1656312863432](./assets/1656312863432.png)

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





# ES6相关语法

## 声明变量方式

### 声明变量方式 `let` 和 `var` 的区别

**区别1：**

- let + {} 可以形参块级作用域，在块级作用域通过let声明的块级变量，只能在当前块级作用域中使用
- var 无法形参块级作用域

**区别2：**

- 全局作用域通过let声明的变量，不会挂载到window上
- 全局作用域通过var声明的变量，会被挂载到window上

**区别3：**

- let 必须先声明，在使用
- var 可以先使用，再声明，也不会报错（不严谨）

**区别4：**

- let 不可以重复声明多次
- var 可以重复声明多次，也不会报错



### 声明常量 const

**const常量的特点：**

1. const 用于声明一个常量（不可改变的量），如果强行修改常量的值，会报错
2. let 具有的特性，const都具备，除了不能更改
3. const 常量必须要有初始值

**注意点：**

- 如果const声明的常量中，储存的是一个引用数据类型，那么实际储存的是一个内存地址，只要常量中储存的地址不变，去修改该引用类型的本体，是不会报错的（记忆）



## 解构赋值（重点）

**需求：** 实际开发中，希望把对象、数组中的值取出来，储存到变量中去，方便操作

**解构（拆解结构）：** 按照一种模式，从目标结构（对象、对象）中提取值，赋值给变量

**目的：** 简化了声明变量，并从对象和数组中获取值的步骤

**要求：** 数组解构和对象解构时，要求左右必须结构一致

### 数组解构

**数组解构-完全解构：**

```js
let [one, two, three] = ['yellow', 'green', 'blue']
console.log(one, two, three)

let [, str] = ['yellow', '你好鸭', 123]
console.log(str)
```

**数组解构-部分解构：**

```js
// 用变量储存数组中部分数据——》只解构出 '你好鸭'
let [, str] = ['yellow', '你好鸭', 123]
console.log(str)
```

### 对象解构

**基本语法：**

```js
let obj = {
    name: '小明',
    age: 18,
    desc: '喜欢小红'
}
let { name, age, desc } = obj
console.log(name, age, desc)
```

**解构出多层对象：**

```js
let result = {
    success: true,
    message: '添加用户成功',
    data: {
        name: 'zs',
        age: 20
    }
}
// 需求：结构出result对象的data对象中的name属性
// 方法一：----------------------------------------
let {success,message,data} = result
let {name,age} = data
console.log(name, age)

// 方法二：----------------------------------------
let { success, message, data: { name, age } } = result
console.log(name, age)
```

**对象解构的特殊写法一：解构时变量重命名**

```js
let result = {
    success: true,
    message: '添加用户成功',
    data: {
        name: 'zs',
        age: 20
    }
}
// 需求1：如果data变量在之前的代码已经声明过了，不能再重名了，此时需要换一个名字怎么解构？？
let data = 123
// 解构出data，重命名为res
let {success,message,data:res} = result
console.log(success,message,res)
```

**对象解构的特殊写法二：指定默认值**

```js
let result = {
    success: true,
    message: '添加用户成功',
    data: {
        name: 'zs',
        age: 20
    }
}
// 需求2：如果解构取值时没取到，指定所取属性的默认值（对象上没有就是默认值，有就按照有的设置）
let {success,message,data,age=123} = result
console.log(success,message,data,age)
```



## 箭头函数（重点）

**箭头函数：** 简化匿名函数的写法

```js
(形参) => {
    函数体
}
```

### 基础语法

```js
// 1、无参，无返回值
let fn1 = () => {
    console.log(111)
}
fn1()

// 2、无参，有返回值
let fn2 = () => {
    return 222
}
console.log(fn2())

// 3、有参，无返回值
let fn3 = (num) => {
    console.log(num)
}
fn3(333)

// 4、有参，有返回值
let fn4 = (num) => {
    return num
}
console.log(fn4(444))
```



### 简化写法

1. **如果形参只写一个，可以省略小括号**

   **注意点：** 0个形参、2个形参、3个形参、...... 都不能省略括号

   ```js
   let fn = num => {
       console.log(num)
   }
   fn(222)
   ```

   

2. **如果函数体，只有一句话，大括号可以省略**

   **注意点：** 当函数体省略时，会自动将后面式子的结果返回

   ```js
   let fn = () =>  123
   console.log(fn())
   ```



##### ヾ(๑╹◡╹)ﾉ" 箭头函数的改写练习题

```js
// 给定一个数组
let studentList = [
    { id: 1, name: '小明', score: 97 },
    { id: 2, name: '小王', score: 55 },
    { id: 3, name: '小刘', score: 85 },
    { id: 4, name: '小刘', score: 80 }
]

// 1、请用reduce, 求和后, 算出学生们的平均成绩
let sum = studentList.reduce((sum, item) => sum + item.score, 0)
console.log(sum)
console.log(sum / studentList.length)

// 2、请用some判断, 整个班级是否不及格的同学 ? (60分以下)
let flag1 = studentList.some(item => item.score < 60)
console.log(flag1)
if (flag1) {
    console.log('有不及格的同学')
} else {
    console.log('没有不及格的同学')
}

// 3、请用find找出, 整个班级中不及格的那一位同学
let obj = studentList.find(item => item.score < 60)
console.log(obj)

// 4、请用filter筛选出及格的好学生们
let newArr = studentList.filter(item => item.score >= 60)
console.log(newArr)
```



### 箭头函数的this指向

**箭头函数中的this：** 没有自己的this，在箭头函数中访问this，会访问到外部作用域中的this

**因此：**

1. 如果函数内部原本的this需要，就用普通函数声明
2. 如果函数内部原本的this不需要，此时就用箭头函数声明

**结论：**

1. 箭头函数没有自己的this，访问this时，就近往外部作用域找this
2. 事件处理函数中，不要用箭头函数声明
3. 定时器、延时器、一律都用箭头函数
4. 数组的一堆方法，一律都有箭头函数



### 箭头函数的其他特征

**箭头函数的其他特征：**

1. 箭头函数中没有自己的this，访问this，获取的是外部作用域的this
2. 箭头函数不能作为构造函数，不能配合new一起使用
3. 箭头函数中，没有arguments



## 剩余参数 ...rest 

**问题：** 箭头函数中没有arguments，但是如果需要让箭头函数获取所有参数列表怎么办？

**解决：** 箭头函数没有arguments，但是新语法：剩余参数 rest 语法，可以收集参数列表

```js
let fn = (...arr) => {
    console.log(arr) // 获取到的参数列表
}

fn(1,2,3,4,5,6,7,8,9)
```

**例如：**

```js
// 需求：使用箭头函数，封装一个函数，要求可以传入任意个数个参数，将所有的参数进行求和
let getSum = (...arr) => {
    console.log(arr) // 此时arr获取的是所有参数
    let sum = arr.reduce((sum, item) => sum + item, 0)
    console.log(sum)
}

getSum(1)
getSum(1, 2)
getSum(1, 2, 3)
getSum(1, 2, 3, 4)
getSum(1, 2, 3, 4, 5)
```

**注意点：** 剩余参数 ...rest 固定使用场景——》在函数声明的小括号里面使用



## 展开运算符 ...

### 展开数组

```js
let arr = [1,2,3,4,5]
// 需求：打印数组的每一项？？
console.log(arr[0],arr[1],arr[2],arr[3],arr[4])
console.log(...arr)


// (1) 拼接两个数组
let arr1 = [1,2,3,4,5]
let arr2 = [6,7,8,9,10]
let arr3 = [...arr1,...arr2]
console.log(arr3)


// (2) 求数组的最大值
let arr4 = [11,22,33,44,55,66,77,88]
let max = Math.max(...arr4)
console.log(max)
```



### 展开对象

```js
// 利用展开运算符，可以快速的进行对象的浅拷贝
let obj1 = {
    name:'zs',
    age:18
}

let obj2 = {
    house:'豪华海景大床房',
    car:'五菱宏光'
}

// 需求：obj3中拷贝obj1和obj2所有的属性
let obj3 = {
    ...obj1,
    ...obj2
}
console.log(obj3)
```



## 函数形参默认值

**在ES6中允许我们在函数声明的小括号中，对形参赋予默认值**

**默认值：** 如果没有接收值，那么就会使用默认值

**语法：** `function fn(参数1 = 默认值1，参数2 = 默认值2,) {}`

```js
// 需求：a和b两个形参，在调用的时候，如果a,b没传，就使用默认值 0
function fn(a = 0, b = 0) {
    console.log(a + b)
}
fn(1, 2)
fn(5)
fn()
```



## 对象键值对的简化写法

**对象键值对的简化写法：**

- 对象的属性名和属性值的变量名同名，可以简写
- 对象的属性值是函数，也可以简写

```js
/*
      对象键值对的简写：
        1、对象的属性名和属性值的变量名同名，可以简写
        2、对象的属性值是函数，也可以简写
*/
let name = 'zs'
let age = 18
let desc = '法外狂徒'

let obj = {
    name: name,
    age: age,
    desc: desc,
    sayHi: function () {
        console.log('你好鸭')
    },
    fn: function () {
        console.log('哈哈哈')
    }
}

// 需求：简化上列写法
let obj1 = {
    name,
    age,
    desc,
    sayHi() {
        console.log('你好鸭')
    },
    fn() {
        console.log('哈哈哈')
    }
}

console.log(obj,obj1)
```



## ES6新增数据类型-Set容器（了解）

### Set容器

**Set容器：新对象类型（类似于数组），一些值的集合，但是规定了里面的值不允许重复！！**

**使用场景：** 数组去重

**和数组的区别：**

- **数组：** 可重复的集合
- **Set：** 不可重复的集合