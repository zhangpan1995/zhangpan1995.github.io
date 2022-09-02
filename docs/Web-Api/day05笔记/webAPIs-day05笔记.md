# 学习目标

> - [ ] 能够写出页面加载事件
> 
> 
>- [ ] 能够写出页面滚动事件 
>
> 
> - [ ] 能够利用offset系列获取元素的坐标和大小
>- [ ] 能够写出页面被卷去头部的代码`
>
> 。。。。。。



**理解上课的知识点......**



# 事件委托

> 事件委托：是利用事件流的特征解决一些开发需求的知识技巧

**需求：让每个li标签点击之后，让当前li标签的文字变红**

**优点：** 给父级元素加事件（可以提高性能）

**原理：** 事件委托其实是利用事件冒泡的特点， 给父元素添加事件，子元素可以触发

**实现：** `事件对象.target` 可以获得真正触发事件的元素

```js
// 方法1，找到每一个li标签，给每一个li标签注册点击事件---------------------------------
let lis = document.querySelectorAll('li')
// 给每一个li注册点击事件
for (let i = 0; i < lis.length ; i++) {
    lis[i].addEventListener('click',function () {
        this.style.color = 'red'
    })
}

// 方法2：利用事件委托，只需要找ul，给ul一个标签注册一个点击事件即可----------------------------
let ul = document.querySelector('ul')
ul.addEventListener('click',function (e) {
    e.target.style.color = 'blue'
})
```



# 移除事件的两种方式（了解）

> 除了可以给元素注册事件之外，还可以移除元素身上原有的事件

**需求：给button注册点击事件，然后通过代码移除事件**

## on+事件名=null

> 对于on注册的事件，直接把之前的事件覆盖即可

```js
btn.onclick = null;
```



## removeEventListener('事件名称'，函数名)

> 对于addEventListener注册的事件，需要使用特定的方法移除

```javascript
// 第一个参数：事件的类型
// 第二个参数：要移除的函数名
removeEventListener(type, func);
```

**注意点：**如果想要让你注册的事件之后能够移除，不能使用匿名函数。要声明一个有名字的函数使用。



# 数组常见相关方法

## 数组的增删操作（push、pop、unshift、shift）

```javascript
let arr = ['张三','李四','王五','赵六']

// --------------------在数组的最后，添加一个或多个项，返回添加后数组的length
arr.push()
// -------------------在数组的最后，删除一项，返回删除的项
arr.pop()
// --------------------在数组的最前面，添加一个或多个项，返回添加后数组的length
arr.unshift()
// ---------------------在数组的最前面，删除一项，返回删除的项
arr.shift()
```

##### ヾ(๑╹◡╹)ﾉ" 数组的增删操作练习

```js
//练习1
let arr = ["刘备"]
//添加数据后变成：["赵云","马超","刘备","关羽","张飞"]

//接着删除数据后变成：["关羽","张飞"]

console.log(arr)

//练习2
let arr = ["赵云","马超","刘备","关羽","张飞"]
//把数组的最后一个元素变成数组的第一个元素

//把数组的第一个元素变成数组的最后一个元素

console.log(arr)
```



## 数组的删除、添加、替换：splice

> splice可以在数组的任意位置，添加或者删除任意项，会改变原数组

```js
//------------------splice 方法可以在数组的任意位置，添加或者删除任一项（会改变原数组）
arr.splice(从哪开始删除，删除几个，添加的项1，添加的项2，......)
arr.splice(begin,deleteCount,item1,item2,...)

let arr = ["赵云","马超","刘备","关羽","张飞"]         
           
//删除--------------------从下标为1开始删除，删除两项
arr.splice(1,2) // 删除

//添加--------------------把第一项、第二项添加到下标2的位置
arr.splice(2,0,'第一项','第二项') // 添加

//替换--------------------把下标2这一项替换成新项（先删除，再添加）
arr.splice(2,1,'新项') // 替换
```

##### ヾ(๑╹◡╹)ﾉ" 数组的练习

```js
//练习：
let arr = ["赵云","马超","刘备","关羽","张飞"] 
// 1、在马超后面增加 马腾
// 2、删除关羽
```



# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 渲染学生信息案例

![image-20220116013155475](webAPIs-day05笔记.assets/image-20220116013155475.png)

**说明：** 本次案例使用思路是 **数据操作视图**，是为了之后学习Vue铺垫，并不是直接操作dom（用直接操作dom会更简单，但是目的是为了铺垫就业重要框架Vue），同学们能按照老师思路步骤写出来案例即可，目前感知不深，但后期vue是就是数据操作视图

**逻辑：** 无论是添加还是删除，都是先操作数据数组，然后重新渲染数组数据到页面

**功能1：把数据渲染到页面中去**

1. 找对象——》找到需要操作的tbody
2. 遍历当前的数据数组，每遍历一项，则创建一项tr标签
3. 往tr中通过模板字符串添加内容
4. 把创建好的tr标签添加到tbody中去
5. 需要数组中的数据动态渲染到模板字符串中
6. 防止html结构中原本就存在的tr，可以在最开始渲染之前，先把tbody的内容清空（设置内容为空字符串）
7. 优化：封装函数：因为本案例是数据操作视图，整体逻辑就是：先修改数据数组，然后重新渲染数组，因此会经常用到渲染数组，因此封装函数，可以一次声明多次调用
8. 一打开页面先调用render函数，把数组数据渲染到页面中去

**功能2：点击录入按钮之后，把数据添加到数组中，然后把数组中数据渲染到页面中去**

1. 找对象——》找到录入按钮、5个表单标签
2. 给录入按钮注册点击事件
3. 点击之后，获取5个表单标签的数据，组装成数据数组中每一项的对象格式
4. 注意点：用户并没有输入学号，学号的做法是获取到数据数组的最后一项的stuId，然后+1设置的
5. 把组装好的对象格式，push添加到数据数组中去
6. 把添加之后的数据数组重新渲染——》调用渲染函数render即可
7. 添加渲染完数据之后，记得把5个表单标签重新回复成默认值

**功能3：如果点击的录入的时候，三个输入框中有一个没输入数据，则弹框请输入数据，并且不录入**

1. 录入按钮的点击事件一开始，就判断三个输入框是否有一个没输入
2. 如果有一个没输入，则弹框提示，清空三个输入框，结束当前事件处理函数



**功能4：点击删除a标签之后，把数据数组中对应的数据删除掉，然后重新渲染数据数组**

1. 直接找a标签会找很多，而且还需要等a标签创建出来之后，才能注册事件麻烦，此时我们会使用事件委托优化代码——》给一个父元素注册点击事件，利用事件冒泡，判断如果是a标签，则清除对应的数据数组再渲染
2. 找对象——》找到父元素tbody
3. 给tbody注册点击事件
4. 点击的时候，判断触发事件的标签是不是a标签 e.target.tagName
5. 如果触发事件的是标签就是a标签，则通过a标签身上的id属性（把当前渲染数据数组下标储存到a标签身上，这样可以直接知道当前是第几个li中的a标签）
6. 通过数组删除方法arr.splice()方法删除对应的数组中的数据
7. 使用渲染函数render() 重新渲染数据



# 滚动事件和加载事件

## 滚动事件scroll

**滚动事件：** 当页面进行滚动时触发的事件

**场景：**很多网页需要检测用户把页面滚动到某个区域后做一些处理， 比如：固定导航栏、返回顶部

**事件名：** `scroll`

**监听整个页面滚动：**

```js
// 监听整个页面滚动——》给window或者document注册scroll事件
window.addEventListener('scroll', function () {
  //  页面滚动时需要执行的代码
  console.log('页面被滚动了')
})
```

**注意点：**监听某个元素的内部滚动直接给某个元素加即可



## 加载事件load

**加载事件：** 加载外部资源（如：图片、外联样式、外联js等等）加载完毕时触发的事件

**场景：**

1. 有些代码需要等页面资源全都加载完再执行功能
2. 如果script标签写在body内容上面，无法直接找到dom元素

**事件名：** `load`

**监听页面所有资源加载完毕：**

```js
// 监听页面所有资源加载完毕——》给window注册load事件
window.addEventListener('load',function () {
  //  页面所有资源加载完毕后的代码
  console.log('页面所有资源加载完毕')
})
```



## 加载事件DOMContentLoaded

**场景：**当初始HTML文档被完全加载和解析完成之后，DOMContentLoaded事件被触发，而无需等待：图片、外部样式表等资源完全加载

**事件名：** `DOMContentLoaded`

**监听页面DOM加载完毕：**

```js
// 监听页面DOM加载完毕，其他外部资源另说
window.addEventListener('DOMContentLoaded',function () {
  //  页面DOM加载完毕后的代码，但是
  console.log('页面DOM加载完毕啦')
})
```



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

<img src="webAPIs-day05笔记.assets/image-20201009195631543.png" alt="image-20201009195631543" style="zoom:80%;" />

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

![111](webAPIs-day05笔记.assets/111.gif)

**步骤：**

1. 找对象——》backtop
2. 给window注册滚动事件
3. 监测html标签的滚去的距离
   1. 如果滚去的距离大于500，此时显示backtop
   2. 如果滚去的距离小于500，此时隐藏backtop
4. 找到a标签，给a标签注册点击事件，点击之后回到顶部



## offset家族

> 通过offset系列的相关属性可以获取元素在页面中的位置

![image-20220118174343751](webAPIs-day05笔记.assets/image-20220118174343751.png)

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



 ![1](webAPIs-day05笔记.assets/11.png)

##### ヾ(๑╹◡╹)ﾉ" 仿京东固定导航栏案例

**需求：** 当页面滚动到秒杀模块，导航栏自动滑入，否则滑出

![666](webAPIs-day05笔记.assets/666.gif)

**步骤：**

1. 找对象——》header和秒杀部分sk
2. 给页面注册滚动事件——》给window注册
3. 滚动的时候实时判断滚去的距离
   1. 如果滚去的距离为大于秒杀部分的offsetTop，则滑入
   2. 如果滚去的距离为小于秒杀部分的offsetTop，则滑出



##### ヾ(๑╹◡╹)ﾉ" 电梯导航案例

**需求：** 点击可以页面跳到指定位置

![333](webAPIs-day05笔记.assets/333.gif)

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

 ![client1](webAPIs-day05笔记.assets/client1-1602230074062.png)



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

 ![client](webAPIs-day05笔记.assets/client-1602230074062.png)

# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 轮播图案例

![444](webAPIs-day05笔记.assets/444.gif)

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



![image-20220110172413201](webAPIs-day05笔记.assets/image-20220110172413201-16425170080953.png)



# 重绘和回流（拓展了解）

![image-20220115150421972](webAPIs-day05笔记.assets/image-20220115150421972.png)

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

![image-20220115151100044](webAPIs-day05笔记.assets/image-20220115151100044.png)

