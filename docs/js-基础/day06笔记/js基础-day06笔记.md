# 学习目标

>  - [ ] 能够自定义创建对象
>- [ ] 能够使用对象的属性和方法（点语法和中括号语法）
> - [ ] 能够for...in遍历对象的所有属性
> - [ ] 能够说出Math对象的至少3个方法
> - [ ] 能够画出简单类型和复杂类型在内存中的存储
> 
> 。。。。。。



**理解上课的知识点......**



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 综合案例：用户输入秒数，将总秒数转换成x小时x分钟x秒

![111](../../../../../../%E5%BE%80%E5%B1%8A%E6%8E%88%E8%AF%BE/%E4%B8%8A%E6%B5%B7-%E5%B0%B1%E4%B8%9A102%E6%9C%9F%EF%BC%88%E7%9B%B4%E6%92%AD%EF%BC%89/02-js%E5%9F%BA%E7%A1%80/day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/%E7%AC%94%E8%AE%B0/js%E5%9F%BA%E7%A1%80-day05%E7%AC%94%E8%AE%B0.assets/111.gif)

# 对象（object）

## 为什么学习对象？

**数组的作用：** 用于储存大量的数据，一般储存的是同类型数据

**对象的作用：** 万物皆对象，**一个具体的事物就是一个对象**，在现实生活中只要能被描述出来的就是对象

```js
人类、棠哥、班主任、102期的刘静、手机、我手里的iPhone......
```

**比如：注册页中用户需要填写自己的信息，在js中需要储存这个用户的信息，怎么做？**

> 一个具体的用户，就是一个对象，此时就需要在js中需要储存现实生活中的对象了

**描述人这个对象：**

- 特征：姓名、年龄、性别、身高、体重......
- 行为：吃饭、睡觉、敲代码......

**解决方案：**

- **用变量储存：**需要一个一个的单独储存 → 代码麻烦冗余，不方便管理

  ```js
  // -------------------静态特征
  let name = "张三"
  let age = 18
  let sex = "男"
  let height = 180
  let weight = 150
  // -------------------动态行为
  let eat = function () {
      console.log('吃饭')
  }
  let sleep = function () {
      console.log('睡觉')
  }
  //-------------------变量太多麻烦
  ```

- 使用数组存 → 数组规范一般储存同类型的数据，并且数组中的数据用户不明白分别表示什么意思

  ```js
  let arr = ['张三',18,'男',180,150]
  //-----------------------数组一般只存储同类型的数据，并且这样写每一项不明确表示什么含义
  ```

- 如果需要描述现实中的对象，此时就需要通过js中的对象完成！



## 对象的基本概念

**数组：**  一组有序的值的集合 → 下标有序

**对象：** 一组**无序的键值对的集合** → 可以用于描述生活中对象的特征与行为

> 键值对就是类似于之前css中的样式
>
> 格式：**键：值 → key：value**



## 创建对象的方法

- **字面量（用的最多）**

  > 123、'abc'、true、undefined、null、[]、{}

  ```js
  let obj = {} // 创建一个空对象
  console.log(obj)
  //----------------------------
  let obj = {
      // ------------静态特征——》对象的属性
      name:"张三",
      age:18,
      sex:"男",
      height:180,
      weight:150,
      // ------------动态行为——》对象的方法（对象中的函数）
      eat:function (){
          console.log('吃饭')
      },
      sleep:function (){
          console.log('睡觉')
      }
  };
  console.log(obj)
  ```

  **注意点：** 

  - 键值对之间以逗号隔开
  - 对象中的静态特征叫做**对象的属性**
  - 对象中的动态行为（函数）叫做**对象的方法**

- **Object构造函数**

  ```js
  let person = new Object() //创建一个空的对象
  //------------------------------
  let person = new Object({
      name:"张三",
      age:18,
      sex:"男",
      height:180,
      weight:150,
      eat:function (){
          console.log('吃饭')
      },
      sleep:function (){
          console.log('睡觉')
      }
  })
  ```

---

**小结：**

1. 对象中的属性之间，有顺序之分吗？
   - 
2. 对象中，属性名和属性值之间用什么符号隔开？属性与属性之间以什么符号隔开？
   - 

---



##### ヾ(๑╹◡╹)ﾉ" 1、创建对象的练习

![image-20210910205301617](js基础day06笔记.assets/image-20210910205301617.png)

创建一个商品对象，对象中包括以下信息：

**要求：**

1. 对象名可以是：`goods`
2. 商品名词属性名：`name`
3. 商品编号属性名：`num`
4. 商品毛重属性名：`weight`
5. 商品产地属性名：`address`



## 对象属性的取值与赋值-点语法

**对象的取值：**

- **对象名.属性名**

  ```js
  let person = {
      name:'张三'
  }
  
  console.log(person.name)
  console.log(person.height)
  ......
  ```

  **注意点：**

  - 如果属性名存在，获取对应的值
  - 如果属性名不存在，返回undefined

- **对象名.方法名**

  1. 如果取值的是对象的方法，此时返回的是方法的函数体。如：`console.log(person.eat)`

2. 对象的方法一般是不会直接打印，而且进行调用。如：`person.eat()`

**对象的赋值：**

- **对象名.属性名 = 值**
  - 如果属性名存在，被覆盖
  - 如果属性名不存在，添加一个新属性



## 对象属性的取值与赋值-中括号语法

### 点语法和中括号语法的介绍

> 之前对于对象的取值与赋值，使用的是点语法

**点语法：**

- 取值：`对象名.属性名`
- 赋值：`对象名.属性名 = 值`

---

**中括号语法：**

> 中括号语法也叫做关联数组语法，类似于把对象看做是数组取值

- 取值：**对象名["属性名"]**
- 赋值：**对象名["属性名"] = '值'**



### 点语法与中括号语法的区别

> 两种方法都能使用，但是 **只有中括号语法中支持变量**

- **点语法：对象名.属性名** → 简洁 → 只能写属性名，**不支持变量（不管变量）**
- **中括号语法：对象名['属性名']**  → 灵活 → 可以写写字符串或者变量

```js
// 下列分别访问的是对象的什么属性
// 1、
obj.name // obj的？？？属性

// 2、
let str = 'age'
obj.str // obj的？？？属性


// 3、
obj['height'] // obj的？？？属性


// 4、
let str = 'weight' 
obj[str] // obj的？？？属性
```



### 中括号语法的使用场景

> 如果访问的属性名是一个变量，必须使用中括号语法



##### ヾ(๑╹◡╹)ﾉ" 2、遍历数组，将数组每项（即对象）的属性渲染到页面中案例

```js
let students = [
    { name: '小明', age: 18, gender: '男', hometown: '河北省' },
    { name: '小红', age: 19, gender: '女', hometown: '河南省' },
    { name: '小刚', age: 17, gender: '男', hometown: '山西省' },
    { name: '小丽', age: 18, gender: '女', hometown: '山东省' }
]
```

![image-20220102154056752](js基础day06笔记.assets/image-20220102154056752.png)

**步骤：**

1. 先在网页中打印出公共不需要变化的表格头部和尾部
2. 中间部分遍历数组，将数组中的每一项（即每个对象）的属性通过模板字符串渲染到页面中去



## 遍历对象

**遍历对象：**一个一个的访问对象的全部属性

- 对象没有像数组一样的length属性，所以无法确定长度
- 对象里面是无序的键值对，没有规律，没有数组中有规律的下标

**遍历对象语法：**

```js
// --------------------key——》键——》是一个变量可以变化
// --------------------obj——》需要遍历的对象
// --------------------obj[key]——》对应的值
for(let key in obj) {
    console.log(key)
    console.log(obj[key])
}
```

##### ヾ(๑╹◡╹)ﾉ" 3、遍历对象的练习

```js
// 需求: 将所有 obj2 的属性, 添加到 obj 中去
let obj = {    
    name: '张三',    
    age: 30
};

let obj2 = {    
    money: 1000000,    
    car: '玛莎拉蒂'
};

// 1、可以一个一个的添加，但是通用性不好（属性变了之后代码也需要变）
// 2、可以遍历数组动态的把所有的数据都添加上
```



# 内置对象

> JS内置对象就是指Javascript自带的一些对象，供开发者使用，这些对象提供了一些常用的的功能。
>
> 常见的内置对象有Math、String、Array、Date等

## Math对象

> Math对象中封装很多与数学相关的属性和方法，需要时直接使用Math对象即可，不需要声明

- **圆周率**

  `Math.PI`

- **最大值/最小值**

  ```js
  Math.max(1,2,3,4,5,6)
  Math.min(1,2,3,4,5,6)
  ```

- **取整**

  ```javascript
  Math.ceil()
  //天花板，向上取整，取大的那个
  Math.floor()
  //地板，向下取整，取小的那个
  Math.round()
  //四舍五入，如果是.5，则取更大的那个数
  console.log( Math.ceil(1.1) )
  console.log( Math.ceil(1.9) )
  console.log( Math.ceil(-1.1) )
  console.log( Math.ceil(-1.9) )
  ```

- **随机数**

  ```javascript
  Math.random();//返回一个[0,1)之间的数，能取到0，取不到1
  ```



##### ヾ(๑╹◡╹)ﾉ" 4、随机获取0、1、2这三个数

```js
// --------------获取0~2.9999的随机数
Math.random()*3
//---------------只需要把小数点之后的去掉即可
parseInt(Math.random()*3)
```

> 求0~n的整数随机数
>
> `parseInt(Math.random()*(n+1))`



##### ヾ(๑╹◡╹)ﾉ" 5、简单的随机点名效果

```js
// 每次刷新打印的名字随机——》能随机获取下标即可
let arr = ['张三','李四','王五','赵六','田七','老王']

// 随机获取下标：  0 ~ arr.length-1
let index = parseInt(Math.random() * arr.length)
console.log(index)
console.log(arr[index])
```



##### ヾ(๑╹◡╹)ﾉ" 6、随机生成一个rbg颜色

```js
let colorA = parseInt( Math.random() * 256 )
let colorB = parseInt( Math.random() * 256 )
let colorC = parseInt( Math.random() * 256 )
let str = 'rgb('+ colorA + "," + colorB + ',' + colorC +')'
console.log(str)

// 使用ES6的模板字符串更加方便
let color = `rgb(${r},${g},${b})`
console.log(color)

//----------------------设置body的颜色（web api内容）
document.body.style.backgroundColor = str
```

- **绝对值**

  ```javascript
  Math.abs()
  //求绝对值
  //-----------------------------
  console.log(Math.abs(1)) // 1
  console.log(Math.abs(-1)) // 1
  ```

- **次幂（次方）**

  ```javascript
  Math.pow(num, power) // 求num的power次方
  //-----------------------------
  console.log(Math.pow(3, 2)) // 3的平方  9
  console.log(Math.pow(10, 3)) // 10的三次方 1000
  console.log(Math.pow(100, 0.5)) // 100的开方  10
  ```

- **开平方**

  ```js
  Math.sqrt(num) // 对num开平方
  //-----------------------------
  console.log(Math.sqrt(9)) // 3
  ```



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 综合案例：学成在线页面渲染案例

> 把数组对象

```js
let data = [
    {
        src: 'images/course01.png',
        title: 'Think PHP 5.0 博客系统实战项目演练',
        num: 1125
    },
    {
        src: 'images/course02.png',
        title: 'Android 网络动态图片加载实战',
        num: 357
    },
    {
        src: 'images/course03.png',
        title: 'Angular2 大前端商城实战项目演练',
        num: 22250
    },
    {
        src: 'images/course04.png',
        title: 'Android APP 实战项目演练',
        num: 389
    },
    {
        src: 'images/course05.png',
        title: 'UGUI 源码深度分析案例',
        num: 124
    },
    {
        src: 'images/course06.png',
        title: 'Kami2首页界面切换效果实战演练',
        num: 432
    },
    {
        src: 'images/course07.png',
        title: 'UNITY 从入门到精通实战案例',
        num: 888
    },
    {
        src: 'images/course08.png',
        title: '我会变，你呢？',
        num: 590
    },
    {
        src: 'images/course08.png',
        title: '我会变，你呢？',
        num: 590
    }
]
```



![image-20220102155647786](js基础day06笔记.assets/image-20220102155647786.png)



**思路：**遍历数组，将数组中的每一项（即每个对象）的属性通过模板字符串渲染到页面中去

**注意点：** `script` 标签写在哪里，`document.write()` 中渲染的内容就会显示在html标签的哪里



# 拓展：值类型与引用类型

**简单数据类型（值类型）：**number、string、boolean、undefined、null

**复杂数据类型（引用类型）：** Array、Object、Function

> 从内存角度上划分，可以把数据分为值类型与引用类型。

---



**简单数据类型（值类型）：**在储存时，变量中储存的是**值本身**！！

> 简单数据类型在内存角度储存在**栈内存**中

**复杂数据类型（引用类型）：** 在储存时，变量中储存的是内存地址！！

> 复杂数据类型在内存角度储存在**堆内存**中

![image-20220102161641672](js基础day06笔记.assets/image-20220102161641672.png)



## 值类型与引用类型的内存分布

##### (◕ᴗ◕✿)画图说明值类型内存分布

> 值类型变量中存的是值本身

```js
// 变量和简单数据类型储存在栈内存
let num = 10
console.log( num )
```

##### (◕ᴗ◕✿)画图说明引用类型内存分布

> 引用类型变量中存的是内存地址

```js
// 赋值数据类型无法直接储存到栈内存中，会储存在堆内存中
let obj = {    
    name:'zs',    
    age:18
}
console.log( obj.name )
```



## 值类型与引用类型的赋值特征

- 值类型变量中存的是值本身，所以赋值给其他变量时，赋值的就是值本身

  ##### (◕ᴗ◕✿) 画图演示

  ```js
  let num = 10
  let num2 = num
  num2 = 20
  console.log(num)
  console.log(num2)
  ```

- 引用类型变量中存的是内存地址，所以赋值给其他变量时，赋值的是内存地址

  ##### (◕ᴗ◕✿) 画图演示

  ```js
  let obj = {    
    name:'jj',    
    age:18
  }
  let obj2 = obj
  obj2.name = 'tg'
  console.log(obj2.name)
  console.log(obj.name)
  ```

##### ヾ(๑╹◡╹)ﾉ" 面试题

```js
let a = []
let b = a
console.log(a === b) // ??

let c = {}
let d = c
console.log(c === d) // ??

let e = []
let f = []
console.log(e === f) // ??

console.log({} === {}) // ?? 
```

