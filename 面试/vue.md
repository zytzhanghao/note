[TOC]



##  vuex	

描述：vuex是专门为vue.js应用程序开发的状态管理模式。是vue程序非父子组件通讯手段的一种

核心概念

state

每个应用对象只有一个store

getter

自定义获取state,相当于store的计算属性

mutations

改变store的唯一属性

actions

Action 类似于 mutation，不同在于：

- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。

modules

分组，方便管理数量多的store

## 双向绑定原理

vue.js采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineproperty()来劫持各个属性的setter,getter.在数据变动时发布消息给订阅者

![img](https://upload-images.jianshu.io/upload_images/13292193-46b64b15abed5139.png?imageMogr2/auto-orient/strip|imageView2/2/w/730)



1、实现一个数据监听器Observer，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者

2、实现一个指令解析器Compile，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数

3、实现一个Watcher，作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图

4、mvvm入口函数，整合以上三者



##  组件间传递数据 

- 父子通信：
  父向子传递数据是通过 props，子向父是通过 events（`$emit`）；通过父链 / 子链也可以通信（`$parent` / `$children`）；ref 也可以访问组件实例；provide / inject API；`$attrs/$listeners`
- 兄弟通信：
  Bus；Vuex
- 跨级通信：
  Bus；Vuex；provide / inject API、`$attrs/$listeners`

## vue 优化

源码优化

- v-if 和 v-show选择调用
  - v-show和v-if的区别是：v-if是懒加载，当状态为true时才会加载，并且为false时不会占用布局空间；v-show是无论状态是true或者是false，都会进行渲染，并对布局占据空间对于在项目中，需要频繁调用，不需要权限的显示隐藏，可以选择使用v-show，可以减少系统的切换开销。
- 为item设置唯一key值，
  - 在列表数据进行遍历渲染时，需要为每一项item设置唯一key值，方便vuejs内部机制精准找到该条列表数据。当state更新时，新的状态值和旧的状态值对比，较快地定位到diff。
- 细分vuejs组件
  - 在项目开发过程之中，第一版本把所有的组件的布局写在一个组件中，当数据变更时，由于组件代码比较庞大，vuejs的数据驱动视图更新比较慢，造成渲染比较慢。造成比较差的体验效果。所以把组件细分，比如一个组件，可以把整个组件细分成轮播组件、列表组件、分页组件等。
- 减少watch的数据
  - 当组件某个数据变更后需要对应的state进行变更，就需要对另外的组件进行state进行变更。可以使用watch监听相应的数据变更并绑定事件。当watch的数据比较小，性能消耗不明显。当数据变大，系统会出现卡顿，所以减少watch的数据。其它不同的组件的state双向绑定，可以采用事件中央总线或者vuex进行数据的变更操作。
- 内容类系统的图片资源按需加载
  - 对于内容类系统的图片按需加载，如果出现图片加载比较多，可以先使用v-lazy之类的懒加载库或者绑定鼠标的scroll事件，滚动到可视区域先再对数据进行加载显示，减少系统加载的数据。



## MVVM和MVC 

 Mvvm定义MVVM是Model-View-ViewModel的简写。即模型-视图-视图模型。【模型】指的是后端传递的数据。【视图】指的是所看到的页面。【视图模型】mvvm模式的核心，它是连接view和model的桥梁。它有两个方向：一是将【模型】转化成【视图】，即将后端传递的数据转化成所看到的页面。实现的方式是：数据绑定。二是将【视图】转化成【模型】，即将所看到的页面转化成后端的数据

MVC是Model-View-Controller。即模型-视图-控制器。

## Computed和Watch 

 computed特性

<p>1.是计算值，<br>2.应用：就是简化tempalte里面{{}}计算和处理props或$emit的传值<br>3.具有缓存性，页面重新渲染值不变化,计算属性会立即返回之前的计算结果，而不必再次执行函数</p>

watch特性

<p>1.是观察的动作，<br>2.应用：监听props，$emit或本组件的值执行异步操作<br>3.无缓存性，页面重新渲染时值不变化也会执行</p>

## V-for 和 v-if同时使用的问题

原因：v-for比v-if优先级高，所以使用的话，每次v-for都会执行v-if,造成不必要的计算，影响性能，尤其是当之需要渲染很小一部分的时候。

```
<ul>
 <li v-for="user in users" v-if="user.isActive" :key="user.id">
 {{ user.name }}
 </li>
</ul>
```

如上述情况，即使有100个user中只有一个需要使用v-if，也需要整个循环数组，这在性能上是极大的浪费。

那难道就没有更好的解决办法，回答：当然是有解决方法的；我们可以使用computed

示例：

```vue
<div>
    <div v-for="(user,index) in activeUsers" :key="user.index" >
        {{ user.name }} 
    </div>
</div>
data () {  // 业务逻辑里面定义的数据
    return {
      users,: [{
        name: '111111',
        isShow: true
      }, {
        name: '22222',
        isShow: false
      }]
    }
  }
computed: {
    activeUsers: function () {
        return this.users.filter(function (user) {
            return user.isShow;//返回isShow=true的项，添加到activeUsers数组

        })
    }
```

## 什么时候使用$.nextTick() 

this.$nextTick()将回调延迟到下次dom更新循环之后执行。

比如在created()钩子函数执行的时候dom其实没有任何渲染,因此进行dom操作并没有作用，而在created()里使用this.$nextTick()可以等待dom生成以后再来获取dom对象

## router 原理

1、Hash模式： 
    hash（#）是URL  的锚点，代表的是网页中的一个位置，单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页，也就是说  #是用来指导浏览器动作的，对服务器端完全无用，HTTP请求中也不会不包括#；同时每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；

 2、History模式： 

  HTML5 History API提供了一种功能，能让开发人员在不刷新整个页面的情况下修改站点的URL，就是利用 history.pushState API 来完成 URL 跳转而无须重新加载页面；

通常情况下，我们会选择使用History模式，原因就是Hash模式下URL带着‘#’会显得不美观；但实际上，这样选择一不小心也会出问题；比如：
 但当用户直接在用户栏输入地址并带有参数时： 
 Hash模式：xxx.com/#/id=5 请求地址为 xxx.com,没有问题; 
 History模式: xxx.com/id=5 请求地址为 xxx.com/id=5，如果后端没有对应的路由处理，就会返回404错误；


为解决这一问题，vue-router提供的方法是：

在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。 

给个警告，因为这么做以后，你的服务器就不再返回 404 错误页面，因为对于所有路径都会返回 index.html  文件。为了避免这种情况，你应该在 Vue 应用里面覆盖所有的路由情况，然后在给出一个 404 页面。或者，如果你使用 Node.js  服务器，你可以用服务端路由匹配到来的 URL，并在没有匹配到路由的时候返回 404，以实现回退。

## vue中常用修饰符

**一、v-model修饰符**

1、.lazy：

输入框改变，这个数据就会改变，lazy这个修饰符会在光标离开input框才会更新数据：

![img](https://img2020.cnblogs.com/blog/1472868/202004/1472868-20200422095359145-2129658851.png)

2、.trim：

输入框过滤首尾的空格：

![img](https://img2020.cnblogs.com/blog/1472868/202004/1472868-20200422095421707-831592670.png)

3、.number：

先输入数字就会限制输入只能是数字，先字符串就相当于没有加number，注意，不是输入框不能输入字符串，是这个数据是数字：![img](https://img2020.cnblogs.com/blog/1472868/202004/1472868-20200422095441517-895479507.png)

 

**二、事件修饰符**

4、.stop：

阻止事件冒泡，相当于调用了event.stopPropagation()方法：

 ![img](https://img2020.cnblogs.com/blog/1472868/202004/1472868-20200422095722262-891576888.png)

5、.prevent：

阻止默认行为，相当于调用了event.preventDefault()方法，比如表单的提交、a标签的跳转就是默认事件：

![img](https://img2020.cnblogs.com/blog/1472868/202004/1472868-20200422095520346-1148774494.png)

6、.self：

只有元素本身触发时才触发方法，就是只有点击元素本身才会触发。比如一个div里面有个按钮，div和按钮都有事件，我们点击按钮，div绑定的方法也会触发，如果div的click加上self，只有点击到div的时候才会触发，变相的算是阻止冒泡：

![img](https://img2020.cnblogs.com/blog/1472868/202004/1472868-20200422095746426-1272980881.png)

7、.once：

事件只能用一次，无论点击几次，执行一次之后都不会再执行

![img](https://img2020.cnblogs.com/blog/1472868/202004/1472868-20200422095802227-1462269056.png)

8、.capture：

事件的完整机制是捕获-目标-冒泡，事件触发是目标往外冒泡

9、.sync

对prop进行双向绑定

10、.keyCode：

监听按键的指令，具体可以查看vue的键码对应表

