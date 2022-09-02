# 学习目标

> - [ ] 能够使用swiper插件完成移动端轮播图的制作
> - [ ] 能够写出设置、获取、删除本地存储的语法
> 
> - [ ] 能够设置获取自定义属性
> - [ ] 能够利用classList操作类名
> 
> 。。。。。。



**理解上课的知识点......**



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

![image-20220115150421972](./webAPIs-day07%E7%AC%94%E8%AE%B0.assets/image-20220115150421972.png)

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

![image-20220115151100044](./webAPIs-day07%E7%AC%94%E8%AE%B0.assets/image-20220115151100044.png)



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



# 正则表达式

## 介绍

**正则表达式：** 是用于匹配字符串中字符组合的模式。在JavaScript中，正则表达式也是对象

**使用场景：** 正则通常用于匹配、替换、提取那些符合正则表达式的文本，许多语言都支持正则表达式

- 表单校验中的**校验**规则功能
- 过滤敏感词的**替换**功能
- 字符串中**提取**我们想要的部分

**例如：**现实生活中通过多个条件规则查找人

![image-20220121172832018](webAPIs-day07笔记.assets/image-20220121172832018.png)

在图中中找出【戴帽子和眼镜的男人】

- 戴帽子、戴眼镜、男人都是描述信息，通过这些信息能够在人群中查找到确定的人
- 这种用于查找描述信息的条件规则，对应到计算机中就是所谓的正则表达式



## 语法

### 使用步骤

- 我们需要查找需要找到人应该怎么做？
  1. 定义规则：戴帽子的
  2. 根据规则查找：找到则结果
- 正则的使用步骤一样，分两步：
  1. 定义规则：写正则
  2. 查找：利用正则表表达式查找文本，找到则返回结果

**例子：**

```js
// 需求：查找下面文本中是否包含字符串：'前端'
let str = 'IT培训,前端开发培训,web前端培训,软件测试培训,产品经理培训'
```



### 创建正则语法

`let 变量名 = /表达式/`

- 其中 `/  /` 是正则表达式的字面量
- 比如：`let reg = /前端/`

### 判断是否是有符合规则的字符串

**test()：** 用来查看字符串是否符合正则规则

- 是符合，返回true
- 不符合，返回false

**语法：**`reg.test(被检测的字符串)`

**比如：**

```js
let str = 'IT培训,前端开发培训,web前端培训,软件测试培训,产品经理培训'
let reg = /前端/
let result = reg.test(str)
console.log(result) // true
```



### 检索（查找）符合规则的字符串

**exec()：** 在字符串中搜索匹配的字符串部分

**语法：**`reg.exec(被检测字符串)`

- 如果匹配成功，则返回一个数组
- 如果匹配失败，则返回一个null

**比如：**

```js
let str = 'IT培训,前端开发培训,web前端培训,软件测试培训,产品经理培训'
let reg = /前端/
let result = reg.exec(str)
console.log(result) // 返回的是一个数组
```



## 元字符

**正则表达式的组成：**

- **普通字符：**没有特殊含义，只能匹配和自己相同的字符，如：`/前端/`
- **元字符：**有特殊含义，可以匹配更多规则，如：`/[a-z]/`

**参考文档：**

- MDN：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions
- 正则测试工具：http://tool.oschina.net/regex



**元字符分类：**

1. **边界符：** 表示位置，开头和结尾，必须用什么开头，用什么结尾
2. **量词：** 表示重复次数
3. **字符类：**特定的字符表示特定的匹配规则



### 边界符

> 表示位置，开头和结尾，必须用什么开头，用什么结尾

正则表达式中的边界符（位置符）用来 **提示字符所处的位置**，主要有两个字符

![image-20220121214926045](webAPIs-day07笔记.assets/image-20220121214926045.png)



```js
console.log(/哈/.test('哈'))
console.log(/二哈/.test('二哈'))
console.log(/二哈/.test('很二哈哈'))

// ^ 开头
console.log(/^二哈/.test('很二哈哈'))
console.log(/^二哈/.test('二哈很傻'))
console.log(/^二哈/.test('二哈'))

// $ 结尾
console.log(/二哈$/.test('二哈很傻'))
console.log(/二哈$/.test('二哈二哈'))
console.log(/二哈$/.test('二哈'))

// 注意点：当^和$一起使用时，表示精准匹配，从头到尾都要符合，常用语表单校验
console.log(/^二哈$/.test('二哈很傻'))
console.log(/^二哈$/.test('二哈二哈'))
console.log(/^二哈$/.test('二哈'))
```

**注意点：** 如果 ^ 和 $ 在一起，表示必须是精准匹配



### 量词

> 表示重复次数

量词用来 **设定某个模式出现的次数**

![image-20220121220713346](webAPIs-day07笔记.assets/image-20220121220713346.png)

```js
// 量词：表示重复次数
// *  次数 >= 0 次
// +  次数 >= 1 次
// ?  次数 0次 或者 1次
// {n}  次数 == 1 次
// {n,}  次数 >= n 次
// {n,m}  n <= 次数 <= m

// * 表示重复0次或者更多次 ——》 次数 >= 0 次
console.log(/^哈*$/.test(''))
console.log(/^哈*$/.test('哈'))
console.log(/^哈*$/.test('哈'))

// + 表示重复1次或者更多次 ——》次数 >= 1 次
console.log(/^哈+$/.test(''))
console.log(/^哈+$/.test('哈'))
console.log(/^哈+$/.test('哈哈哈'))

// ？ 表示重复0次或者1次 ——》次数 0次 或者 1次
console.log(/^哈?$/.test(''))
console.log(/^哈?$/.test('哈'))
console.log(/^哈?$/.test('哈哈哈'))

// {n} 重复n次 ——》次数 == 1 次
console.log(/^哈{2}$/.test(''))
console.log(/^哈{2}$/.test('哈'))
console.log(/^哈{2}$/.test('哈哈'))
console.log(/^哈{2}$/.test('哈哈哈'))

// {n,} 表示n次或更多次 ——》次数 >= n 次 
console.log(/^哈{2,}$/.test(''))
console.log(/^哈{2,}$/.test('哈'))
console.log(/^哈{2,}$/.test('哈哈'))
console.log(/^哈{2,}$/.test('哈哈哈'))

// {n,m} 表示重复 n次 到 m 次 ——》n <= 次数 <= m
console.log(/^哈{2,4}$/.test(''))
console.log(/^哈{2,4}$/.test('哈'))
console.log(/^哈{2,4}$/.test('哈哈'))
console.log(/^哈{2,4}$/.test('哈哈哈'))
console.log(/^哈{2,4}$/.test('哈哈哈哈'))
console.log(/^哈{2,4}$/.test('哈哈哈哈哈'))

// 注意点：
// 1、{n,m} 之间是不能有空格的
console.log(/^a{1,3}$/.test('aaa'))

// 2、量词是就近修饰
console.log(/tang{2}/.test('tang'))
console.log(/tang{2}/.test('tangtang'))
console.log(/tang{2}/.test('tangg'))
```

**注意点：** 逗号左右两侧不能出现空格



### 字符类

> 特定的字符表示特定的匹配规则

- [xxx] 只要字符串中有[]其中任何一个字符，就匹配成功
- [] 里面有中划线 - ，表示一个范围 只要字符串的其中一个符合范围，就配合成功
- [] 里面有一个^表示取反 只有字符串中有一个符合范围，就匹配成功
- . 匹配除换行符以外的任何单个字符

```js
// 1、[xxx] 只要字符串中有[]其中任何一个字符，就匹配成功
console.log(/[abc]/.test('andy'))
console.log(/[abc]/.test('baby'))
console.log(/[abc]/.test('cry'))
console.log(/[abc]/.test('die'))

// 2、[] 里面有中划线 - ，表示一个范围 只要字符串的其中一个符合范围，就配合成功
//   [0-9] ：0~9的范围
//   [a-z] ：a~z的范围
//   [A-Z] ：A~Z的范围
//   [0-9a-zA-Z] ：0~9 + a~z + A~Z 的范围
console.log(/[0-9]/.test('123'))
console.log(/[0-9]/.test('b2b'))
console.log(/[a-z]/.test('qaq'))
console.log(/[a-z]/.test('QAQ'))
console.log(/[A-Z]/.test('QAQ'))

// 3、[] 里面有一个^表示取反 只有字符串中有一个符合范围，就匹配成功
//   [abc] ： 除了abc以外的就行
console.log(/[^abc]/.test('abc'))
console.log(/[^abc]/.test('abcd'))
console.log(/[^0]/.test('0'))
console.log(/[^0]/.test('0123'))
console.log(/[^0]/.test('100'))

// 4、. 匹配除换行符以外的任意字符
// 注意点：换行符指的是js字符串中的换行，是\n，不是<br>
console.log(/./.test('abc'))
console.log(/./.test('1231'))
console.log(/./.test('\n'))
```

#### 字符类-预定义类

![image-20220121223741456](webAPIs-day07笔记.assets/image-20220121223741456-16427758627801.png)

```js
// 1、 \d 匹配0-9的任意数字 ——》[0-9]
console.log(/\d/.test('123'))
console.log(/\d/.test('b2b'))
console.log(/\d/.test('abc'))

// 2、 \D 匹配非0-9的任意字符 ——》[^0-9]
console.log(/\D/.test('123'))
console.log(/\D/.test('b2b'))
console.log(/\D/.test('abc'))

// 3、 \w 匹配任意字母、数字、下划线 ——》[a-zA-Z0-9_]
console.log(/\w/.test('123'))
console.log(/\w/.test('b2b'))
console.log(/\w/.test('@#！@#￥@#￥@'))
console.log(/\w/.test('@#！@#￥@1#￥@'))

// 4、 \W 匹配任意非字母、数字、下划线 ——》[^a-zA-Z0-9_]
console.log(/\W/.test('123'))
console.log(/\W/.test('b2b'))
console.log(/\W/.test('@#！@#￥@#￥@'))
console.log(/\W/.test('@#！@#￥@1#￥@'))

// 5、 \s 匹配不可见字符，如：空格、换行\n、制表符tab \t 
console.log(/\s/.test('123'))
console.log(/\s/.test('1 23'))
console.log(/\s/.test('b2 b'))
console.log(/\s/.test('   '))
console.log(/\s/.test('\n'))

// 6、 \S 匹配可见字符
console.log(/\S/.test('123'))
console.log(/\S/.test('1 23'))
console.log(/\S/.test('b2 b'))
console.log(/\S/.test('   '))
console.log(/\S/.test('\n'))
```





-------------------------------------

##### ヾ(๑╹◡╹)ﾉ" 用户名验证案例

> 正则表达式已经准备好，直接使用即可

**需求：当失去焦点时，对用户名进行判断，用户名要求用户英文字母、数字、下划线或者短横线组成，并且用户名长度为6~16位**

**步骤：**

1. 找对象——》input
2. 创建正则规则，方便之后判断：**/^[a-zA-Z0-9-_]{6,16}$/**
3. 给input注册失去焦点事件
4. 当失去焦点时，获取input的值，通过正则判断：
   1. 当正则判断通过为true，则给span标签加right类
   2. 当正则判断未通过为false，给span设置wrong类



##### ヾ(๑╹◡╹)ﾉ" 昵称验证中文案例

> 正则表达式已经准备好，直接使用即可

**需求：当输入框失去焦点时，对用户名进行判断，用户名只能是中文**

**步骤：**

1. 找对象——》input
2. 创建正则规则，方便之后判断：**/^[\u4e00-\u9fa5]{2,8}$/**
3. 给input注册change事件
4. 当失去焦点并且内容修改时，触发change事件，通过正则判断：
   1. 当正则判断通过为true，则给span标签加right类
   2. 当正则判断未通过为false，给span设置wrong类

**事件拓展：**

- `change事件` 失去了焦点并且内容改变了，才会触发事件

[常用正则网址](https://www.baidufe.com/fehelper/regexp/index.html)



## 修饰符

**修饰符约束正则执行的某些细节行为，如：是否区分大小写，是支持多行匹配等**

**语法：**`/表达式/修饰符`

- `i` 是单词 `ignore` 的缩写，正则匹配时字母不区分大小写

```js
console.log(/a/i.test('a'))
console.log(/a/i.test('A'))
```

- `g` 是单词 `global` 的缩写，匹配所有满足正则表达式的结果

- 替换字符串中的字符：`str.replace(正则表达式,'需要被替换的文本')`



##### ヾ(๑╹◡╹)ﾉ" 过滤敏感字案例

**需求：需要把用户输入内容中的敏感字替换成**

**步骤：**

1. 找对象——》textarea、button、div
2. 给btn注册点击事件
   1. 点击之后，获取area中的内容，进行replce替换，把所有的 基情 和 激情 都替换成**
   2. 把替换之后的内容，设置给div的内容



# 拓展：标签的自定义属性

## 固有属性和自定义属性

标签上属性可以大致分成两类：

- 固有属性：标签上本来就有的属性：如：title、id、class......

- 自定义属性：标签上本来没有的属性，自己随意添加的属性

**需求：通过js获取标签上的属性**

如果要获取**html标签上**的固有属性（本来就有的属性：title、id、class），可以直接通过dom对象点语法获取和设置

**比如：**

```html
<div title="one">我是一个标签</div>

<script>
  let box = document.querySelector('div')
  console.log(box.title) // one
</script>
```

---

但是如果要获取**html标签上**的自定义属性（本来没有的属性，自己随意添加的），使用点语法就不行了，需要通过特殊的方法获取和设置

**比如：**

```html
<div aa="one" >我是一个标签</div>

<script>
  let box = document.querySelector('div')
  console.log( box.aa ) // undefined
</script>
```



**注意点：**标签的自定义属性在DOM对象中是不存在的，DOM对象中只会储存固有属性

> 如果需要通过DOM对象操作标签上的自定义属性，此时需要通过attribute相关的方法完成



## attribute方法

> attribute系列方法是通用的操作标签属性的方法，不管是固有属性还是自定义属性都可以操作

```js
// 获取标签的属性
box.getAttribute('属性名');
// 设置标签的属性
box.setAttribute('属性名', '属性值');
// 移除标签的属性
box.removeAttribute('属性名');
```

**注意点：attribute方法可以操作标签的自定义属性和固有属性**

## data-自定义属性

**data-自定义属性：**传统的自定义属性没有专门的定义规则，开发者随意命名，不够规范，所以在html5中推出来了专门的 data-自定义属性，在标签上一律以data-开头

**注意点：** 在DOM对象上的data-自定义属性，一律以dataset对象方式获得

![image-20220120002120585](webAPIs-day07笔记.assets/image-20220120002120585.png)

# 综合案例

##### ヾ(๑╹◡╹)ﾉ" 小兔鲜注册页面

![image-20220122002159073](webAPIs-day07笔记.assets/image-20220122002159073.png)

**需求1：点击验证码**

**步骤：**

1. 找对象——》a.code
2. 给code注册点击事件
3. 点击之后：
   1. 声明一个变量count储存还剩多少时间
   2. 先设置code的内容为 `05秒后重新获取`
   3. 开启定时器，每隔1s，count--，并且动态渲染code中的内容 `04秒后重新获取`
   4. 等剩余时间count等于0时，此时清除定时器，变设置code中的内容为 `重新获取`

**需求2：用户名校验**

**步骤：**

1. 找对象——》input[name=username]
2. 给input注册change事件
3. 当input被change时
   1. 获取用户输入的内容
   2. 声明变量reg储存正则规则： **/^[a-zA-Z0-9-_]{6,16}$/**
   3. 用正则判断输入是否符合规则：
      1. 如果符合规则，则把span标签内容的提示消息清空
      2. 如果不符合规则，则把span标签内容设置为 请输入6~16位的用户名

**需求3：把根据正则的设置内容的代码封装成函数**

**步骤：**

1. 用function (){} 把根据正则设置内容的代码包裹起来
2. 把函数中每次使用需要变化的部分，变成函数的参数，由调用时实参传入即可

**需求4：手机号验证**

**步骤：**

1. 找对象——》input[name=phone]
2. 给input注册change事件
   1. 正则：**/^(0|86|17951)?(13[0-9]|15[012356789]|166|17[3678]|18[0-9]|14[57])[0-9]{8}$/**
   2. 信息：'请输入11位手机号'

**需求5：验证码验证**

**步骤：**

1. 找对象——》input[name=code]
2. 给input注册change事件
3. 当input被change时，调用verity事件，直接解决
   1. 正则：**/^\d{6}$/**
   2. 信息：'请输入6位的验证码'

**需求6：密码验证**

**步骤：**

1. 找对象——》input[name=password]
2. 给input注册change事件
3. 当input被change时，调用verity事件，直接解决
   1. 正则：/^[a-zA-Z0-9-_]{6,20}$/
   2. 信息：'请输入正确的密码'

**需求7：再次密码验证**

**步骤：**

1. 找对象——》input[name=confirm]
2. 给input注册change事件
3. 当input被change时，判断两次输入的密码是否相同
   1. 如果相同，则清空span的内容
   2. 如果不相同，则显示 '两次输入的密码不一致'

**需求8：我同意模块**

**步骤：**

1. 找对象——》i.icon-queren
2. 给i注册点击事件
3. 点击之后，给i添加icon-queren2类
4. 优化：如果点一次加icon-queren2，再点一次取消，类名的添加和取消可以使用classList.toggle('类名')

**需求9：提交按钮模块**

**步骤：**

1. 找对象——》button.submit
2. 给button注册点击事件
3. button点击之后
   1. 阻止button按钮的默认提交功能，否则会提交
   2. 对以上所有表单一一判断校验，并且判断是否选中确认协议，需要在verity函数中设置返回正则判断结果
      1. 如果校验有问题，需要提醒信息
      2. 如果以上内容全都通过，此时直接跳转去登录页  login.html
4. 如果用户为勾选同意协议，跳转的代码不执行，判断需要卸载跳转代码的前面


