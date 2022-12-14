# 学习目标

>- [ ] 能说出JavaScript三部分组成
>- [ ] 能够使用变量来存储数据
> 
> - [ ] 能够说出变量的命名规范
> - [ ] 能够写出交换两个变量的值 
>
>- [ ] 能够说出JavaScript中的基本数据类型
>- [ ] 能够把其它转换成Number类型/String类型
> 
> 。。。。。。。。



**理解上课的知识点......**



# JavaScript 基本介绍（了解）

## 我们最开始认识的JS

`WEB` 标准的三部分（网页的三大部分）

- **HTML**：控制页面的**结构**
- **CSS**：控制页面的**样式**
- **JavaScript**：控制网页的**行为**（动态效果）



## 什么是 JavaScript

> JavaScript是一种运行在 **客户端（浏览器）** 的 **脚本语言** ，现在也可以运行在服务器端 

不同于 `HTML` 和 `CSS` ，`JavaScript` 是一门**编程语言**，因此比 `HTML` 和 `CSS` 会更加复杂一下，学习的时间也会更长。



## JavaScript的作用

>在学习 `JS` 之前，首先要明白JS的作用是什么？
>
>远古时期：表单校验
>
>现在：无所不能

#### 最初的JavaScript：表单校验

- 用于判断表单的输入是否正确（表单校验）

#### 现在的JavaScript：无所不能

- 前端的本职工作：网页特效
- 后端的事情也能做：服务端编程（`nodejs`）
- 前后端数据交互：数据交互（`AJAX`）

- 命令行工具开发（`nodejs`）
- 桌面程序（`Electron`）
- app开发（`ReatNative`）
- 控制硬件：物联网（`Ruff`）
- 游戏开发（`cavans`）
- 等等......

演示：[Canvas游戏](https://www.html5tricks.com/8-html5-canvas-animation.html) [美女相册](http://www.webhek.com/post/3d-album.html)

----

**小结：**

1. js全称是什么？
   - javascript
2. js的作用有哪些？
   - 早期：表单校验
   - 现在：无所不能
     - 前端的特效
     - 后端服务器的代码
     - 前后端的数据交互
     - 命令行工具
     - 手机app
     - 微信小程序
     - ......

---



## JavaScript的组成 (记忆)

> `JavaScript`  =  `ECMAScript` + `DOM` + `BOM`

![image-20211222143454987](js基础-day01笔记.assets/image-20211222143454987.png)

- **ECMAScript（JavaScript的核心）**：ECMAScript是一套标准，规范了语言的基本语法。 

  > 比如：变量 `let`、分支语句 `if`、循环语句 `for`等等

- **DOM**（**Document** Object Model）：一套操作网页元素的方法 

  > 比如：控制页面元素进行移动、改变大小、添加删除等操作

- **BOM**（Browser Object Model）：一套操作浏览器功能的方法

  > 比如：浏览器的页面前进后退、检测浏览器窗口宽度等操作

---

**小结：**

1. js由哪些部分组成？每个部分的含义是什么？
   - ECMAScript：一套语言标准，指定了js语言的语法
   - DOM：文档对象模型：一套操作网页元素的方法
   - BOM：浏览器对象模型：一套操作浏览器功能的方法

---



# JavaScript入门

## JS的书写位置

> js的书写位置和css的书写位置有点相似

![image-20211222143807657](js基础-day01笔记.assets/image-20211222143807657.png)

- **内嵌式：把js写在`script`标签中**

  ```html
  <script>
    alert('hello world')
  </script>
  ```

- **外联式：把js写在一个单独的.js文件中，通过script的src属性引入即可**

  ```html
  <script src="demo.js"></script>
  ```

- **行内式：把js写在标签内部（当前阶段不推荐，后期vue阶段才会用到）**

  ```html
  <button onclick="alert('我是一个弹框')">点我出弹框</button>
  ```

  

**注意点：**

- `script` 标签理论上可以写在页面的很多位置，但是一般会写在 `body` 标签内容的最后
- 带有 `src` 属性的 `script` 标签内部的 `js` 代码，浏览器会直接忽略

---

**小结：**

1. js常见书写位置有哪几种？
   - 
2. 在带有 `src` 属性的script标签内部，书写的js代码，浏览器会不会执行呢？
   - 

---



## JS注释

> 注释的作用：代码中可以看到，但是浏览器会忽略不执行。注释起到代码注解的作用。
>
> 开发时需要养成写注释的好习惯~

- **单行注释**

  ```js
  // 这是单行注释， 单行注释只能注释一行代码
  // 快捷键： ctrl + /  
  // 注释的内容
  ```

- **多行注释（块注释）** 

  ```js
  /*
      这是多行注释，多行注释中可以注释多行
      快捷键：alt + shift + a
  */
  /* 注释的内容 */
  ```

---

**小结：**

1. 单行注释的快捷键是？
   - 
2. 多行注释（块注释）的快捷键是？
   - 

---



## js中的结束符

![image-20211223164504917](js基础-day01笔记.assets/image-20211223164504917.png)

**结束符：**

- 结束符表示语句结束，写法为英文分号 `;`
- 在js中可写可不写（现在有很多的程序员在js中不写结束符）
- 因为js代码中换行会被识别成结束符，所以一个完整的语句中，不要随意换行
- 为了代码风格统一，要么每句都写结束符 `;` ，要么每句都不写结束符（按照团队要求）



## JS中常见5种输出语句（记忆）

- **alert ： 弹框**

  ![alert](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/alert.png)

  ```js
  // alert：弹出一个：弹框/警告框/提示框/弹窗
  alert("hello world") 
  ```

- **confirm ： 确认框**

  ![confirm](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/confirm.png)

  ```js
  // confirm：弹出一个确定框
  confirm("棠哥帅不帅？") 
  ```

- **prompt ： 输入框**

  ![prompt](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/prompt.png)

  ```js
  // prompt：弹出一个输入框，可以输入内容
  prompt("请输入谁是最靓的仔？") 
  ```

- **document.write ： 网页中写入内容**

  ![document](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/document.png)

  ```js
  // document.write：在网页中写入内容，可以识别标签
  document.write("我是一段文本") 
  document.write("<h1>我是一个h1标签</h1>") 
  ```

- **console.log ：控制台打印数据**

  ![log](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/log.png)

  ```js
  // console.log：在控制台中输出信息（打印）信息
  console.log("hello word") 
  ```

**注意点：**

- `alert`、`comfirm`、`prompt` 此类弹出框用户体验不好，开发中极少用到，一般仅会在学习过程中使用。
- `console.log`经常用来打印数据，项目调试的时候非常有用！

---

**小结：**

1. `弹框` 的js语句是什么？
   - 
2. `确认弹框 `的js语句是什么？
   - 
3. `输入弹框` 的js语句是什么？
   - 
4. `网页中输入内容 `的js语句是什么？
   - 
5. `控制台打印` 的js语句是什么？
   - 

---

##### ヾ(๑╹◡╹)ﾉ" 1、输出语句练习

写一段js代码，完成以下需求：

1. 先弹出弹框：`欢迎打开该网页`
2. 再弹出确认弹框：`是否进入 JS 的世界？`
3. 再弹出输入弹框：`请输入您的名字`
4. 再在网页中显示h1标签的效果：`这是我用 JS 代码在网页中显示的大标题`
5. 最后在控制台中打印：`以后我们会经常在控制台打印数据哦~`



# 变量

## 变量初体验

**变量：** 可以变化的量（相当于一个储存数据的容器）

![image-20211223171739243](js基础-day01笔记.assets/image-20211223171739243.png)

**作用：** 储存数据

在使用变量之前需要先声明，才能使用变量。（相当于先做出一个容器，才能装东西）

**声明：** `let 变量名;`

**比如：** 用变量储存用户的年龄（年龄是不断变化的）

---

**小结：**

1. 可以怎样理解变量？
   - 
2. 规范要求：使用变量前，需要先做什么？
   - 
3. 如何在变量中储存数据？
   - `

---

##### ヾ(๑╹◡╹)ﾉ" 2、变量初体验练习

写一段 `js` 代码，完成以下需求：

1. 声明一个变量：`name` ，用于存放用户的姓名为：`'张三'`
2. 声明一个变量：`age` ，用于存放用户的年龄为：`18`
3. 依次在控制台中打印输入以上两个变量。



## 使用变量的常见形式（了解）

> 规范：使用变量前，必须先声明！
>

- **写法一：** 先声明后赋值

  ```js
  let age // 声明一个变量 age
  age = 18 // 一个等号表示赋值（把等号后面的赋值给前面的！）
  console.log(age)
  ```

- **写法二：** 同时声明和赋值

  ```js
  let age2 = 20
  console.log(age2)
  ```

- **写法三：** 同时声明多个变量且赋值

  > **用的不多** ，其实只是省略了一个let。

  ```js
  // ， => 并列
  let age3 = 30,age4= 40
  // 相当于-----------------------------
  let age3 = 30
  let age4 = 40
  ```

---

- **错误写法1：**直接声明变量，不赋值

  > 变量的默认值是undefined

  ```js
  let age5
  console.log(age5) // undefined =》 表示只声明，没有赋值
  ```

- **错误写法2：**不声明变量，直接赋值

  > 虽然浏览器可以识别，但是**不推荐**，这种写法之后会出现问题！！

  ```js
  // 不推荐 ，不符合规范
  age6 = 60
  console.log( age6 )
  ```

- **错误写法3：**不声明变量，也不赋值变量，直接使用

  > **绝对不能这样写，会报错！！！**

  ```js
  // age7 is not defined 表示是没有定义（说白了就是没有声明和赋值直接使用）
  console.log(age7)
  ```

**注意点：**

- `JS` 代码一旦报错了，报错之后的代码浏览器不会执行
- 开发规范要求：变量需要声明后，再使用。同学们需要养成良好的编程习惯

---

**小结：**

1. 规范要求：使用变量前，需要先做什么？
   - 
2. 变量如果只声明，未赋值，变量的默认值是什么？
   - 
3. 如果一个变量未声明，未赋值，直接使用，会出现什么结果？
   - 
4. 如果js中代码报错，报错之后的代码会执行吗？
   - 

---



## 变量的命名规则和规范

### 命名规则

> 类似于法律：必须遵守！不遵守会报错！

- 由 `数字`、`字母`、`_` 、`$` 组成 ，并且不能以数字开头

  下列变量名是否符合规则?

  ```
  a	    
  1
  age18
  18age
  2b
  name
  $name
  _sex
  &sex
  theworld
  a b
  ```

- 区分大小写

  > 大写的变量和小写的变量表示两个不同的变量

- 不能是**关键字**或**保留字**

  > js中和语法相关的单词，不能作为变量名
  >
  > 不用同学们专门记忆，随着学习的深入不断会使用到

  **关键字**：现在版本中语法相关的单词

  ![key1](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/key1.png)

  **保留字**：未来版本中语法相关的单词

  ![key2](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/key2.png)

### 命名规范

> 类似于道德，建议遵守，不遵守也不会报错

- 变量名要有意义

- 遵守**小驼峰命名法**， 从第二个单词开始首字母大写！

  > 为了可读性更好

  比如：userName、userAge

---

**小结：**

1. 变量名可以由哪些部分组成？
   - 
2. 变量 `NAME` 和 变量 `name` 是同一个变量吗？
   - 
3. 变量名可以是js中有特定含义的单词吗？
   - 
4. 多个单词组合的变量名，最好使用怎样的写法？
   - 

---


##### ヾ(๑╹◡╹)ﾉ" 3、变量赋值练习

```js
// 1. 
let  a = 10    
a = 20
console.log(a) // ??

// 2.
let a = 20
let b = a // 把a的值赋值给b
console.log(b) // ?? 
```



##### ヾ(๑╹◡╹)ﾉ" 4、变量储存数据练习

<img src="js基础-day01笔记.assets/变量练习2.gif" alt="变量练习2" style="zoom:80%;" />

写一段 `js` 代码，完成以下需求：

1. 浏览器弹出 `输入弹框`，提示用户：`请输入您的名字`
2. 用户输入完名字之后，用变量 `userName` 储存用户输入的内容
3. 将变量 `userName` 中储存的用户的名字，在网页中输出



##### ヾ(๑╹◡╹)ﾉ" 5、交换变量的值练习

**需求：**

```js
let a = 10
let b = 20
//要求：
console.log(a) // 20
console.log(b) // 10
```

**方法：**

- 使用临时变量、交换两个变量的值  **（记忆）**

  ```js
                    // a   b    temp
  let temp = a     // 10  20    10
         a = b	  // 20   20   10
         b = temp  // 20   10    10
  ```



## var声明变量（拓展）

> 早期 `js` 使用的是 `var` 声明变量，但是 `var` 声明的方式不够严谨，所以在ES新版本里面推荐使用let声明变量
>
> 之后的阶段中，会进一步对比说明 `let` 声明变量的好处 

**特点：**		

1. `var` 可以先使用，再声明（不合理）

   ```js
   // let 声明变量比较严格，必须先声明变量，再使用
   console.log(a) // 报错 Cannot access 'a' before initialization 初始化前无法访问a
   let a = 10
   
   // var 声明变量不够严谨，可以先使用变量，再声明
   console.log(a) // undefined
   var a = 10 
   ```

   

2. `var` 声明过的变量可以重复声明

   ```js
   // let 声明变量比较严格，同一变量只能声明一次
   let a = 10 
   let a = 20 // 报错 Identifier 'a' has already been declared 标识符“a”已声明
   
   // var 声明变量不够严谨，同一变量可以重复声明（不会报错，浏览器会自动忽略多余声明）
   var a = 10
   var a = 20
   console.log(a)
   ```

---

**小结：**

1. `var` 声明变量的形式，有哪些不同的特点？

---



# 数据类型

> 数据可以有多种类型：
>
> - 可以是数字（100，234......）
> - 可以是一个文本（'棠哥' 、'棠哥真帅！'，'小姐姐真漂亮'）
> - .......
>
> 我们为了之后能通过 `JS` 操作不同的数据，需要先学习不同的数据类型

## 数据类型分类

#### 基本数据类型（简单数据类型）

- 数字类型：number
- 字符串类型：string
- 布尔类型：boolean
- undefined：未定义（声明未赋值）
- null：空类型

#### 引用数据类型（复杂数据类型）

> 可以统一看做是对象，但是对象的范围很大，细分成以下情况

- 数组：array
- 函数：function
- 对象：object

---

**小结：**

1. js中基本数据类型有哪些？单词分别是什么？
   - 数字类型：number
   - 字符串类型：string
   - 布尔类型：boolean
   - undefined
   - null
2. js中复杂数据类型有哪些？单词分别是什么？
   - 数组：array
   - 函数：function
   - 对象：object

---



## Number 数字类型

> 所有数字都是数字类型

- 整数：`let num = 10;`

- 小数（浮点数）：`let num = 3.14; `

- 科学计数法

  ```js
  // e 表示10的多少次方
  // 比如： 50000 → 5 * 10000 → 5 * 10^4 → 5e4
  // 当一次数字很大的时候，可以用科学计数法来表示
  let num = 5e4
  console.log(num)
  ```

#### 浮点数精度丢失问题（了解）

> 计算机在计算小数时，有时计算会不准确，开发中尽量避免使用小数直接进行计算

```javascript
// 在进行浮点数运算的时候，可能会出现精度丢失的问题
let num1 = 0.1
let num2 = 0.2
console.log( num1 + num2 ) // 0.30000000000000004
```

---

**小结：**

1. 哪些数据是数字类型？
   - 
2. 在开发时尽量使用小数还是整数进行计算？
   - 

---



## String 字符串类型

> 使用双引号 `"`  或者 `'` 包裹起来的字符都是字符串类型

### 字符串的格式

```js
let str1 = 'abc'
let str2 = '123'
```

### 字符串长度

>  每一个字符串都有一个length属性，表示字符串长度（字符的个数）    

```javascript
let str = "akdjflksjdflk"
console.log(str.length)
```

### 转义字符

**注意点：**

- 单引号不能嵌套单引号
- 双引号不能嵌套双引号
- 单双引号可以互相嵌套

**例子：**

```js
// 1. 如果要打印：好看的'外表'千篇一律
// 2. 如果要打印：有趣的"灵魂"万里挑一
// 3. 如果要打印：好看的'外表'千篇一律，有趣的"灵魂"万里挑一
```



```javascript
// 1、如果要打印：好看的'外表'千篇一律
let str = "好看的'外表'千篇一律"
console.log( str )

// 2、如果要打印：有趣的"灵魂"万里挑一
let str = '有趣的"灵魂"万里挑一'
console.log( str )

// 3、如果要打印：好看的'外表'千篇一律，有趣的"灵魂"万里挑一
let str = "好看的\'外表\'千篇一律，\n有趣的\"灵魂\"万里挑一"
console.log( str )
```

| 代码 |    输出    |
| :--: | :--------: |
| `\'` | **单引号** |
| `\"` | **双引号** |
| `\\` |   反斜杠   |
| `\&` |    和号    |
| `\n` | **换行符** |
| `\r` |   回车符   |
| `\t` |   制表符   |
| `\b` |   退格符   |
| `\f` |   换页符   |

---

**小结：**

1. 通过什么格式判断数据是不是字符串类型？
2. 单引号和双引号的转义字符的写法是什么？

---



### 字符串拼接（拼串）

> **字符串类型** 可以通过 + 进行拼接

**比如：**

```js
let str = 'hello' + 'world'
console.log(str) // helloworld
```

**+号的规则：**

- 如果两边只要有一个是字符串类型，就是拼接的功能
- 如果两边都是数字类型，此时就是加法运算

---

**小结：**

1. 如果 `+` 两边有一个是字符串类型的数据，此时 `+` 是什么功能？
   - 
2. 如果 `+` 两边都是数字类型的数据，此时 `+` 是什么功能？
   - 

---



##### ヾ(๑╹◡╹)ﾉ" 6、字符串拼接测试题

```js
// 1、下列哪一个选项可以打印出：我是棠哥
let nickname = '棠哥'
// A、console.log ('我是' + 'nickname')
// B、console.log ('我是nickname')
// C、console.log ('我是' + nickname)
```



##### ヾ(๑╹◡╹)ﾉ" 7、输入用户信息拼接练习

![输入用户信息练习](js基础-day01笔记.assets/输入用户信息练习.gif)

编写一段 `js` 代码，完成以下需求：

1. 弹出 `输入弹框` ：请输入您的姓名，用变量储存起来
2. 弹出 `输入弹框` ：请输入您的年龄，用变量储存起来
3. 弹出 `输入弹框` ：请输入您的性别，用变量储存起来
4. 最后在页面中输出：`您的姓名是：xxx，您的年龄是：xxx，您的性别是：xxx`



## Boolean 布尔类型

> 布尔类型只有两个值

- true：真、对的、成立
- false：假、错的，不成立

```js
console.log(3 > 2) // true → 表示真/成立
console.log(3 < 2) // false → 表示假/不成立
```

**注意点：**

- 写法上区分大小写：不要写成 `True` 或者是 `False`
- `'true'`  和  `true` 是两个东西，前面带引号的是字符串！

---

**小结：**

1. 布尔类型的数据有几个？

---



## undefined 未定义（声明未赋值）

> 未定义：当一个变量只声明，未赋值，此时变量默认是 `undefined`

```js
let num 
console.log(num) // undefined
```



## null 空类型

> 表示变量已赋值，只不过值为空。之后可能出现在获取页面对dom对象未获取到的情况，`web API` 阶段才会遇到

**null的官方解释：**

- 把null作为尚未创建的对象
- 大白话：将来变量里面存放的是一个对象，但是该对象还没创建好，先用null表示

```js
// 在 web api 阶段会遇到null的情况，先有印象即可
let div = document.getElementById('box') 
console.log(div) 
```

![image-20200912192436771](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/image-20200912192436771.png)



---

**小结：**

1. `undefined` 在什么情况下会出现？
   - 
2. `null` 是什么类型？
   - 

---



## 如何查看数据的类型（了解）

- 最方便的是通过数据的颜色判断
  - Number类型的数据偏向蓝色
  - String类型的数据是黑色
  - Boolean类型的数据偏向紫红色
  - Undefined的数据颜色是灰色
  - Null的数据颜色是灰色 

![数据类型颜色](js%E5%9F%BA%E7%A1%80-day01%E7%AC%94%E8%AE%B0.assets/%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E9%A2%9C%E8%89%B2-1573657157888.png)

- 通过 `typeof 数据` 来查看数据的类型

  ```js
  let num = 20 // number
  let str = 'abc' // string
  let flag = true // boolean
  let un = undefined // undefined
  let nu = null // object
  
  // 可以通过typeof来查看数据的类型
  console.log(typeof num) // number
  console.log(typeof str) // string
  console.log(typeof flag) // boolean
  console.log(typeof un) // undefined
  console.log(typeof nu) // object (特殊情况，记忆即可)
  ```

[null返回object的原因](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)

---

**小结：**

1. 简单数据类型有哪些？单词是？
   - 
2. 复杂数据类型有哪些？单词是？
   - 

---



## 字面量赋值与变量赋值（了解）

- **字面量（直接量）：** 值是固定不变的，**浏览器可以直接识别的量**

  ```js
  // 同学们直接一眼就能看出来是什么类型的数据，一般就是字面量
  console.log(123)
  console.log("字符串")
  console.log(true)
  console.log(undefined)
  console.log(null)
  ```

- **字面量赋值与变量赋值**

  ```js
  // 字面量赋值（直接量赋值）
  let num = 123 // 把字面量赋值给num变量
  
  // 变量赋值 
  let age = num // 通过num这个变量，把num变量的值给age变量
  ```

---

**小结：易错点**

> 打印字符串务必注意：字符串是用引号包裹起来的，没有用引号包裹起来的文本会被当做变量！！！

```js
// 有同学们想在控制台中打印字符串 'abc'
console.log(abc) // 浏览器会把abc当做变量，此时会报错
console.log("abc") // 结果是字符串的 abc
```

---



# 类型转换

## 为什么要进行类型转换?

> 在实际的开发过程中，有时候需要进行不同数据类型之间的转换

```js
// 要求：用户输入年龄，在控制台中打印出用户明年的年龄。(使用弹出输入框输入用户年龄)
 let age = prompt() // 通过prompt获取的数据是一个字符串
 console.log( age + 1 ) // +两边有一个是字符串，所以是字符串的拼接，如果需要实现加法运算，需要把字符串类型转换成数字类型
```



## 转换成数字类型

> 转换成number类型

### 显式转换：

> 自己写代码告诉系统该转成什么类型

- **Number（值）**

  > 把数据整体转换成数字类型

  ```javascript
  let str = '300' // str 是字符串 字符串打印是黑色
  console.log( Number(str) ) // 数字类型打印是蓝色
  ```

- **parseInt（值）**

  > 把数据逐位转换成整数类型——》属于数字类型

  ```js
  let str = '300' 
  console.log( parseInt(str) ) // 300
  // -----------------------------------只能转换出整数部分，从小数点开始不转换
  let str = '3.1415926' 
  console.log( parseInt(str) ) // 3
  ```

- **parseFloat（值）**

  > 把数据转换成浮点数类型——》可以是整数/小数——》属于数字类型

  ```js
  let str = '300' 
  console.log( parseFloat(str) ) // 300
  // -----------------------------------可以转换成小数
  let str = '3.1415926' 
  console.log( parseFloatt(str) ) // 3.1415926
  ```


### 隐式转换：

> 某些运算符被执行时，**系统内部自动**将数据类型进行转换，这种转换称为**隐式转换。**
>
> **算术运算符中的除了`+`以外，其他的运算符：`-` `*` `/` 等都会把数据转换成数字类型**

- **不会改变值的计算**

  ```js
  let str = '600'
  console.log(str - 0)
  console.log(str * 1)
  console.log(str / 1)
  ```

- **正号**

  ```js
  let str = '600'
  console.log(+str)
  ```

---

**小结：**

1. 把数据转换成数字类型的显示转换方法有哪些？

2. 把数据转换成数字类型的隐式转换方法有哪些？

---



##### ヾ(๑╹◡╹)ﾉ" 8、计算两个数和练习

![两个数相加](js基础-day01笔记.assets/两个数相加.gif)

编写一段 `js` 代码，完成以下需求：

1. 弹出两次 `输入弹框`，计算两者的和，输出到页面中 



## 转换成字符串类型

> 转换成字符串，手动加 `""` 即可，但是项目中需要通过js来控制

### 显示转换：

- **String（值）**

  ```js
  let num = 100
  console.log( String(num) ) // 字符串的100
  ```

- **值.toString（）**

  ```js
  let num = 100
  console.log( num.toString() ) // 字符串的100
  ```


### 隐式转换：

> 算术运算符 `+` 有两个功能
>
> - 拼接字符串：当两边只要有一个是字符串时，此时就是拼串
> - 运算功能：当两边都是数字类型时，此时是加法运算

- **拼接字符串**

  ```js
  let num = 100
  console.log(num + 'abc') // 字符串 100abc
  console.log(num + '') // 字符串的 100
  ```

---

**小结：**

1. 转换成字符串类型的显示转换的方法有哪些？
2. 转换成字符串类型的隐式转换的方法有哪些？

---



## 转换成布尔类型（boolean）

> 所有的值都可以转换成布尔类型	

### 显示转换：

- **Boolean（值）**

  ```js
  console.log( Boolean(123) )
  console.log( Boolean('123') )
  ```

**转化布尔类型的规则：**基本数据类型中只有 `0`、 `""`、 `undefined`、`null`、`false`、  `NaN `、这6个值会转换成 `false` ，其他都是`true`。

**以下是易错的几种情况：**

```js
console.log(Boolean(false))
console.log(Boolean("false"))
console.log(Boolean(0))
console.log(Boolean("0"))
```

### 隐式转换：

- !! 非非

  > 取反一次可以转化成布尔值，但是结果不对，所以需要取反两次保证值一样。

  ```js
  console.log(Boolean(3))
  console.log(!3)
  console.log(!!3)
  ```

---

**小结：**

1. 转换成布尔类型的方法有哪些？
2. 有哪些数据转换成布尔类型结果是 `false` ?

---



## NaN（了解）

> `NaN`：`NaN：not a number ` 

在js中，如果把**无法用数字表示的值**转换为数字类型，此时浏览器不会报错，会用 `NaN` 表示。

> 如果代码中出现了 `NaN` ，表示代码中有问题，将不能转换为数字的数据转化为数字了！

```js
let str = 'abc'
console.log( +str ) // NaN
```

**注意点：**

- `NaN` 的类型是 `number` 类型

---

**小结：**

1. 什么情况下会出现 `NaN` 这个值？
2. `NaN` 这个值是什么类型的数据？

---



# 模板字符串

> ''   ""  ``
>
> 模板字符串是ES6中推荐的字符串语法，使用模板字符串可以更加方便的拼接变量

**例子：** 使用 `name` 和 `age` 变量拼接出字符串为：`大家吼，我叫张三，今年18岁`

- 早期用普通字符串拼接：

  > 用 `''` 或者 `""` 表示的字符串，需要通过 `+` 把变量拼接进字符串

  ```js
  let name = '张三'
  let age = 18
  document.write('大家吼，我叫' + name + '，今年' + age + '岁')
  ```

- 现在用模板字符串拼接：

  > 用 ` `` ` 表示的字符串，需要用 `${}` 包裹住变量即可

  ```js
  let name = '张三'
  let age = 18
  document.write(`大家吼，我叫${name}，今年${age}岁`)
  ```



##### ヾ(๑╹◡╹)ﾉ" 9、输入用户信息拼接练习（改成用模板字符串）

![输入用户信息练习](js基础-day01笔记.assets/输入用户信息练习.gif)

编写一段 `js` 代码，完成以下需求：

1. 弹出 `输入弹框` ：请输入您的姓名，用变量储存起来
2. 弹出 `输入弹框` ：请输入您的年龄，用变量储存起来
3. 弹出 `输入弹框` ：请输入您的性别，用变量储存起来
4. 最后在页面中输出：`您的姓名是：xxx，您的年龄是：xxx，您的性别是：xxx`



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 综合案例：用户订单信息案例

![111](js基础-day01笔记.assets/111.gif)

编写一段 `js` 代码，完成以下需求：

1. 弹出 `输入弹框` ：请输入商品名字，用变量储存起来

2. 弹出 `输入弹框` ：请输入商品单价，用变量储存起来

3. 弹出 `输入弹框` ：请输入购买数量，用变量储存起来

4. 弹出 `输入弹框` ：请输入收获地址，用变量储存起来

5. 使用模板字符串，将对应内容改成获取的变量表示，在页面中输出，需要显示的HTML结构如下：

   ```html
   <table>
       <caption>
           <h2>订单确认</h2>
       </caption>
       <tr>
           <th>商品名称</th>
           <th>商品价格</th>
           <th>商品数量</th>
           <th>总价</th>
           <th>收货地址</th>
       </tr>
       <tr>
           <td>x商品</td>
           <td>xxx元</td>
           <td>xxx</td>
           <td>xxx元</td>
           <td>xxx</td>
       </tr>
   </table>
   ```



# 每日学习流程：

1. 参考上课老师的笔记 `md` ，梳理今天上课内容的xmind，可以跟着老师写好的对着写一遍，加深印象
2. 在整理今日学习内容时哪里有点模糊的，可以在每日资料中找到本节视频，快速的看一遍（切记：只看遗漏的，不要全都看一遍）
3. 把上课案例多敲几遍，直到能不看老师代码和视频，只看效果图就能独立敲出来为止（遗忘了也上课有录的视频兜底，你可以的）
4. 剩下的时间做做每日作业和预习第二天内容
5. 到了晚上9:00记得在博学谷填写反馈，网址为（教室局域网访问使）http://ntlias-stu.boxuegu.com/。同学们之间互相提醒，

**备注：**

1. 和之前网页布局阶段不同， `js` 阶段需要记忆的代码不多，更重要的是逻辑思维能力。同学们需要及时调整听课状态，上课重点不在记忆，而在于听懂老师的思路，注意，听懂最关键，上课听懂了，课后练习就是不断巩固思路的过程。

# 每日作业：

## 1、获取用户信息

**要求：**依次弹出 `输入弹框`，收集用户的：姓名、年龄、性别，分别用变量储存，然后分别在控制台输出相关信息

> 其实就是把上课的案例从：`document.write()` 改成了 `console.log()` 

![作业1](js基础-day01笔记.assets/作业1.gif)

## 2、检测题

1. 下列定义的变量名中，不合法的是 ()

   ```js
   A： 2age
   
   B： newClass
   
   C： userName
   
   D： _age
   ```

2. 下面代码运行后打印结果分别是？

   ```js
   let num = 10
   console.log(num + 11) // ???
   console.log(num + '11') // ???
   console.log(num + '') // ???
   ```

3. 请说出基本数据类型有哪些？单词分别是什么？

   ```js
   
   ```

4. 请说出复杂数据类型有哪些？单词分别是什么？

   ```js
   
   ```

5. 下面代码运行后打印结果分别是？

   ```js
   console.log(111 + 222) // ??
   console.log("111" + 222) // ??
   console.log(111 - 222) // ??
   console.log(111 - "222") // ??
   console.log(8 * "9") // ??
   console.log(8 / 8) // ??
   console.log(8 % 2) // ??
   ```





# 常见问题：经验值

## 情况一：

![image-20210904223742260](js基础-day01笔记.assets/image-20210904223742260.png)

![image-20210904223911296](js基础-day01笔记.assets/image-20210904223911296.png)

## 情况二：

![image-20210904224032168](js基础-day01笔记.assets/image-20210904224032168.png)

![image-20210904224046715](js基础-day01笔记.assets/image-20210904224046715.png)

## 情况三：

![image-20210904224122932](js基础-day01笔记.assets/image-20210904224122932.png)

![image-20210904224136849](js基础-day01笔记.assets/image-20210904224136849.png)

