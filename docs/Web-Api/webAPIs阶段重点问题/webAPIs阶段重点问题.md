# webAPIs阶段重点问题

## day01

### 1、webAPIs的组成是什么？分别表示什么含义？

- DOM：文档对象模型：一套操作页面元素的方法
- BOM：浏览器对象模型：一套操作浏览器的方法

### 2、DOM中的document、node、element分别表示什么？

- document：文档，表示当前网页
- node：节点，表示网页中所有内容都可以称之为节点（标签、文本、注释等）
- element：元素，表示特指网页中的标签节点

### 3、获取DOM对象的方法有哪些？

- **通过css选择获取**
  - 获取单个元素：`document.querySelector('css选择器')`
  - 获取多个元素：`document.querySelectorAll('css选择器')`

- 通过id获取元素：`document.getElementById('id属性值')`
- 通过标签名获取元素：`document.getElementsByTagName('标签名')`
- 通过类名获取：`document.getElementsByClassName("类名")`

### 4、on注册事件的语法是什么？注册好的事件会立刻执行吗？

```js
事件源.on事件名 = function () {
    事件处理程序
}
```

- 注册好的事件不会立刻执行，只有当事件被触发时，才会执行

### 5、常见的事件名有哪些？

- 点击事件：click
- 鼠标经过事件：mouseenter
- 鼠标离开事件：mouseleave
- 获取焦点事件：focus
- 失去焦点事件：blur
- 键盘按下事件：keydown
- 键盘弹起事件：keyup
- 用户输入事件：input

### 6、如何通过js修改元素样式的方法有哪些？

- 通过给DOM对象设置类名的方式添加样式，具体设置dom对象.className
- 通过给DOM对象上的style属性设置，style属性设置的是元素的行内样式

### 7、表单属性中布尔类型的属性有哪些？

- disabled：true表示表单禁用
- checked：true表示单选或者多选的选中
- selected：true表示下拉菜单option被选中

### 8、innerText和innerHTML的区别是什么？

- **innerText属性：**
  - 只能获取文本——》如果有标签会忽略
  - 只能设置文本——》当设置的是标签时，标签不能被解析，标签不能生效
- **innerHTML属性：**
  - 可以获取文本和标签
  - 可以设置文本和标签——》当设置的是标签，标签可以被解析，标签可以生效

### 9、事件处理函数中的this默认指向谁？

- 事件源

### 10、如何阻止a标签的默认跳转？

- 在事件处理函数的最后，写上 `return false`

## day02

练习为主

## day03

### 1、查找所有子元素、第一个子元素、最后一个子元素的节点查找代码是什么？

- 所有子元素：node.children
- 第一个子元素：node.firstElementChild
- 最后一个子元素：node.lastElementChild

### 2、查找上一个兄弟元素、下一个兄弟元素的节点查找的代码是什么？

- 上一个兄弟元素：previousElementSibling
- 下一个兄弟元素：nextElementSibling

### 3、查找父节点的代码是？

- parentNode

### 4、创建节点和添加节点的代码分别是什么？

- 创建节点： `document.createElement('标签名')`
- 添加节点： `parent.appendChild(newChild)` 
  - parent：要添加内容的父节点
  - newChild：需要添加进入的子节点

### 5、插入节点的代码是什么？

-  `parent.insertBefore(newChild,refChild)`
  - parent：要插入元素的父元素
  - newChild：添加的元素
  - refChild：被插入前面的元素

### 6、克隆节点的代码是什么？

-  `node.cloneNode(布尔类型)`
  - false：浅克隆，只克隆当前节点，不包含其中内容节点
  - true：深克隆，克隆当前节点以及其中所有内容节点

### 7、删除节点的代码是什么？

-  `parent.removeChild(child)`
  - parent：要删除元素的父元素
  - child：需要删除的元素

### 8、如何创建当前日期对象？如何获取日期对象中的每个部分？

```js
let now = new Date() // 当前时间

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
```

## day04

### 1、如何获取鼠标在页面中的坐标？不同的坐标有什么区别？

- 通过事件对象获取

  - `clientX/clientY`：获取光标相对于浏览器可视区域左上角的水平和垂直坐标

    > 如果有滚动条，不包括被卷去的距离

  - `pageX/pageY`：获取光标相对于整个网页左上角的水平和垂直坐标（推荐）

    > 如果有滚动条，包括被卷去的距离

  - `offsetX/offsetY`：获取光标相对于当前DOM元素左上角的位置（在border内边界的坐标）

### 2、如何判断用户按下的是不是回车按键？

- 通过事件对象的e.key判断是不是Enter即可
- 通过事件对象的e.keyCode判断是不是13即可

### 3、事件流有哪三个阶段？分别介绍以下

- 事件捕获阶段：当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素**由外而内依次被触发**。这一过程被称为事件捕获。
- 事件目标阶段：当前触发的本体事件触发时
- 事件冒泡阶段：当一个元素的事件被触发时，**同类型事件**将会在该元素的所有祖先元素**由内而外中依次被触发**。这一过程被称为事件冒泡。

### 4、阻止浏览器的默认行为（如：a标签的跳转）有哪些方法？有什么区别？

- `return false;` ：可以阻止浏览器的默认行为，但是之后的代码不会执行，并且无法阻止addEventListener注册事件的方式（不推荐使用）
- `e.preventDefault()` ：可以阻止浏览器的默认行为，并且之后的代码可以执行，并且阻止addEventListener注册事件的方式（推荐使用）
- `<a href="javascript:;">我是一个a标签</a>`

### 5、如何阻止事件冒泡？

- `e.stopPropagation()`

## day05

### 1、如何移除事件？

- on注册事件的方式：`事件源.on事件名 = null`
- addEventListener注册事件的方式：`事件源.removeEventListener(事件类型, 需要移除的处理函数名);`

### 2、分别介绍数组的增删操作（push、pop、unshift、shift）

```js
// --------------------在数组的最后，添加一个或多个项，返回添加后数组的length
arr.push()
// -------------------在数组的最后，删除一项，返回删除的项
arr.pop()
// --------------------在数组的最前面，添加一个或多个项，返回添加后数组的length
arr.unshift()
// ---------------------在数组的最前面，删除一项，返回删除的项
arr.shift()
```

### 3、如果需要监测页面的滚动事件，如何设置？

```js
// 监听整个页面滚动——》给window或者document注册scroll事件
window.addEventListener('scroll', function () {
  //  页面滚动时需要执行的代码
  console.log('页面被滚动了')
})
```

### 4、如果需要监听页面所有资源的加载事件，如何设置？

```js
// 监听页面所有资源加载完毕——》给window注册load事件
window.addEventListener('load',function () {
  //  页面所有资源加载完毕后的代码
  console.log('页面所有资源加载完毕')
})
```

### 5、介绍一下三大家族-scroll家族的相关属性？

- `scrollWidth` 和 `scrollHeight`：获取元素内容区域的宽高

  > 包含元素的填充（padding），不包含边框（border）
  >
  > 如果盒子内容超出了，此时内容区域大小比盒子实际大小更大！！

- `scrollLeft` 和 `scrollTop` ：获取元素内容在水平和垂直滚去的距离

### 6、如何实时监测页面滚去的距离？

```js
// 页面滚动事件
window.addEventListener('scroll',function () {
  // document.documentElement.scrollTop 获取当前页面顶部被卷去的距离
  let num = document.documentElement.scrollTop
  console.log(num)
})
```

### 6、介绍一下三大家族-offset家族的相关属性？

- `offsetWidth` 和 `offsetHeight` ：获取元素的实际大小

  > content+ padding + border三部分组成

- `offsetParent` ：获取最近的有定位的祖先元素

  - 如果祖先元素中没有定位的元素，最终offsetParent找到的是body
  - 如果祖先元素中有定位的元素，最终offsetParent找到的是最近的有定位的祖先元素

- `offsetLeft` 和 `offsetTop` ：获取元素距离自己最近定位祖先元素（offsetParent）的左上角的距离

### 7、介绍以下三大家族-client家族的相关属性

- `clientWidth` 和 `clientHeight` ：获取元素可视区域的宽高
- `clientLeft` 和 `clientTop`：获取元素左边框和上边框的宽度（没啥用）

### 8、如何实时获取浏览器可视区域的宽度

```js
// 浏览器窗口尺寸改变时触发事件
window.addEventListener('resize',function () {
  //  执行的代码
  // 检测当前浏览器窗口的宽度
  let w = document.documentElement.clientWidth
  console.log(w)
})
```

### 9、js中哪些任务是异步任务？

常见的异步任务有以下三种类型:

1. 注册事件，如 click、resize 等
2. 定时器，包括 setInterval、setTimeout 等
3. ajax（网络模块）

### 10、location对象上的常见属性和方法有哪些？

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

### 11、history对象上的常见方法有哪些？

```js
// 页面前进
history.forward()
// 页面后退
history.back()

// ------------------------------------------
history.go(1)// 前进一页，相当于：history.forward()
history.go(0)// 刷新当前页，相当于：location.reload()
history.go(-1)// 后退一页，相当于：history.back()
```

### 12、localStorage的储存、获取、删除数据的方法分别是什么？

- 储存数据：`localStorage.setItem(key,value)`
- 获取数据：`localStorage.getItem(key)`
- 删除数据：`localStorage.removeItem(key)`

### 13、复杂类型和JSON字符串互相转换的代码分别是什么？

- 把复杂数据类型转换成JSON字符串：`JSON.stringify(复杂数据类型)`
- 把JSON字符串转换回复杂数据类型：`JSON.parse(JSON字符串)`

## 前端面试题

### 1、localStorage、sessionStorage和cookie的区别

```js
答: 共同点: 都是可以用来存储数据
	区别: 
	1. 请求不同: 
		cookie 数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递。
				sessionStorage 和 localStorage不会自动把数据发给服务器，仅在本地保存。
	2. 存储大小限制也不同: 
		cookie 数据不能超过4k，同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如会话标识。
		sessionStorage 和 localStorage虽然也有存储大小的限制，但比cookie大得多，sessionStorage约5M、localStorage约5M 。
	3. 数据有效期不同: 
		 sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持； 
		 localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；
		 cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。 
```

### 2、什么是事件代理（事件委托）

```js
1、事件代理（事件委托），是JavaScript中绑定事件的常用技巧。顾名思义，“事件代理”，就是把原本需要绑定的事件委托给父元素，让父元素负责事件监听。事件代理的原理是DOM元素的事件冒泡

事件委托的好处：
减少事件数量，提高性能
```

### 3、什么是事件流

```js
事件流是指从页面接收事件的顺序。也就是说，当一个事件发生时，这个事件的传播过程就是事件流。
事件流一般包含三个阶段：捕获  目标  冒泡
```

### 4、js的运行机制是什么

```
答：js是单线程执行的，页面加载时，会自上而下执行主线程上的同步任务，当主线程代码执行完毕时，才开始执行在任务队列中的异步任务。具体如下  
    1.所有同步任务都在主线程上执行，形成一个执行栈。
    2.主线程之外，还存在一个"任务队列(eventloop队列或者消息队列)"。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
    3.一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。哪些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
    4.主线程不断重复上面的第三步。
```

### 5、异步函数有哪些

```js
JavaScript 中常见的异步函数有：定时器，事件和 ajax 等
```

###6、伪数组有哪些

```js
1、参数 arguments，
2、DOM 对象列表（比如通过 document.getElementsByTags 得到的列表）、childNodes也是伪数组
3、jQuery 对象（比如 $("div")）
```

### 7、真数组和伪数组的区别

```js
伪数组：
1、拥有length属性
2、不具有数组的方法
3、伪数组是一个Object，真数组是Array
4、伪数组的长度不可变，真数组的长度是可变的
```

### 8、伪数组怎么转真数组

```js
1、let newArr = Array.protype.slice.call(伪数组)
2、let newArr = Array.from(伪数组),ES6的新语法
3、let newArr = [...伪数组]，使用扩展运算符,也是ES6的语法
```

### 9、DOM操作常用的API有哪些

```js
1、创建节点
	createElement
	cloneNode
    
2、页面修改
	appendChild
	insertBefore
	removeChild
	replaceChild

3、节点查询
	document.querySelector
	document.querySelectorAll
	document.getElementById
	document.getElementsByTagName

4、节点关系
  父关系型：parentNode
  子关系型：children
  
5、元素属性
	设置：setAttribute
    获取：getAttribute

```

### 10、如何检测浏览器的类型

```js
可以通过检测navigator.userAgent  在通过不通浏览器的不同来检测
```

### 11、JavaScript计时函数

```js
1、setInterval() 周期执行函数。间隔指定的毫秒数不停地执行指定的代码。
  clearInterval() 方法用于停止 setInterval() 方法执行的函数代码。
  
2、setTimeout() 延迟执行函数。延迟执行指定的函数，只能执行一次
  clearTimeout() 方法用于停止执行setTimeout()方法的函数代码。
```

### 12、如何阻止冒泡和默认行为

```js
答: 阻止冒泡和捕获  e.stopPropagation()
    阻止默认行为   e.preventDefault()   return false
    注意：addEventListener注册的事件，在高浏览器版本中，return false将没有效果，必须要用事件对象
```

### 13、原生注册事件的方式有哪些？区别是什么

```js
答: 注册方式
		  1. on + 事件名称
		  2. addEventListener
		区别: 
			1. 使用on注册事件,同一个元素只能注册一个同类型事件,否则会覆盖。
			2. addEventListener可以注册同一事件多次,不会被覆盖。
```

