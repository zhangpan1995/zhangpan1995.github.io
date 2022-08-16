# webAPIs阶段重点问题

## 1、webAPIs的组成是什么？分别表示什么含义/

- DOM：文档对象模型：一套操作页面元素的方法
- BOM：浏览器对象模型：一套操作浏览器的方法

## 2、DOM中的document、node、element分别表示什么？

- document：文档，表示当前网页
- node：节点，表示网页中所有内容都可以称之为节点（标签、文本、注释等）
- element：元素，表示特指网页中的标签节点

## 3、获取DOM对象的方法有哪些？

- **通过css选择获取**
  - 获取单个元素：`document.querySelector('css选择器')`
  - 获取多个元素：`document.querySelectorAll('css选择器')`

- 通过id获取元素：`document.getElementById('id属性值')`
- 通过标签名获取元素：`document.getElementsByTagName('标签名')`
- 通过类名获取：`document.getElementsByClassName("类名")`

## 4、on注册事件的语法是什么？注册好的事件会立刻执行吗？

```js
事件源.on事件名 = function () {
    事件处理程序
}
```

- 注册好的事件不会立刻执行，只有当事件被触发时，才会执行

## 5、常见的事件名有哪些？

- 点击事件：click
- 鼠标经过事件：mouseenter
- 鼠标离开事件：mouseleave
- 获取焦点事件：focus
- 失去焦点事件：blur
- 键盘按下事件：keydown
- 键盘弹起事件：keyup
- 用户输入事件：input

## 6、如何通过js修改元素样式的方法有哪些？

- 通过给DOM对象设置类名的方式添加样式，具体设置dom对象.className
- 通过给DOM对象上的style属性设置，style属性设置的是元素的行内样式

## 7、表单属性中布尔类型的属性有哪些？

- disabled：true表示表单禁用
- checked：true表示单选或者多选的选中
- selected：true表示下拉菜单option被选中

## 8、innerText和innerHTML的区别是什么？

- **innerText属性：**
  - 只能获取文本——》如果有标签会忽略
  - 只能设置文本——》当设置的是标签时，标签不能被解析，标签不能生效
- **innerHTML属性：**
  - 可以获取文本和标签
  - 可以设置文本和标签——》当设置的是标签，标签可以被解析，标签可以生效

## 9、事件处理函数中的this默认指向谁？

- 事件源

## 10、如何阻止a标签的默认跳转？

- 在事件处理函数的最后，写上 `return false`