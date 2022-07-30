# jQuery

> 一款伟大的，用原生js封装的，操作DOM的类库：它里面装有大量的方法，基于这些方法我们可以快速的进行DOM操作和项目开发 

![截屏2022-07-29 20.15.32](/Users/ccxs/Documents/笔记/js-笔记/JQuery.assets/截屏2022-07-29 20.15.32.png)

## JQ中的常用方法

### 获取DOM元素

> 操作方法:JQ选择器（根据选择器类型快速获取元素)

~~~javascript
$([selector],[context])
	$('#box')
	$('.box a')
//jQ支持的选择器：传统css3中大部分都支持、还支持一些自己独有的
/*
	:eq(n)获取集合中索引为n的
	:gt(n)大于这个索引的
	:lt(n)小于这个索引的
*/ 

//用JQ选择器获取的元素一般设置是时候用$符合开始
let $box = $('.box')
~~~

> 节点之间的关系

~~~javascript
// 还可以再设置对应的选择器进行二次筛选
let $box = $('.box')
$box.children('a') //获取对应的子元素
$box.find('a') //获取对应的后代元素
$('a').filter('.active') //同级筛选（在所有的A中筛选出具备class='active'样式类的A）
$box.prev();
$box.prev('p') //获取他上一个标签名为p的哥哥
$box.preAll()
$box.next()
$box.nextAll()
$box.siblings()//获取所有的兄弟
$box.index()//获取索引
$box.parent()//获取父元素
$box.parents() //获取祖先元素一直到document
~~~

### DOM增删改查

~~~JavaScript
let str =`<div class="ccxs">
          ......
          </div>`
$('body').append(str)//追加到容器末尾
$('body').html(str)//等价于innerHTML
$('body').html()//不传参是获取BODY中的HTML内容，除了这个办法还有text方法,等价于innerText
$a.insertBefore($b)//把$a放到$b前面($a,$b都是页面中已经存在的元素)
$a.insertAfter($b)//把$a放到$b的后面
$(`<div class="ccxs">
          ......
          </div>`).insertBefore($a)//需要把新增加元素放到$a前面需要把字符串用$()包裹起来,相当于创建了一个元素
$a.appendTo($b) //=>$b.append($a)
$a.prependTo($b) //=>$b.prepend($a) 在$b容器的开头追加$a
$a.clone()//实现元素的克隆
$a.remove()//实现元素的删除
//操作表单元素的内容
$inp.valu()
$inp.val('aaa')
~~~

### 操作自定义属性

~~~JavaScript
$box.attr('data-type')//获取自定义属性的值
$box.atttr('data-type','b')//设置自定义属性值
$box.attr({
  type:1,
  'name':'ccxs'
})//批量设置
$box.removeAttr('data-type')//删除自定义属性
//表单元素操作或者自定义属性一般都使用prop和removeProp
$radio.prop('checked')
$radio.prop('checked',true)
~~~

### 设置css样式

~~~javascript
$box.css('width',200)//css方法是设置或者批量设置样式（原理是设置style行内样式）$box.css({width:200,height:200}),写的值不加单位，方法会自动帮我们加上px
$box.addClass('active')//设置样式类
$box.removeClass('active')//删除样式
$box.hasClass('active')//验证是否存在某个样式类
$box.toggleClass('active')//之前有就删除没有就创建

//获取样式
$box.css('width')//不设置的时候就是获取
$box.offset()//当前元素距离BODY的左偏移和上偏移
$box.width()/$box.height()//获取盒子的宽高
$box.innerWidth/.innerHeight/.outerWidth/.outerHeight()
//=>等价于clientWidth 和offsetWidth
$(document).scrollTop([val])//可以获取或者设置scrollTop对应的信息，对应的方法
~~~

### 除了操作DOM，jQ中还提供了其他有助于项目开发的方法

~~~javascript
//事件处理
//$元素.on([event type],[function])
//$元素.off([event type],[function]) 移除事件绑定
//$元素.bind()  $元素.unbind() $元素.delegate() 事件委托.....
//$元素.click() .mouse() .mouseout ....常用的事件绑定
$box.on('click',function(){})
$box.click(function(){})

//=>动画处理
$box.animate({
  top:100,
  left:200
},1000,'linear',function(){})

//jq中的ajax请求

//常用的工具方法
$.each([数组、类数组、对象],function(index,item){
  //对象的情况index是属性名 item是值
})
$('a').each(function(index,item){})

//$.toArray()转换为数组  $.merge()数组的合并 $makeArry()把类数组转换为数组  $.uniqueSort()去重加排序  $.type数据类型的检查
~~~

