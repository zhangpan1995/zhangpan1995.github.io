# 学习目标

> - [ ] 能够写出页面被卷去头部的代码
>
>   - [ ] 能够说出BOM是什么
>   
>   - [ ] 能够写出2种定时器的使用语法
>
> 
> - [ ] 能够写出5秒钟之后跳转页面的案例
> 
>  - [ ] 能够使用swiper插件完成移动端轮播图的制作
> 
>  - [ ] 能够写出设置、获取、删除本地存储的语法
> 
> 
> 。。。。。。



**理解上课的知识点......**



# 元素的大小和位置

## scroll家族

> 通过scroll系列的相关属性可以用于获取内容区域的宽高、滚去的距离

**使用场景：**我们想要页面滚动一段距离，比如：100px之后，让某个元素显示隐藏，那就需要知道页面滚去了多少距离进行判断处理——》scroll就可以用来检测页面滚动的距离

### 获取宽高

- `scrollWidth` 和 `scrollHeight`：获取元素内容区域的宽高

  > 包含元素的填充（padding），不包含边框（border）

  ```html
  <style>
      div {
          width: 100px;
          height: 100px;
          padding: 10px;
          border: 10px solid #000;
          background-color: pink;
      }
  </style>
  
  <div></div>
  ```

**注意点：**如果盒子内容超出了，此时内容区域大小比盒子实际大小更大！！



### 获取位置

- `scrollLeft` 和 `scrollTop` ：获取元素内容在水平和垂直滚去的距离

<img src="./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/image-20201009195631543.png" alt="image-20201009195631543" style="zoom:80%;" />

**注意点：** 这两个属性是可以修改的



### 检测页面滚动的距离

开发中，我们经常会检测页面滚动的距离，比如：页面滚动了100px，就显示一个元素

```js
// 页面滚动事件
window.addEventListener('scroll',function () {
  // document.documentElement.scrollTop 获取当前页面顶部被卷去的距离
  let num = document.documentElement.scrollTop
  console.log(num)
})
```





##### ヾ(๑╹◡╹)ﾉ" 页面滚动显示返回顶部按钮

**需求：** 当页面滚动500px，就显示返回顶部按钮，否则隐藏，同时点击按钮，可以回到顶部

![111](./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/111.gif)

**步骤：**

1. 找对象——》backtop
2. 给window注册滚动事件
3. 监测html标签的滚去的距离
   1. 如果滚去的距离大于500，此时显示backtop
   2. 如果滚去的距离小于500，此时隐藏backtop
4. 找到a标签，给a标签注册点击事件，点击之后回到顶部



## offset家族

> 通过offset系列的相关属性可以获取元素在页面中的位置

![image-20220118174343751](./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/image-20220118174343751.png)

### 获取宽高

- `offsetWidth` 和 `offsetHeight` ：获取元素的实际大小

  > content+ padding + border三部分组成

  **需求：**通过js获取页面中某个div的宽高

  ```html
  <style>
    div {
      width: 400px;
      height: 400px;
      background-color: pink;
      padding: 20px;
      border: 10px solid #000;
    }
  </style>
  ```

  

**注意点：**offsetWidth和offsetHeight是 **只读属性**，不能修改设置（只能看，不能动）



### 获取最近有定位父元素

- `offsetParent` ：获取最近的有定位的祖先元素

  **需求：**找到sun的offsetParent看看是谁

  ```html
  <style>
      * {
          margin: 0;
          padding: 0;
      }
  
      .father {
          width: 600px;
          height: 600px;
          background-color: pink;
          margin: 0 auto;
          position: relative;
      }
  
      .son {
          width: 400px;
          height: 400px;
          background-color: green;
          margin: 0 auto;
          position: relative;
      }
  
      .sun {
          width: 200px;
          height: 200px;
          background-color: blue;
          margin: 0 auto;
          /* position: absolute;
          right: 0;
          bottom: 0; */
      }
  </style>
  
  <div class="father">
    <div class="son">
      <div class="sun"></div>
    </div>
  </div>
  ```

**注意点：**

- 如果祖先元素中没有定位的元素，最终offsetParent找到的是body
- 如果祖先元素中有定位的元素，最终offsetParent找到的是最近的有定位的祖先元素



### 获取位置

- `offsetLeft` 和 `offsetTop` ：获取元素距离自己最近定位祖先元素（offsetParent）的左上角的距离

**注意点：**offsetLeft和offsetTop同样都是 **只读属性**，不能修改设置（只能看，不能动）



 ![1](./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/11.png)

##### ヾ(๑╹◡╹)ﾉ" 仿京东固定导航栏案例

**需求：** 当页面滚动到秒杀模块，导航栏自动滑入，否则滑出

![666](./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/666.gif)

**步骤：**

1. 找对象——》header和秒杀部分sk
2. 给页面注册滚动事件——》给window注册
3. 滚动的时候实时判断滚去的距离
   1. 如果滚去的距离为大于秒杀部分的offsetTop，则滑入
   2. 如果滚去的距离为小于秒杀部分的offsetTop，则滑出



##### ヾ(๑╹◡╹)ﾉ" 电梯导航案例

**需求：** 点击可以页面跳到指定位置

![333](./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/333.gif)

**步骤：**

1. 找对象——》找到所有的电梯导航items 和 所有显示的neirongs
2. 给所有的电梯导航items注册点击事件
3. 每个item被点击之后
   1. 给当前item添加点击类名 .active
   2. 设置当前网页的scrollTop设置为，当前item对应的neirong的offsetTop



## client家族

> 通过client系列的相关属性可以获取元素可视区域的宽高大小

**使用场景：** 获取元素可视区域的宽度大小

### 获取宽高

- `clientWidth` 和 `clientHeight` ：获取元素可视区域的宽高

  > 包含元素的填充（padding），不包含边框（border）

```html
<style>
  div {
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #000;
    background-color: pink;
  }
</style>

<div>我是内容</div>
```

**注意点：** 和scroll系列不同，scroll系列是包含内容的超出部分，但是client只是当前可视区域



### 获取位置

- `clientLeft` 和 `clientTop`：获取元素左边框和上边框的宽度（没啥用）

 ![client1](./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/client1-1602230074062.png)



#### 实时获取浏览器可视区域的宽度

> 开发中需要实时获取整个浏览器的可视窗口的宽度

- 在窗口尺寸改变的时候触发事件：`resize`

- 检测浏览器窗口宽度：`document.documentElement.clientWidth`

  ```js
  // 浏览器窗口尺寸改变时触发事件
  window.addEventListener('resize',function () {
    //  执行的代码
    // 检测当前浏览器窗口的宽度
    let w = document.documentElement.clientWidth
    console.log(w)
  })
  ```

  

**三大家族的对比：**

 ![client](./webAPIs-day06%E7%AC%94%E8%AE%B0.assets/client-1602230074062.png)

# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 轮播图案例

![444](webAPIs-day06笔记.assets/444.gif)

**需求1：鼠标移入小图片li之后，让当前小图片li高亮，并且让上面对应的大图片li显示**

**步骤：**

1. 找对象：小图片li（indicator下面的li）和大图片li（slides下面的li）
2. 给所有的小图片li注册移入事件
3. 当每一个小图片li被移入之后：
   1. 让当前的小图片li添加active类显示，其他的小图片li去除active类，排他
   2. 让对应的大图片li添加active类显示，其他的大图片li去除active类，排他
   3. 重新设置h3中的文字，加上当前数据的下标 + 1

**需求2：右侧按钮点击之后，让轮播图往下轮播一张**

**步骤：**

1. 找对象：右侧按钮next
2. 给右侧按钮next注册点击事件
3. 点击之后，显示下一张
   1. 需要知道当前是第几张，才能知道下一张显示哪一张，因此需要在全局声明一个全局变量count
   2. 每次点击之后，让count++，然后让此时的count下标对应的小图片li和大图片li设置active，排他
   3. 判断如果当前count已经超出当前小图片li数组的长度，需要手动重置为0，显示第0张

**需求3：bug解决：鼠标先移入小图片切换图片，再点击右箭头，此时会以count显示**

**步骤：**

1. 因为鼠标移入小图片之后，图片虽然改变，但是count的值未改变
2. 此时鼠标点击右箭头之后，会按照count的值显示下一张，如果移入的时候没有同步，此时会按照原始的count来
3. 解决：在鼠标移入的时候，同步更新count的值，这样点击的时候就是新的count了

**需求4：左侧按钮点击之后，让轮播图往上轮播一张**

**步骤：**

1. 找对象：左侧按钮prev
2. 给左侧按钮prev注册点击事件
3. 点击之后，显示下一张
   1. 每次点击之后，让count--，然后让此时的count下标对应的小图片li和大图片li设置active，排他
   2. 判断如果当前count已经小于0，此时需要手动重置为最后一张，即：arr.length-1

**需求5：开启定时器，每隔1s，让轮播图往下切换一张**

**步骤：**

1. 开启定时器
2. 每隔1s往下切换一张图片，相当于每隔1s按一下右侧按钮，即：每隔1s，用js触发右击按钮事件

**需求6：鼠标经过整个轮播图区域，此时清除定时器**

**步骤：**

1. 找对象——》main
2. 给main注册鼠标移入事件
3. 移入main之后，清除上一个定时器

**需求7：鼠标移出整个轮播图区域，此时重新开启定时器**

**步骤：**

1. 找对象——》main
2. 给main注册鼠标移出事件
3. 移出main之后，添加定时器



![image-20220110172413201](webAPIs-day06笔记.assets/image-20220110172413201-16425170080953.png)



# BOM

**BOM（Browser Object Model）：** 浏览器对象模型，提供了一套操作浏览器功能的方法

**说明：**

- BOM的核心是window对象，表示当前浏览器对象

![image-20220119203218710](webAPIs-day06笔记.assets/image-20220119203218710.png)

BOM包含的内容很多，但是很多东西都不太常用，但在BOM中是有一个需要大家掌握的东西，那就是***定时器*** 



## window对象

**window对象是浏览器的顶级对象，也是一个全局对象（可以直接使用）**

> 普天之下莫非王土

- document、alert()、confirm()、prompt()、console.log()...... 所有东西都是window对象上的

- 我们定义在全局作用域中的函数，其实也是加到了window身上
- window非常常用，如果每次都要加很麻烦，所以使用的时候可以省略



## 定时器与延时器（重要）

### 定时器：setInterval

**setInterval定时器：**可以让代码隔一段时间就执行一次，除非被清除，否则一直执行下去

**设置定时器：**

```javascript
// 语法：setInterval(func, time);
//  参数1：需要重复执行的代码函数
//  参数2：每次间隔的毫秒数
//  返回值：当前定时器的id（用于清除）

let timeId = setInterval(function(){
	//重复执行的代码。
}, 1000)
```

**清除定时器：**

```javascript
// 语法：clearInterval(timeId)
//  参数：需要清除的定时器id

clearInterval(timeId) //清除上面定义的定时器
```



### 延时器：setTimeout

**setTimeout延时器：**可以让代码延时一段时间，**只执行一次**

**需求：让一段代码2秒后再执行**

> 如果需要让代码延时执行，可以使用延时器实现

**设置延时器：**

```javascript
// 语法：setTimeOut(func, time);
// 	参数1：需要延时执行的代码函数
// 	参数2：延时多少时间（单位：毫秒）
// 	返回值：当前延时器的id（用于等会清除）

let timeId = setTimeOut(function(){
	// 1秒后将执行的代码。
}, 1000)
```

**清除延时器**

```javascript
// 语法：clearTimeOut(timeId)
//  参数：需要清除的延时器id

//示例：
clearTimeOut(timeId) //清除上面定义的定时器
```



##### ヾ(๑╹◡╹)ﾉ" 5秒之后消失的广告

**需求：5秒钟之后，广告自动消失**

**步骤：**

1. 找对象——》img
2. 设置延时5s的延时器，5s之后执行隐藏img标签的代码



## JS执行机制

**经典面试题：**

```js
console.log(111)
setTimeout(function () {
    console.log(222)
},1000)
console.log(333) 
// 输出的结果是什么？？

// ----------------------------------------------
console.log(111)
setTimeout(function () {
    console.log(222)
},0)
console.log(333) 
// 输出的结果是什么？？
```



### JS是单线程  

**js的特点：** 单线程（同一个时间只能做一件事情）

**影响：** 多个任务需要执行，此时所有任务需要排队，前一个任务结束，才能执行下一个任务。这样会导致：如果 如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

![v2-714dce933a35e596245d92b9e2117d49_1440w](webAPIs-day06笔记.assets/v2-714dce933a35e596245d92b9e2117d49_1440w.jpg)

### 同步和异步

为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程。于是，JS 中出现了同步和异步。

#### 同步

**任务一个一个来**，前一个任务结束，才会执行后一个任务。比如：烧水和做饭，同步的做法是：我们先烧水等水开，10min之后等水开了以后，再去洗菜，再去切菜，再去炒菜

#### 异步

**多个任务同时进行**，做第一件事情同时，还可以做其他事情。比如：烧水做饭，异步的做法是：我们烧水的10min的同时，去洗菜切菜炒菜



#### 异步任务

常见的异步任务有以下三种类型:

1. 注册事件，如 click、resize 等
2. 定时器，包括 setInterval、setTimeout 等
3. ajax（网络模块）

**异步任务：**添加到**任务队列**中（任务队列也称为消息队列）

**同步任务：**会在主线程执行



### JS执行机制（事件循环Event loop）

**流程：**

1. 同步任务由JS的主线程依次执行
2. 异步任务委托给浏览器执行
3. 浏览器会将已完成条件的异步任务代码，加入任务队列等待执行
4. 一旦主线程中的同步任务执行完毕后，系统就会按顺序读取任务队列中的异步任务，让异步任务进入主线程，开始执行。



**思考：**

```js
console.log(1)
document.addEventListener('click', function () {
  console.log(4)
})
console.log(2)
setTimeout(function () {
  console.log(3)
}, 3000)
```



## location对象

**location对象：** 是window对象上的属性，其实对应的就是浏览器中的地址栏。

### 常见属性和方法

- `location.href` ：获取地址栏完整的URL地址，赋值可以用于**跳转**

  ```js
  // 获取地址
  console.log( location.href ) // 拿到地址栏的地址
  
  // 设置跳转——》可以做到点击任意元素都可以跳转
  location.href = "https://www.baidu.com" // 让页面跳转到百度
  ```

- `location.search` ：获取地址栏中携带的参数，即：`?` 后面的部分

- `location.hash` ：获取地址中携带的哈希值，即：符号 `#` 后面的部分

  > 后期vue路由的铺垫，经常用于不刷新页面，显示不同页面，比如：网易云音乐

- `location.reload()` ：重新加载，刷新页面，传入参数true时表示强制刷新



##### ヾ(๑╹◡╹)ﾉ" 5秒之后跳转的页面

**需求：用户点击可以跳转，如果不点击，则5秒之后自动跳转，要求里面有秒数倒计时**

**步骤：**

1. 找对象——》a标签
2. 用变量count储存还剩多少时间
3. 设置定时器，每隔1s
   1. 让count--
   2. 把count渲染到a标签的内容中去
   3. 判断如果count === 0，此时清除定时器，并且通过js直接跳转去a标签的目标链接



## navigator对象（了解）

**navigator对象：**是window上的属性，该对象上记录了浏览器自身的相关信息

```javascript
// navigator.userAgent：浏览器版本

// 检测 userAgent（浏览器信息）
!(function () {
  const userAgent = navigator.userAgent
  // 验证是否为Android或iPhone
  const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
  const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
  // 如果是Android或iPhone，则跳转至移动站点
  if (android || iphone) {
    location.href = 'http://m.itcast.cn'
  }
})()
```



## history对象（了解）

**history对象：** 是window上的属性，表示页面的历史，可以通过history对象的属性完成：前进、后退等效果。

**功能：**

```javascript
// 页面前进
history.forward()
// 页面后退
history.back()

// ------------------------------------------
history.go(1)// 前进一页，相当于：history.forward()
history.go(0)// 刷新当前页，相当于：location.reload()
history.go(-1)// 后退一页，相当于：history.back()
```



# swiper插件

> 实际开发的时候可以选择使用轮播图插件完成轮播图。会更加方便和快捷，并且功能也很强大，还兼容移动端。

- [swiper官网](https://www.swiper.com.cn/)
- [swiper在线演示](https://www.swiper.com.cn/demo/index.html
  )
- [swiper基本使用流程](https://www.swiper.com.cn/usage/index.html)
- [swiper的API，配置自己的插件](https://www.swiper.com.cn/api/index.html
  )

**使用流程：**

- 在官网下载

- 按照官网的教程使用

  - 引入：css、js

  - 设置基本html结构

    ```html
    <div class="swiper">
      <div class="swiper-wrapper">
          <div class="swiper-slide"><img src="./images/b_01.jpg" alt=""></div>
          <div class="swiper-slide"><img src="./images/b_02.jpg" alt=""></div>
          <div class="swiper-slide"><img src="./images/b_03.jpg" alt=""></div>
          <div class="swiper-slide"><img src="./images/b_04.jpg" alt=""></div>
          <div class="swiper-slide"><img src="./images/b_05.jpg" alt=""></div>
          <div class="swiper-slide"><img src="./images/b_06.jpg" alt=""></div>
      </div>
      <!-- 如果需要分页器 -->
      <div class="swiper-pagination"></div>
    
      <!-- 如果需要导航按钮 -->
      <div class="swiper-button-prev"></div>
      <div class="swiper-button-next"></div>
    </div>
    ```

  - 设置js初始化

    ```js
    let mySwiper = new Swiper ('.swiper', {
        direction: 'vertical', // 垂直切换选项
        loop: true, // 循环模式选项
    
        // 如果需要分页器
        pagination: {
            el: '.swiper-pagination',
        },
    
        // 如果需要前进后退按钮
        navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev',
        },
    
        // 如果需要滚动条
        scrollbar: {
            el: '.swiper-scrollbar',
        },
    })       
    ```

- 按照API文档介绍常用属性

  ```js
  // 两个参数：
  // 第一个参数：整个轮播图容器的类选择器
  // 第二个参数：轮播图的配置项
  let mySwiper = new Swiper('.swiper', {
    direction: 'horizontal', // 垂直切换选项 默认水平horizontal
    loop: true, // 循环模式选项
    // speed:10000, // 轮播图轮播速度
  
    // autoplay:true,//等同于以下设置
    autoplay: {
      delay: 1000, // 自动切换的时间间隔
      stopOnLastSlide: false, // 如果设置为true，当切换到最后一个slide时停止自动切换。（loop模式下无效）
      disableOnInteraction: true, // 用户操作轮播图之后，是否禁用自动轮播， true表示不会自动轮播
    },
  
    // 设置Slide的切换效果，默认为"slide"（普通位移切换），还可设置为"fade"（淡入）、"cube"（方块）、"coverflow"（3d流）、"flip"（3d翻转）、"cards"(卡片式)、"creative"（创意性）。
    effect:'creative',
  
    // 如果需要分页器
    pagination: {
      el: '.swiper-pagination',
    },
  
    // 如果需要前进后退按钮
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
  
  })
  ```



# 本地储存

> 随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常性在本地存储大量的数据，HTML5规范提出了相关解决方案。

- 数据存储在用户浏览器中
- 设置、读取方便、甚至页面刷新不丢失数据
- 容量较大，sessionStorage和localStorage约 5M 左右

## localStorage的特点

1. 生命周期永久生效，除非手动删除，否则关闭页面也会保留
2. 同一浏览器的多页面之间可以共享
3. 以键值对的形式储存使用

## localStorage的方法

- 储存数据：`localStorage.setItem(key,value)`
- 获取数据：`localStorage.getItem(key)`
- 删除数据：`localStorage.removeItem(key)`

## localStorage储存复杂数据类型的方法

**场景：** 基本数据类型可以直接储存到localStorage中，但是复杂数据类型无法直接储存，需要把复杂数据类型先转换成JSON字符串，在把JSON字符串（就是个字符串）储存到localStorage中

- 把复杂数据类型转换成JSON字符串：`JSON.stringify(复杂数据类型)`

  > 储存数据时，使用本方法

- 把JSON字符串转换回复杂数据类型：`JSON.parse(JSON字符串)`

  > 去除数据时，使用本方法

## sessionStorage的特点（了解）

1. 生命周期为关闭浏览器窗口
2. 在同一个页面下数据可以共享
3. 以键值对的形式存储使用
4. 用法跟localStorage 基本相同



# 重绘和回流（拓展了解）

![image-20220115150421972](webAPIs-day06笔记.assets/image-20220115150421972.png)

**渲染步骤：**

1. 解析（Parser）HTML，生成DOM树(DOM Tree)
2. 同时解析（Parser） CSS，生成样式规则 (Style Rules)
3. 根据DOM树和样式规则，生成渲染树(Render Tree)
4. 进行布局 Layout（回流/重排）：根据生成的渲染树，得到节点的几何信息（位置，大小）
5. 进行绘制 Painting（重绘）：根据计算和获取的信息进行整个页面的绘制
6. Display：展示在页面上

**回流/重排：** 当 **Render Tree** 中部分或者全部元素的**尺寸、结构、布局**等发生改变时，浏览器就会重新渲染部分或全部文档的过程

**重绘：**由于节点（元素）的样式的改变并 **不影响**它在文档流中的**位置**和**文档布局**时（如：color、background-color、outline等）

**注意点：** 重绘不一定会引起回流，而回流一定会引起重绘

**会导致回流/重排的操作：**

- 页面的首次刷新
- 浏览器的窗口大小发生改变
- 元素的大小或位置发生改变
- 改变字体的大小
- 内容的变化（如：图片的大小）
- 激活css伪类 （如：:hover）
- 脚本操作DOM（添加或者删除可见的DOM元素）

**简单理解影响到布局了，就会有回流**

**例子：**

![image-20220115151100044](webAPIs-day06笔记.assets/image-20220115151100044.png)



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 动态创建表格-本地储存版本

**问题：**之前day04中我们写过动态创建表格案例，但是存在一个问题是：如果添加了很多条新数据，但是只要页面刷新或者重新打开，数据不会保持。

**解决：** 把案例中使用的数据使用本地储存，每次添加或者删除，都把数据在本地储存更新，每次渲染，都从本地储存中获取数据，因为本地储存会一直保留，因此页面刷新或者重新打开，数据会保持

**需求：把day04的动态创建表格——》改为本次存储版本**

**功能1：渲染**

**步骤：**

1. 读取本地储存中的数组
   1. 如果本地储存中没有储存数据，此时把默认的数组储存进去
      1. 把默认数组通过 `JSON.stringify(数组)` 转换成 JSON字符串
      2. 把JSON字符串储存到本地储存中去
   2. 如果本地储存中有储存数据，此时则获取本地储存数据
      1. 获取到的数据默认是JSON字符串，需要把JSON字符串通过 `JSON.parse(JSON字符串)` 转换成复杂数据类型
2. 将获取的数组渲染到页面中去
   1. 本地储存中没有数据则渲染默认数组
   2. 本地储存中有数据则渲染获取到的数据
3. 优化：因为每个功能都需要获取本地储存中的数据，因此，可以将读取本地储存的数组的代码，封装成函数

**功能2：添加**

1. 从本地储存获取原数组——》调用封装好的函数
2. 往获取的原数组中添加新数据
3. 把新数组储存到本地储存中去——》需要先数组通过 `JSON.stringify(数组)` 转换成 JSON字符串，再储存
4. 渲染新数组

**功能3：删除**

1. 从本地储存获取原数组——》调用封装好的函数
2. 往获取的原数组中删除这一项
3. 把新数组储存到本地储存中去——》需要先数组通过 `JSON.stringify(数组)` 转换成 JSON字符串，再储存
4. 渲染新数组
