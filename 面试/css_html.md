###  CSS 

 \1. 常见的块级元素和行内块元素，以及它们有何不同 

 \2. 常见选择器 

 \3. px em 和 rem的区别 

 \4. 水平垂直居中的几种方法 

 \5. 盒模型的理解 

 \6. Flex布局 

 \7. 怎么解决浮动中塌陷的问题 

 \8. CSS3新特性 

 \9. [前端]()常见的布局方式 

   

 HTML 

 \1. HTML的语义化标签 

 \2. [前端]()优化的解决方案 

 \3. HTML5新特性 

 \4. 常见的浏览器兼容问题 

   

1、html的语义化标签

 语义是指一个词或者一句话的正确解释，html也有这种具有语义意义的标签，语义化标签本身的存在就包含某种信息

2、[前端]()优化的解决方案 

https://juejin.cn/post/6844903814659571720

3、HTML5新特性

https://juejin.cn/post/6844903829679390728

4、常见浏览器兼容问题

ie9以下不兼容，老版edge不兼容

vue-cli本身带有Babel 

Babel 是一个可以将 **使用ES2015+语法的代码** 编译成 **向后兼容** 的代码的工具。

https://www.jianshu.com/p/a1f237dacf5b

CSS 

 \1. 常见的块级元素和行内块元素，以及它们有何不同 

一般来说，html的元素分为两种，即块级元素和行内元素。

 

**块级元素**：块状元素排斥其他元素与其位于同一行，可以设定元素的宽（width）和高（height），块级元素一般是其他元素的容器，可容纳块级元素和行内元素。

**行内元素**：行内元素不可以设置宽（width）和高（height），但可以与其他行内元素位于同一行，行内元素内一般不可以包含块级元素。行内元素的高度一般由元素内部的字体大小决定，宽度由内容的长度控制。

 

常见块级元素有：h1,h2,h3,h4,h5,h6,p,div,dl,dt,hr,ol,ul,li,form,pre,table,td,th；

常见内联元素有：em,strong,span,button,input,label,code,select,img,textarea

 

两者之间的区别：

区别：
1.块级元素占据一整行，内联元素的宽度是其元素内容的宽度，多个内联元素排列会放在同一行里除非放不下，才会挤到新的一行
2.块级元素可以设置宽度width和高度height，而内联元素设置widht和height是无效的
3.块级元素可以包含块级元素和内联元素，而内联元素只能包含文本
4.块级元素可以设置margin和padding属性，行内元素只有margin-left、margin-right、padding-left、padding-right起作用

 

2、常见选择器

标签选择器：

div{

}

3、类选择器

.name{

}

4、id选择器

#west{

}

5、层级选择器

 ul li a{           color: red;       }     

input[type='submit']

{           background: palevioletred;            width: 200px;        }

3. px em 和 rem的区别 

px：

px像素。相对长度单位，像素px是相对于屏幕分辨率而言

1、ie无法调整px单位字体大小

2、国外大部分网站能调整在于使用em或rem字体单位

3、firefox能调整px和em,rem

Em:

em是相对长度单位。相对于当前对象内文本的字体尺寸。

rem:

'rem'是'css3'新增的一个相对长度单位，它的出现是为了解决em的缺点，em可以说是相对于父级元素的字体大小，当父级元素字体大小改变时，又得重新计算。rem出现就可以解决这样的问题，rem只相对于根目录，即HTML元素。有了rem这个单位，我们只需要调整根元素`html`的`font-size`就能达到所有元素的动态适配了，附上一段常用适配代码：

https://juejin.cn/post/6844904167719305229

4、布局:
居中， 俩列，三列，双飞翼，圣杯，全局，慕课网复习

 \7. 怎么解决浮动中塌陷的问题 

https://www.jianshu.com/p/0721403d4ee5

overflow

both:clear

after:伪类

