# DOM以及基础操作

> DOM：document object model 文档对象模型，提供一些属性和方法供我们操作页面中的元素

**获取DOM元素的方法**

- document.getElementById()
- [context].getElementsByTagName() <font color="red">在指定上下文（容器中）</font>，通过标签名获取一组元素集合
- [context].getElementsByClassName()<font color="red">在指定上下文（容器中）</font>,通过样式类名获取一组元素集合
- document.getElementByName() 在整个文档中，通过NAME属性值获取一组节点集合（在IE下只有表单元素的NAME才能识别，说以我们一般只应用于表单元素的处理）
- document.head / document.body / document.documentElement 用于获取页面中的 HEAD/BODY/ HTML

- document.querySelector
- document.querySelectorAll

**JS中的节点和描述之间关系的属性**

> 节点：Node（页面中所有的东西都是节点）
>
> 节点集合：NodeList（getElementsByName / querySelectorAll 获取的都是节点集合）

- 元素节点（元素标签）
  - nodeType ：1
  - nodeName：大写的标签名
  - nodeValue：null
- 文本节点
  - nodeType：3
  - nodeName：'#text'
  - nodeValue: 文本内容
- 注释节点
	- nodeType：8
  - nodeName：'#commen'
  - nodeValue： 注释内容
- 文档节点 document
	- nodeType：9
  - nodeName：'#document'
  - nodeValue: null
- .......

**描述这些节点之间关系的属性**

- childNodes: 获取所有子节点
- Parent :获取父亲节点
- firstChild：获取第一个子节点
- lastChild：获取最后一个子节点
- previousSibling:获取上一个哥哥节点
- nextSibling：获取下一个弟弟节点
- children：获取所有的元素子节点（子元素标签集合）
- firstElementChild  /  lastElementChild：获取第一个和最后一个元素子节点（不兼容IE6~8）
- previousElementSibling / nextElementSibling：获取哥哥和弟弟元素节点（不兼容IE6~8）
- ........

## 在JS中动态增加修改元素

**creatElement()创建元素对象**

**createTextNode()创建文本对象**

**appendChild()把元素添加到容器末尾**

**insertBefore( [新增元素] , [指定元素] )把元素添加到指定容器中指定元素的前面**

~~~JavaScript
let newDiv = document.createElement('div'); //动态创建元素节点
const haha = document.querySelector('.haha');

newDiv.style.width = '200px'
newDiv.style.height = '200px'
newDiv.style.backgroundColor = 'red'

let text = document.createTextNode('游戏人生')//创建文本节点

newDiv.appendChild(text) // 添加文本节点

// document.body.appendChild(newDiv) // 把newDiv 插入到body最后

document.body.insertBefore(newDiv, haha) // 把newDiv 插入到hahah之前

~~~

**cloneNode(true/false) 克隆元素**

**removeChild([element]) 删除元素**

## 自定义属性

**setAttribute()**

- 设置自定义属性：基于setAttribute是吧属性信息写到了元素标签的结构上（在结构中可以看到的），并没有放到元素对象对应的堆内存中

**getAttribute()**

- 基于getAttribute 可以吧结构上存储的自定义属性值获取到

**removeAttribute()**

- 删除自定义属性
