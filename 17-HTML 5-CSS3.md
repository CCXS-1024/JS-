# HTML 5

> HTML :超文本标记语言
>
> XHTML: 更严谨的超文本标记语言

###  新增加的语义化标签

- 块级标签
  - header  头部
  - main
  - footer
  - acrticle 文章
  - nav 
  - figure 配图
  - figcaption  配图说明
  - aside 侧边栏
  - section 普通区域
- 块级标签
  - mark 文本标签
  - time 时期标记

.....

### 新增加的表达元素

> input: search/email/tel/number/date/time/color/range..
>
> 1. 功能强大
> 2. 在移动端能调出对应的键盘
> 3. 内置表单验证的格式
> 4. 新真加  checkvaliditity方法来判断验证

## CSS3

> - @font-face
> - CSS3选择器
> - 背景的处理
>   - 渐变颜色背景
>   - 背景图片的处理
>   - 滤镜功能
> - 变形和动画
> - 盒子模型
> - 媒体响应式开发

### 响应式布局

> 让H5页面适配不同的设备
>
> 1. pc端（一般用于大型项目，大型项目都是pc和页面两套）不需要做响应式布局开发，都是固定宽高布局（100%还原设计搞）
>
> 2. 移动端产品（不需要pc处理访问）
>
>    1. webApp：把开发好的H%页面放到手机浏览器、微信、自己公司的App运行“Hybrid混合App开发”
>    2. 小程序
>    3. App
>
>    => 需要做响应式布局开发，但是只需要适配移动端即可
>
> 3. pc端和移动端用同一套项目

#### 响应式布局开发

> 基础：我们把HTML5页面放到手机上预览，默认情况下，不管手机又多宽，HTML都是按照980（1024）渲染，这样页面会整体缩小（内容也会缩小）
>
> 解决方法：viewport视口（layout viewport 布局视口），设定页面渲染中的一些规则
> 					width=device-width:让当前页面渲染的宽度和设备宽度保持一致
>
> ​					initial-scale=1.0：初始缩放比例1：1
>
> ​					maximum-scale=1.0：最大缩放比例1:1
>
> ​					minmum-scale=1.0：最小缩放比例1:1
>
> ​					user-scalable=no：禁止用户用手缩放



1. css中设置条件就是基于@meida完成的
   		媒体设备 all/print/screen
      媒体条件：不同的条件写不同的样式
   Max-width min-width width

   ~~~css
   @media screen ann (max-width 500px){
     .box{
       	width:200px;
     }
   }
   ~~~
2. DPI适配：屏幕像素比


![截屏2022-08-12 13.46.04](/Users/ccxs/Documents/笔记/js-笔记/17-HTML 5-CSS3.assets/截屏2022-08-12 13.46.04.png)

#### 

