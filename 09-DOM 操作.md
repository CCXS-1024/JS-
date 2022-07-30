# Js中的DOM操作：盒子模型属性

> DOM：document object model文档对象模型，提供的属性和方法，让我们在JS中操作页面中的元素

### JS盒子模型属性

> 基于一些属性和方法，让我们获取当前元素的样式信息，例如：clientWidth、offsetWidth等
>
> - clint
>
>   - width / height
>   - top / left
>
> - offset
>
>   - width / height
>   - top / left
>   - parent
>
> - scroll
>
>   - wodth / height
>   - top / left
>
>   
>
> 方法：window.getComputedStyle([element],[伪类]) / [element].currentStyle

**client**

~~~javascript
let box = document.getElementById('box')

//=>获取盒子可视化区域的宽高（内容宽度+左右padding）
//1.内容溢出与否对他无影响
//2.获取的结果没有单位（其余的盒模型属性也没有）
//3.获取的结果是整数
box.clientWidth
box.clientHeight
//获取页面一屏幕可视化区域的宽高
let WinW = document.documentElement.clientWidth
let WinH = document.documentelement.clientHeight
//JS 实现居中：（一屏幕的宽度-盒子宽度）/2 === Left
//获取左边宽和上边框的大小
box.clientTop
box.clientLeft
~~~

**offset**

~~~javascript
let box =document.getElementById('box')
//在client基础上加border==盒子本身
box.offsetWidth
box.offsetHeight

//offsetParent：获得他的父级参照物（不一定是父元素）
//父级参照物和他的父元素没有必然的联系，父参照物查找：同一个平面中，最外层元素是所有后代元素的父参照物，而基于position:relative/absolute/fixed可以让元素脱离文档流，从而改变元素的父参照物

offsetTop:距离父参照物的上偏移
offsetLeft:距离其父参照物的左偏移（）
~~~

**scroll**

~~~javascript
//在没有内容溢出的情况下，获取结果和client是一样的
//在内容溢出的情况下，获取的结果约等于内容的高度（上/做padding+真实内容的高度/宽度）
// 在不同浏览器获取的结果不尽相同
//不设置overflow属性值对最后的结果也会产生一定的影响
box.scrollWidth
box.scrollHeight

//获取整个页面的真实高度
document.documentElement.scrollHeight||document.body.scrollHeight

//竖向滚动条卷去的高度
//横向滚动条卷去的宽度
//1. 边界值
//min =0
//max = 整个高度scrollHeight - 一屏幕高度clientHeight
box.scrollTop
box.scrollLeft

//13个盒子属性，只有这两个是可读写的属性，七月的都是只读属性
box.scrollTop=0
~~~

**getComputedStyle**

> 获取当前元素所有经过浏览器计算的样式
>
> - 只要元素在页面中呈现出来，那么所有的样式都是经过浏览器计算的
> - 哪怕你没有设置和见过的样式也都计算了
> - 不管你写或者不写，也不论写在什么地方，样式都在这可以直接获取
>
> 在IE6~浏览器中不兼容需要currentStyle来获取

~~~javascript
//第一个参数是操作的元素 第二个参数是伪元素:after/:before
//获取的结果是cssStyleDeclaration这个类的实力，包含了当前元素的所有样式信息
let styleObj = window.getComputedStyle([element],null)
styleObj['backgroundColor']
styleObj.display

//=>IE6~8
styleObj=[element].currentStyle
~~~

####  图片延迟加载