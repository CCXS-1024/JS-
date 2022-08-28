## AJAX

> Async  javascript and xml：异步的JS和XML

~~~javascript
//1. 创建AJAX实例
const xhr = new XMLHttpRequest
let result=null
//2 打开URL（配置发送请求的信息）
xhr.open('GET','www.xxxxx.com/json',true) // 第三个参数开启异步
//3 监听AJAX状态码，在状态为x的时候，获取服务器响应的内容
//ajax状态码：0 1 2 3 4
xhr.onreadystatechange = function(){
  	if(xhr.readState===4 && /^(2|3)\d{2}$/.test(xhr.status)){
      result = xhr.responseText
    }
}
//4 发送请求
// SEND 中放的是请求主体的内容
xhr.send(null)

//=> AJAX任务（发送一个请求给服务器，从服务器获取对应的内容）从SEND后开始，到xhr.readstate===4的时候才结束
~~~

### HTTP的请求方式

> GET系列请求
>
> - GET
> - delete 一般用于告诉服务器，从服务器上删除点东西
> - head 只想获取响应头部的内容，告诉服务器不需要响应主体
> - options 试探性请求，发个请求给服务器，看看服务器能不能接受到，能不能返回
>
> POST系列请
>
> - POST
> - PUT 一般想让服务器把我们传递的信息存储到服务器上（一般用于大型的数据内容）

GET系列一般用于从服务器端获取信息，POST系列一般用给服务器端推送信息，但不论是GET和POST都可以把信息传递给服务器，也能从服务器获取得到结果，只不过是谁多谁少的问题

- GET：给的少，拿的多
- POST：给的多，拿的少

**客户端把信息传递给服务器**

- 问号传参  xhr.open('GET','www.xxxx.com/data?name=xxx&age=12')
- 设置请求头   xhr.setRequestHeader([key],[value])
- 设置请求主体 xhr.send(请求主体信息)

**服务器吧信息给客户端**

- 通过响应头
- 响应主体 （大部分信息都是基于响应主体返回的）

#### GET系列和POST系列的区别

> GET系列传递给服务器信息的方式一般采用：问号传参
>
> POST系列传递给服务器信息的方式一般采用：设置请求主体

1. GET传递给服务器的内容比POST少，因为URL有最长大小限制（IE浏览器一般限制在2kb，谷歌浏览器一般在4~kb，超过的部分自动被浏览器截取了）

~~~JavaScript
xhr.send('请求体')//请求体内容没有大小限制but为了传输效率我们要自己限制一下大小
~~~



1. GET会产生缓存（缓存不是自己可控制的）：因为请求的地址（尤其是问号传递的信息一样），浏览器有时会认为你要和上次请求的数据一样，拿的是上一次信息；所以真实项目中，如果有一个地址GET请求多次，我们可以在后面加一个随机数去缓存

~~~JavaScript
xhr.open('GET','/list?name=xxx&_='+Math.random())
~~~

3. GET相比比较POST来说不太安全：GET是基于问号传参给服务器的，有一种技术叫URL拦截，这样别人可以获取或者篡改传递的信息；而POST基于请求主体传递信息不容易被截取

### AJAX的状态码

- unsend 0:没有发生（创建一个XHR，初始对象）
- opend 1：已经打开（执行了xhr.open)
- headers_received 2:响应头部的信息已经返回给客户端
- loading 3 ：等待服务器返回响应内容
- done 4 ：响应主体信息已经返回给客户端

#### AJAX常用属性和方法

1. Xhr.response/xhr.responseText/xhr.responseXML
2. Xhr.status/xhr.statusText
3. Xhr.timeout
4. Xhr.withCre