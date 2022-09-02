# 学习目标

> - [ ] 能够创建和添加节点
> 
> 
>- [ ] 能够删除和复制节点
>
> 
> - [ ] 能够写出简单发布留言案例
> 
>。。。。。。



**理解上课的知识点......**

# 节点操作

## DOM树

> 文档页面中的很多节点之间，其实可以通过树状结构表示——》DOM树

html中所有的内容可以通过树状的结构表示，如：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
  </head>
  <body>

    <div>
      <span>我是span1</span>
      <span>我是span2</span>
    </div>
    <!-- 我是一个注释 -->
    <p>我是一个p标签</p>
    
  </body>
</html>
```

用根据元素之间的关系可以通过树状图表示如下：

> 就类比如元素的族谱图

![dom树](webAPIs-day03笔记.assets/dom树.png)

> 之前查找元素是直接在文档中查找的，但是通过DOM树这样的结构，我们可以拓展找元素的方式，直接通过当前节点可以找到其兄弟节点、父子节点
>
> - 之前：直接在整个页面中查找元素——》好比是在全国范围去找某个人
> - 现在：可以通过节点之间的关系查找元素——》好比是可以通过家族关系，去找到父子、找兄弟等会之类的

---



## 查找节点

> 之后可以通过节点查找的方式找到对应的元素。

### 孩子节点

> 获取元素的用的较多

```html
<ul>
  <li>张三</li>
  <li>李四</li>
  <!-- 我是一个注释 -->
  <li>王五</li>
  <li>赵六</li>
</ul>
```



|                          作用                          |         属性          |
| :----------------------------------------------------: | :-------------------: |
|   获取所有子节点（包括元素节点、注释节点、文本节点）   |      childNodes       |
|           获取**所有子元素**（只有元素节点）           |     **children**      |
|  获取第一个子节点（包括元素节点、注释节点、文本节点）  |      firstChild       |
|          获取**第一个子元素**（只有元素节点）          | **firstElementChild** |
| 获取最后一个子节点（包括元素节点、注释节点、文本节点） |       lastChild       |
|         获取**最后一个子元素**（只有元素节点）         | **lastElementChild**  |

---



### 兄弟节点

> 获取元素的用的较多

```html
<ul>
  <li>张三</li>
  <li class="ls">李四</li>
  <!-- 我是一个注释 -->
  <li>王五</li>
  <li>赵六</li>
</ul>
```

|                          作用                          |            属性            |
| :----------------------------------------------------: | :------------------------: |
| 获取上一个兄弟节点（包括元素节点、注释节点、文本节点） |      previousSibling       |
|         获取**上一个兄弟元素**（只有元素节点）         | **previousElementSibling** |
| 获取下一个兄弟节点（包括元素节点、注释节点、文本节点） |        nextSibling         |
|         获取**下一个兄弟元素**（只有元素节点）         |   **nextElementSibling**   |

---



### 父节点

```html
<ul>
  <li>张三</li>
  <li class="ls">李四</li>
  <!-- 我是一个注释 -->
  <li>王五</li>
  <li>赵六</li>
</ul>
```

|    作用    |    属性    |
| :--------: | :--------: |
| 获取父节点 | parentNode |

> 一般html中都是标签包裹内容，所以一般获取父节点就是父元素

---



##### ヾ(๑╹◡╹)ﾉ"  节点查找的小结

> 重点在于查找元素的那几个

---



##### ヾ(๑╹◡╹)ﾉ" 表单校验效果

> 需要在用户**输入时**判断内容的长度是否满足2~6位之间

![表单校验效果](webAPIs-day03笔记.assets/表单校验效果.gif)

**步骤：**

1. 找到input标签，给input标签注册点击事件
2. 当用户输入的时候，进行判断用户输入是否正确
3. 根据用户输入的结果，通过节点查找设置span的提示文本



---



## 增加节点

> 在很多情况下，我们需要通过js在页面中增加元素
>
> 比如：点击发布按钮之后，在下方新增一条数据

**页面增加节点步骤：**

1. 创建元素节点
2. 页面中追加节点

![2000](webAPIs-day03笔记.assets/2000.gif)

### 添加节点appendChild(newChild)

**需求：**点击按钮之后，把div.red添加div.father里面

> 此时需要使用添加节点的方法

```html
<style>
  .father {
    width: 400px;
    height: 400px;
    border: 1px solid #000;
  }

  .red {
    width: 100px;
    height: 100px;
    background-color: red;
  }
</style>

<button>移花接木</button>
<div class="father">
  这是.father的盒子
</div>

<div class="red">
  这是.red的盒子
</div>
```



**语法：** `parent.appendChild(newChild)` 

- parent：要添加内容的父节点
- newChild：需要添加进入的子节点

**作用：**表示把newChild添加到parent内容的**最后**



### 创建节点createElement()

> 在内存中创建一个元素节点，一般配合appendChild()方法一起使用

**需求：** 点击按钮之后，创建一个新的h1标签，添加到div.father里面去

```html
<style>
    .father {
        width: 400px;
        height: 400px;
        border: 1px solid #000;
    }
</style>

<button>点击生成一个h1标签</button>
<div class="father">
    我是div中的内容
</div>
```



**语法：** `document.createElement('标签名')`

**作用：** 在内存中创建一个元素节点

**返回值：**

- 创建好的元素





### 插入节点insertBefore(newChild,refChild)

> 可以将页面中的节点插入到目标节点的前面

**需求：** 点击按钮，在把田七添加到王五前面

```html
<button>点击插队</button>
<ul>
  <li>张三</li>
  <li>李四</li>
  <li class="ww">王五：我预感等会田七会插到我前面</li>
  <li>赵六</li>
</ul>

<li class="tq">田七：我要插队！！</li>
```



**语法：** `parent.insertBefore(newChild,refChild)`

**参数：**

- parent：要插入元素的父元素
- newChild：添加的元素
- refChild：被插入前面的元素

**作用：** 把newChild添加到parent里面的refChild节点的前面

**注意点：** 

- 如果是在父元素内容的最前添加，可以使用 `parent.inserBefore(newChild,firstElementChild);`

- 如果是在父元素内容的最后添加，可以使用appendChild，也可以使用 `parent.insertBefore(newChild,null)`

  >  其实就是appendChild的效果

---

##### ヾ(๑╹◡╹)ﾉ"  动态创建新闻案例

> 现在需要通过js的方式，当点击按钮之后，在div中动态生成相关的列表

<img src="webAPIs-day03笔记.assets/动态创建新闻案例.gif" alt="动态创建新闻案例" style="zoom:80%;" />

**步骤：**

1. 找到button
2. 给button按钮注册点击事件
3. 点击之后
   1. 创建一个ul
   2. 遍历数组，每一项数据创建一个li，
   3. 把数组的每一项数据添加为li的内容
   4. 把每一个创建好的li添加到ul中去
   5. 最后把组合好的ul添加到页面的div中去
4. 在点击事件中判断当前div中是否有ul，如果有ul，此时结束当前事件处理函数（return）



##### ヾ(๑╹◡╹)ﾉ"  学成在线渲染案例

![image-20220115183938680](webAPIs-day03笔记.assets/image-20220115183938680.png)

**需求：** 按照数据渲染页面

**步骤：**

1. 获取需要添加标签的ul标签
2. 根据数组中数据的个数，遍历数组，每次遍历一次就动态创建出一个li标签
3. 在创建好的li标签内部，使用模板字符串添加内容，把数组中的数据添加到内容中
4. 把创建好的li标签添加到ul中去



## 克隆节点：cloneNode()

**需求：**点击按钮之后，复制div.red添加到div.father里面去

> 如果复制的div中有内容呢？

```html
<style>
  .father {
    width: 400px;
    height: 400px;
    border: 1px solid #000;
  }

  .red {
    width: 100px;
    height: 100px;
    background-color: red;
  }
</style>

<button>移花接木</button>
<div class="father">
  这是.father的盒子
</div>

<div class="red">
  这是.red的盒子
</div>
```



**语法：** `node.cloneNode()`

**作用：** 在内存中复制克隆一份node节点

**参数：**

- false：浅克隆，只克隆当前节点，不包含其中内容节点
- true：深克隆，克隆当前节点以及其中所有内容节点



## 删除节点removeChild(child)

**需求：** 点击哪一个li，就删除这个一个li

**语法：** `parent.removeChild(child)`

**参数：**

- parent：要删除元素的父元素
- child：需要删除的元素

**作用：** 通过父节点调用，删除其中的某个子节点



# 日期对象Date

> js提供了一个**Date构造函数**，通过Date构造函数可以创建不同的日期对象
>
> ——》因为日期都是不同的！
>
> Date对象用来处理日期和时间

## 创建日期对象

```javascript
let now = new Date() // 不传参，默认是一个当前时间的对象
let date = new Date("2021-10-14 05:20:00") // (格式固定)指定具体的时间对象，后面的时分秒可以省略
console.log(now)
console.log(date)
```

## 日期对象的常用方法

> 获取日期指定部分的方法，可以用于自定义格式化日期

```javascript
let now = new Date() // 当前时间

console.log(now.toLocaleString()); // 输出本地格式日期

// 获取年份
let year = now.getFullYear()
// 获取月份——》月份从0开始，范围是0~11，一般会+1
let month = now.getMonth() + 1
// 获取日——》一个月的几号——》getDay表示获取星期几（从0开始，0表示周日，1表示周一）
let day = now.getDate()
// 获取时
let hours = now.getHours()
// 获取分
let minutes = now.getMinutes()
// 获取秒
let seconds = now.getSeconds()
let str = `${year}年${month}月${day}日 ${hours}时${minutes}分${seconds}秒`;
document.write(str);
```

##### ヾ(๑╹◡╹)ﾉ" 电子表：能获取当前日期的x年x月x日 x时x分x秒的格式，设置在box中

> 先获取当前的时间，然后设置到box的内容中去

![电子表案例](webAPIs-day03笔记.assets/电子表案例-1603293285931.gif)

```html
<style>
  #box {
    width: 600px;
    height: 200px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
    box-shadow: 12px 12px 18px 3px #ccc;
    text-shadow: 0px 3px 0px #b2a98f, 0px 14px 10px rgba(0,0,0,0.15), 0px 24px 2px rgba(0,0,0,0.1), 0px 34px 30px rgba(0,0,0,0.1);
    line-height: 200px;
    font-size: 40px;
    text-align: center;
  }
</style>

<div id="box"></div>
```



- 获取当前日期对象
- 获取日期对象中的指定部分
- 把日期对象中的指定部分拼接成字符串
- 把拼接的字符串添设置到box中
- 需要隔1s执行一次——》定时器
- 因为定时器中的函数不会立马执行，如果需要让页面一刷新立马有时间——》在定时器前先执行一遍代码



## 时间戳

> 一般日期打印出来，是字符串的形式
>
> **时间戳则是日期的数字形式**，可以运算

**时间戳：**表示距离1970年01月01日00时00分00秒起，过去的总毫秒数

**作用：** 用来计算时间差

**代码：** `let date = +new Date();`

### 计算代码执行的时间

```js
// ------------------------获取开始的时间
let begin = +new Date()
let sum = 0
for (let i = 1; i <= 100000000; i++) {    
    sum += i
}
console.log(sum)
// -------------------------------获取结束的时间
let end = +new Date()
console.log(end - begin) // 计算时间差，可以得出代码的执行时间毫秒数
```

### 距离下课还剩多少时间

```js
// -----------------------------------当前时间
let now = new Date()
// ----------------------------------将来需要倒计时的时间
let future = new Date('2022-01-16 18:30:00')

// ------------------------------得到时间差——》转换成秒数（小数后忽略）
let time = parseInt((future - now) / 1000)

// --------------------------------秒数中获取时——》1小时=3600秒
let hours = parseInt(time / 3600)

// --------秒数中获取分——》1分钟=60秒, 对所有的分钟数, 对60求余数即可(超过60的进位到小时中了）
let minutes = parseInt(time / 60) % 60

// ---------获取秒数，对秒数求60的余数（超过60的部分进位到分钟去了)
let seconds = time % 60;

let str = `距离下课还有: ${hours} 小时 ${minutes} 分钟 ${seconds} 秒`
document.write(str);
```



##### ヾ(๑╹◡╹)ﾉ" 放假倒计时效果

![4000](webAPIs-day03笔记.assets/4000.gif)

**需求：** 计算距离放假还剩多少时间（格式：xx天xx时xx分xx秒），并且每隔1s更新（倒计时）

**步骤：**

1. 找对象——》天、时、分、秒
2. 计算现在距离放假还剩多少时间
3. 把剩余时间转换成xx天xx时xx分xx秒
4. 把对应的部分设置到页面中的去
5. 使用定时器定时执行逻辑代码



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 微博发布案例

![5000](webAPIs-day03笔记.assets/5000.gif)

**需求1：检测用户输入字数**

1. 找对象：textarean和span
2. 给textarea注册input事件
3. 当用户输入的时候，检测当前文字内容的长度，设置给span

**需求2：当用户点击发布按钮之后，新增一条数据**

1. 找对象：发布按钮和ul#list
2. 给发布按钮注册点击事件
3. 点击之后
   1. 将用户输入的数据获取到储存好
   2. 创建li标签
   3. 往li标签中通过模板字符串添加内容，将字符串中需要变化值进行修改（其中头像和名字需要随机从数组中获取，并且渲染）
   4. 把创建好的li标签添加到ul标签中去（评论一般是最新的加到最前面）
   5. 把textarea中的内容和span的内容清空

**需求3：用户输入如果是空，则不能创建新的li，把内容清空，并且弹框警告**

1. 在点击发布的事件处理函数中，判断用户输入的是否为空（需要使用trim，空格也不行）
2. 如果为空，此时需要阻止事件处理函数继续执行 return
3. 并且弹框告知需要输入数据

**需求4：点击x，需要可以把当前的li标签删除**

1. 需要在创建x之后，再注册点击事件
2. 点击之后，把当前的li删除



**拓展补充：**

- **去除字符串首尾空格方法：** `str.trim()`
