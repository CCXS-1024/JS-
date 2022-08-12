# ES6

### “...”的作用

- 拓展运算符（多用在结构赋值中）
- 展开运算符（多用在传递实参中）
- 剩余运算符（多用在接受实参中）

~~~javascript
// 结构赋值
let [n,...m] =[12,21,34]
//n:12
// m[22,34]

//参数传递
let ary = [12,21,13,24,10,25]
let min =Math.min(...ary)

//数组克隆
let obj={name:'ccxs',age:22}
let clnoeobj={...obj,sex:'man',age:12}

//接受参数
let fn=(n,...ary)=>{
  //....
  //n:10
  //aty:[21.32]
}
fn(10,21,32)
~~~

### class创建类

~~~javascript
//=>ES6中类的创建
class Fn{
  //等价于之间的构造函数体
  constructor(){
    this.x=100
  }
  //给实例设置私有属性
  y=200
  // 直接写方法就是在原型上的===Fn.prototype.getx...
  getx(){
    console.log(12)
  }
  // 前面设置static的：吧当前Fn当做普通对象的键值对
  static queryx(){}
  
  
}
//也可以在外面单独这样写
Fn.prototype.gexy=function(){}
Fn.z =100

let f = new fn(10)
~~~

**this的深沉次运用**

~~~javascript
function sum() {
   //argument 是类数组原型上没有数组的方法，只要让forEach中的this指向arguments，就相当于把arguments转换成一个新数组
  [].forEach.call(arguments, (item) => {
     console.log(item)
   })
 
 /* Array.from(arguments).forEach(item=>{
    console.log(item)
  });
  */
}
let ary= [10,21,11,2]
sum(...ary)
~~~

Flat()这个方法可以解决数组的扁平化

- startsWith() / endsWhith()  
- repeat()
