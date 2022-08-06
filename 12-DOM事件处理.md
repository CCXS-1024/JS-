### DOM事件处理

> 事件是元素天生自带的默认操作行为
>
> - 不论我们是否给其绑定了方法，当我们操作的时候，也会把对应的事件触发事件绑定是给元素的某个行为绑定一个方法
> - 目的是当前事件行为触发的时候，可以做一些事情

**常用的事件行为**

- [鼠标事件]
  - click 点击（移动端click被识别为单击）
  - dblclick 双击
  - mousedown 鼠标按下
  - mouseup鼠标抬起
  - mousemove 鼠标移动
  - mouseover  鼠标划过
  - mouseout 鼠标滑出
  - mouseenter 鼠标进入
  - mouseleave鼠标离开
  - mousewhell 鼠标滚动
- [键盘事件]
  - keydown 按下某个键
  - keyup 抬起某个键
  - keypress 除shift / FN/capslock以外的键，其他键按住（连续触发）
- [移动端手指事件]
  - **单手指事件模型 Touch**
    - touchstart 手指按下
    - touchmove 手指移动
    - touchend 手指松开
    - touchcancel 操作取消（一般用于非正常情况下操作结束）
  - 多手指模型 Gesture
    - gesturestart
    - Gesturechange / gestureupdate
    - gestureend
    - gesturecancel
- [表单元素常用事件]
  - foucus 获取焦点
  - blur 失去焦点
  - change 内容改变
- [音视频常用事件]
  - canplay  可以播放（资源没有加载完，播放可能卡顿）
  - canplaythrough 可以播放（资源已经加载完，播放不会卡顿）
  - play 开始播放
  - playing 播放中
  - pause 暂停播放
- [其他常用事件]
  - load 加载完
  - unload 资源卸载
  - beforeunload 当前页面关闭之前
  - error 资源加载失败
  - scroll 滚动时间
  - Readystatechange AJAX请求状态改变事件

### DOM0 和DOM2的区别

> - [DOM0]
>   - Element.on事件行为=function(){}
> - [DOM2]
>   - 元素.addEventListener(事件行为,function(){},true/false)

~~~javascript
// DOM0事件绑定的原理：给当前元素的私有属性赋值，当前事件触发，浏览器会帮我们把赋值的值执行，但是这导致”只能给当前元素某一个事件行为绑定这个方法“
box.onclick = function(){
  console.log('ccxs')
}
box.onclick = function(){
  console.log('zxc')
}// 'zxc'

//DOM2事件绑定的原理：基于原型链查找机制，找到EventTarget.prototype上的方法并且执行，会把当前元素某个事件行为绑定的所有方法，存放到浏览器默认的事件池中（绑定的几个方法，会向事件池存放几个），当事件触发，会把事件池中存储的对应方法，依次按照顺序执行
box.addEventListener('click',function(){
  console.log('ccxs')
},flase)
box.addEventListener('click',function(){
  console.log('zxc')
},flase)
// 'ccxs'
//'zxc'

//DOM2 事件绑定的时候，我们一般都采用实名函数，
//目的：这样可以基于实名函数去移除事件绑定
function fn(){
  console.log('rance')
}
box.addEventListener('click',fn,false)
//基于DOM2向事件池中添加方法，存在去重的机制”同一个元素，同一个事件类型，在事件池中只能存储一遍这个方法，不能重复存储“
~~~

<font color="red">DOM0和DOM2可以混在一起使用：执行的时候依次按照顺序执行输出</font>

~~~~JavaScript
// DOM0能做的事件，DOM2都支持；DOm2里面的一些事件，DOM0不一定支持eg：transitionend、DOMContentLOaded....

window.addEventListener('load',function(){
  // 所有资源都加载完成触发
})
window.addEventListener('DOMContentLoaded',function(){
  // 只要DOM结果加载完就会触发
  // jQ中的$(function(){}) 就是依据这个实现的
})
// jq中所有的事件绑定都是基于 DOM2 绑定的
~~~~

### 事件对象

> 给元素的事件行为绑定方法，当事件行为触发会被执行，不仅执行，而且会把当前操作的相关信息传递给这个函数 => ”事件对象“

![截屏2022-08-03 15.12.05](/Users/ccxs/Documents/笔记/js-笔记/12-DOM事件处理.assets/截屏2022-08-03 15.12.05.png)

**鼠标事件对象**

~~~javascript
box.onclick = function(ev){
  //  鼠标事件对象
  
  //  clientX/clientY:当前鼠标触发点距离窗口做上角x/y轴坐标
  //  pageX/pageY：当前鼠标触发点距离页面左上角x/y轴坐标
  //  type :触发的类型
  //  target：事件原（那个元素触发了 就是那个函数）
  //  preventDefault():用来阻止默认行为的方法，不兼容浏览器
  //  stopPropagation(): 阻止冒泡传播 不兼容的浏览器中也可以只要ev.cancelBubble =true 也可以阻止默认行为
  console.log(ev)
}
// 事件对象和函数以及给谁绑定没有什么必然的关系，它存储的是当前本次操作的相关信息，操作一次只能有一份信息，所有在那个方法中获取的信息都是一样的；第二次操作，存储的信息会把上一次存储的信息给替换掉...
let obj =null
box.addEventListerner('click',function(ev){
  obj =ev
})
box.addEventListerner('click',function(ev){
 	console.log(obj===ev) //true
})
document.body.onclick = function(ev){
  console.log(ev===obj) //true
}
~~~

**阻止a标签的默认行为**

~~~javascript
//1.herf="javascript:;"
//2 a标签是先触发click 事件，然后再去执行href 的跳转
a.onclick = function(){
  return false //这样也可以
}
//3
a.onclick = function(ev){
  ev.preventDefault()
}
~~~

**键盘事件对象**

~~~javascriptD
window.onkeydown = function(){
  // code & key 存储的都是按键，code更仔细
  // keycode & which 存储的都是键盘对应的🐴值
}
~~~

## 事件的传播机制

### 捕获阶段

>  从最外层向最里层事件原依次进行查找（目的：是为冒泡阶段事先计算好传播的层级路径）

### 目标阶段

> 当前元素的相关事件行为触发

### 冒泡传播

> 触发当前元素的某一个行为，不仅他的这个行为被触发了，而且它所有的祖先元素（一直到window）相关的事件行为都会被依次触发（从内到位）

![截屏2022-08-03 19.53.48](/Users/ccxs/Documents/笔记/js-笔记/12-DOM事件处理.assets/截屏2022-08-03 19.53.48.png)

**mouseover 和 mouseenter的区别**

![截屏2022-08-03 20.15.46](/Users/ccxs/Documents/笔记/js-笔记/12-DOM事件处理.assets/截屏2022-08-03 20.15.46.png)

### 事件委托

> 1. 基于事件的冒泡传播机制完成
> 1. 如果一个容器中很多元素都要在触发某一个事件的时候做一些事情，我们只需要给当前容器的这个事件行为绑定方法，这样不论是触发后代中那一个元素的相关事件行为，由于冒泡传播机制，当前容器绑定的方法都要被触发
> 1. 想知道点击谁，只需要基于事件对象中的ev.target事件原获得即可
>
> => 事件委托可以优化性能

###  drag事件

> 可以把一个元素从当前位置拖到指定的容器中
>
> - dragstart 当用户开始拖动一个元素或者一个选择文本的时候 `dragstart` 事件就会触发
> - drag  当元素或者选择的文本被拖动时触发 `drag` 事件 (每几百毫秒).
> - dragend 拖放事件在拖放操作结束时触发 (通过释放鼠标按钮或单击 escape 键)。
> - dragover  拖动元素到指定的目标区域上触发（每几百毫秒触发一次）。
> - Drop  可以把拖动元素放到目标区域中了 ( 事件被抛出)。

~~~javascript
const box = document.querySelector('.box'),
        container = document.querySelector('.container');
      box.ondragstart = function (ev) {
        //DragEvent:拖拽事件对象
        // dataTransfer: setData/getData/clearData 设置的内容最后都会变为字符串  setData(类型标识，对应的值)
        // 类型标识 text/plan text / html text/url-list ..
        ev.dataTransfer.setData('text/plan', box);
      };
      container.ondragover = function (ev) {
        ev.preventDefault();
      };
      container.ondrop = function (ev) {
        ev.preventDefault();
        container.appendChild(box);
      };
~~~

