## （1）promise 理解

promise 是js解决异步提出的一种方案。

promise有三种状态

pending(进行中)、fulfilled(已完成)和rejected(已失败)

俩个特点：

对象状态不受外界影响

一旦改变，就不会再变，任何时候都可以得到这个结果

## （2）箭头函数和普通函数的区别 

上下文

https://www.cnblogs.com/echolun/p/11438363.html

全局上下文：全局上下文只有一个，一般由浏览器创建，也就是window，我们可以通过this访问，而window是var 全局变量的载体

函数上下文：函数上下文可以有多个，每当函数调用时都会创建一个，（一个相同函数被多次调用，都会创造多个函数上下文）

箭头函数：

 （1）都是匿名函数，不能作为构造函数

（2）this指向其上下文，且不会改变，call(),bind()都不会改变

（3）箭头函数没有原生属性（prototype)

##   (3)ES6新特性 

阮一峰：https://es6.ruanyifeng.com/

## （4） Var let const 的区别 

1、var只有全局作用域和函数作用域，let和const有块的作用域概念

2、const 必须初始化，且不能再更改

3，const 和let 都存在暂时性死区，即先调用后声明，会返referenceError.

(4)实现继承几种方式

https://www.cnblogs.com/humin/p/4556820.html

## （5）类的继承几种方式

| 名称                  | 例子                                                         | 优势                                                         | 缺陷                                                         |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| New-initialization    | ` function foo(){} foo.prototype = {  foo_prop: "foo val" }; function bar(){} var proto = new foo; proto.bar_prop = "bar val"; bar.prototype = proto; var inst = new bar; console.log(inst.foo_prop); console.log(inst.bar_prop);` | 支持目前以及所有可想象到的浏览器(IE5.5都可以使用). 这种方法非常快，非常符合标准，并且充分利用JIST优化。 | 为使用此方法，这个问题中的函数必须要被初始化。 在这个初始化过程中，构造可以存储一个唯一的信息，并强制在每个对象中生成。但是，这个一次性生成的独特信息，可能会带来潜在的问题。另外，构造函数的初始化，可能会给生成对象带来并不想要的方法。 然而，如果你只在自己的代码中使用，你也清楚（或有通过注释等写明）各段代码在做什么，这些在大体上都根本不是问题（事实上，还常常是有益处的）。 |
| Object.create         | ` function foo(){} foo.prototype = {  foo_prop: "foo val" }; function bar(){} var proto = Object.create(  foo.prototype ); proto.bar_prop = "bar val"; bar.prototype = proto; var inst = new bar; console.log(inst.foo_prop); console.log(inst.bar_prop); `` function foo(){} foo.prototype = {  foo_prop: "foo val" }; function bar(){} var proto = Object.create(  foo.prototype,  {    bar_prop: {      value: "bar val"    }  } ); bar.prototype = proto; var inst = new bar; console.log(inst.foo_prop); console.log(inst.bar_prop)` | 支持当前所有非微软版本或者 IE9 以上版本的浏览器。允许一次性地直接设置 `__proto__` 属性，以便浏览器能更好地优化对象。同时允许通过 `Object.create(null) `来创建一个没有原型的对象。 | 不支持 IE8 以下的版本。然而，随着微软不再对系统中运行的旧版本浏览器提供支持，这将不是在大多数应用中的主要问题。 另外，这个慢对象初始化在使用第二个参数的时候有可能成为一个性能黑洞，因为每个对象的描述符属性都有自己的描述对象。当以对象的格式处理成百上千的对象描述的时候，可能会造成严重的性能问题。 |
| Object.setPrototypeOf | ` function foo(){} foo.prototype = {  foo_prop: "foo val" }; function bar(){} var proto = {  bar_prop: "bar val" }; Object.setPrototypeOf(  proto, foo.prototype ); bar.prototype = proto; var inst = new bar; console.log(inst.foo_prop); console.log(inst.bar_prop); `` function foo(){} foo.prototype = {  foo_prop: "foo val" }; function bar(){} var proto; proto=Object.setPrototypeOf(  { bar_prop: "bar val" },  foo.prototype ); bar.prototype = proto; var inst = new bar; console.log(inst.foo_prop); console.log(inst.bar_prop)` | 支持所有现代浏览器和微软IE9+浏览器。允许动态操作对象的原型，甚至能强制给通过 `Object.create(null) `创建出来的没有原型的对象添加一个原型。 | 这个方式表现并不好，应该被弃用。如果你在生产环境中使用这个方法，那么快速运行 Javascript 就是不可能的，因为许多浏览器优化了原型，尝试在调用实例之前猜测方法在内存中的位置，但是动态设置原型干扰了所有的优化，甚至可能使浏览器为了运行成功，使用完全未经优化的代码进行重编译。 不支持 IE8 及以下的浏览器版本。 |
| __proto__             | ` function foo(){} foo.prototype = {  foo_prop: "foo val" }; function bar(){} var proto = {  bar_prop: "bar val",  __proto__: foo.prototype }; bar.prototype = proto; var inst = new bar; console.log(inst.foo_prop); console.log(inst.bar_prop); `` var inst = {  __proto__: {    bar_prop: "bar val",    __proto__: {      foo_prop: "foo val",      __proto__: Object.prototype    }  } }; console.log(inst.foo_prop); console.log(inst.bar_prop)` | 支持所有现代非微软版本以及 IE11 以上版本的浏览器。将 `__proto__` 设置为非对象的值会静默失败，并不会抛出错误。 | 应该完全将其抛弃因为这个行为完全不具备性能可言。 如果你在生产环境中使用这个方法，那么快速运行 Javascript 就是不可能的，因为许多浏览器优化了原型，尝试在调用实例之前猜测方法在内存中的位置，但是动态设置原型干扰了所有的优化，甚至可能使浏览器为了运行成功，使用完全未经优化的代码进行重编译。不支持 IE10 及以下的浏览器版本。 |

## (6). Null 和 undefined 的区别 

相同：都会被if判断false

不同：Number(null) // 0   Number(undefined)  NaN

null:表示一个值被定义了，但是该值为空

1、做为一个函数参数时，表明这个参数不是对象

2、作为对象原型链的终点 （Object.getPrototypeOf(Object.prototype)）

3、定义一个值是null 是合理的，定义一个值为undefined是不合理的

undefined:表示缺少值，此处该有值但还未被定义。

1、变量声明了还没有赋值

2、一个函数未被传递的参数

3、函数没有return 默认返回undefined

4、对象没有赋值的属性为undefined

## (7) Call bind apply的区别 

https://www.cnblogs.com/cosiray/p/4512969.html

this.obj.getX.apply(dataObj,[arg1,arg2])

this.obj.getX.call(dataObj,arg1,arg2)

this.obj.getX.bind(dataOb)(arg1,arg2)

## (8) [前端]()缓存的理解 或者 [前端]()数据持久化的理解 

https://juejin.cn/post/6844903561894035463#heading-18

session的概念：session依然是基于cookie，在cookie中保留一个sessionid,这个sessionid就像密码薄，真正的数据由服务器端保存

当用户再次访问该系统其他页面时。就会在cookie带着用户登录的sessionid，这样服务器就可以知道访问的用户

<b>持久化存储</b>

在HTML里面`js文件`里面的变量或对象，每当网页刷新的时候，就会死掉，又重新生成，虽然还是那个`a`，但是刷新后已经是另一块内存了。既然它也没变，我们为什么不把它一直保留着呢，即使刷新了`a`还是那个`a`，也就是持久化存储的意义。以前使用`Cookie`做这个功能，不过`Cookie`每次发请求会把Cookie里面的所有东西都带着去服务器，加重内存的负担，而且请求响应时间长，所以`html5`给了一个新的API `localStorage`

localStorage:

方法:

```
//1. 添加键、值
localStorage.setItem('a', '...')
//2. 获得键、值
localStorage。getItem('a')
//3.清空localStorage
localStorage.clear()
```

第二个参数是json字符串形式

cookie相关

https://segmentfault.com/a/1190000004556040

1. Cookie的特点
   - 服务器通过 Set-Cookie 头给客户端一串字符串
   - 客户端每次访问相同域名的网页时，必须带上这段字符串
   - 客户端要在一段时间内保存这个Cookie
   - Cookie 默认在用户关闭页面后就失效，后台代码可以任意设置 Cookie 的过期时间。比如max-age和后面要讲的`Expires`
   - [大小大概在 4kb 以内](https://stackoverflow.com/questions/640938/what-is-the-maximum-size-of-a-web-browsers-cookies-key)
2. Session的特点
   - 将 SessionID（随机数）通过 Cookie 发给客户端
   - 客户端访问服务器时，服务器读取 SessionID
   - 服务器有一块内存（哈希表）保存了所有 session
   - 通过 SessionID 我们可以得到对应用户的隐私信息，如 id、email
   - 这块内存（哈希表）就是服务器上的所有 session
3. LocalStorage的特点
   - LocalStorage 跟 HTTP 无关
   - 也就是说发送任何请求都不会带上 LocalStorage 的值
   - 只有相同域名的页面才能互相读取 LocalStorage（没有同源那么严格）
   - 每个域名 localStorage 最大存储量为 5Mb 左右（每个浏览器不一样）
   - 常用场景：记录有没有提示过用户（没有用的信息，不能记录密码等敏感信息）
   - LocalStorage 永久有效，除非用户清理缓存

http缓存技术

Cache-Control:

``` javascript
 if (path === '/css/default.css'){
    let string = fs.readFileSync('./css/default.css', 'utf8')
    response.setHeader('Content-Type', 'text/css;charset=utf-8')
    response.setHeader('Cache-Control', 'max-age=1000000')
    response.write(string)
    response.end()
  }
```

通过 max-age 设置缓存有效时间

Expires的英文是到期的意思，很明显与缓存的技术相关。

Expires和本地时间有关。当max-age和Expires共存时，max-age优先度高

ETag：MD5http资源管理的应用

这个响应符时特定的资源版本标记符

如果给定url的资源更改，一定会生成新的Etag符，比较etags能快速确定此资源是否变化，但也可能被跟踪服务器永久存留

HTTP **304** 说明无需再次传输请求的内容，也就是说可以使用缓存的内容。这通常是在一些安全的方法（[safe](https://developer.mozilla.org/zh-CN/docs/Glossary/safe)），例如[`GET`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET) 或[`HEAD`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/HEAD) 或在请求中附带了头部信息： [`If-None-Match`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-None-Match)或[`If-Modified-Since`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Modified-Since)。

Cookie和Session的区别

1. Cookie是存放在浏览器端的数据，每次都随请求发送给 Server。存储`cookie`是浏览器提供的功能。`cookie` 其实是存储在浏览器中的纯文本，浏览器的安装目录下会专门有一个 cookie 文件夹来存放各个域下设置的`cookie`。
2. 而Session是存放在服务器端的内存中，其 Session ID 是通过 Cookie 发送给客户端的，这个Session ID每次都随请求发送给 Server。

Cookie 和 LocalStorage 的区别

1. `Set-Cookie`之后，用户的每次访问服务器，请求里面都会带着`Cookie`到服务器上，与HTTP有关，而`LocalStorage`不用发到服务器端，它是存储在浏览器里面的，与HTTP无关，是浏览器的属性，`window.localStorage`。
2. `Cookie`一般比较小，大约4k左右，而`LocalStorage`大约能用5M
3. `Cookie`默认会在用户关闭页面后失效，不过后端可以设置保存时间，而`LocalStorage`永久有效，除非用户手动清理。

LocalStorage 和 SessionStorage 的区别

1. `LocalStorage`永久有效，除非用户手动清理`localStorage.clear()`。不会自动过期
2. 但是SessionStorage在会话结束后就会失效，也就是用户关闭了页面，就失效了。会自动过期

Cookie 如何设置过期时间？如何删除 Cookie？

1. 设置过期时间：`Set-Cookie: <cookie-name>=<cookie-value>; Expires=<date>`

   data`是格林威治时间，响应头里里面应该这么写代码

   ```
   response.setHeader('Expires', 'Fri, 09 Feb 2018 11:29:48 GMT')
   复制代码
   ```

   也就是说Cookie在格林威治时间的2018年2月9号的11点29分48秒失效。

2. 设置cookie过期时间小于当前时间，那么就会删除该cookie。

```
function deleteCookie(name) {
  document.cookie = name + '=;  expires=Thu, 01 Jan 1970 00:00:01 GMT;'
}
复制代码
```

Cache-Control: max-age=1000 缓存 与 ETag 的「缓存」有什么区别？

1. `Cache-Control: max-age=1000`的缓存 是直接不发请求的，1000秒内相同URL的用户请求资源的时候，不会再去发请求访问服务器了，直接从本地内存的缓存里面获取
2. `ETag`的缓存是不管怎么样都要发起请求，第二次访问的是时候会多一个请求头`If-None-Match : md5值`，如果两次请求之间的MD5值相同就不会去下载新的文件，响应体是第一次下载的；如果MD5值变了，就要去下载新的文件。

## （9）防抖和节流 

https://www.jianshu.com/p/c8b86b09daf0

vue 防抖节流未掌握，原因不明，dome不出来

## （10）闭包 

https://blog.csdn.net/weixin_43586120/article/details/89456183

闭包的特点

1、让外部访问函数内部变量成为可能；

2、局部变量会常驻内存里

3、可以避免使用全局变量，防止变量污染

4、会造成内存泄露

应用场景：闭包找到的是统一地址的父级函数变量最终值

1、实例化

```js
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);
```

2、用闭包模拟私有方法

```js
var Counter = (function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }   
})();

console.log(Counter.value()); /* logs 0 */
Counter.increment();
Counter.increment();
console.log(Counter.value()); /* logs 2 */
Counter.decrement();
console.log(Counter.value()); /* logs 1 */
```



https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures

## （11）数组去重 

俩种思路

1、双循环

2.利用语法自身键不可重复性
其他的都是用了语言不通的api,算不上单独的一种方法，比如indexOf 和includes 两层循环 都是同一类

https://segmentfault.com/a/1190000016418021

## 12、深度拷贝

浅拷贝，深拷贝区别，有没有分配新的内存

1array.slice(start，end)，

2、array.concat(array1，array2，....) 只有一个参数

3、copyof()

4、JSON.parse(JSON.stringify(array))

## 13、原型链

什么是原型链：

​    每个对象都可以有一个原型_proto_，这个原型还可以有它自己的原型，以此类推，形成一个原型链。查找特定属性的时候，我们先去这个对象里去找，如果没有的话就去它的原型对象里面去，如果还是没有的话再去向原型对象的原型对象里去寻找...... 这个操作被委托在整个原型链上，这个就是我们说的原型链了。

https://www.cnblogs.com/xfcao/p/10029731.html

搞清楚构造函数，原型和实例的关系

**1、****构造函数、原型和实例之间的关系**

​    ①+Object

![img](https://images2015.cnblogs.com/blog/918547/201606/918547-20160627093029781-1671268020.png)

　　 ②+Function+Object+Array

　　![img](https://images2015.cnblogs.com/blog/918547/201606/918547-20160627093126312-157612390.png)



![img](https://upload-images.jianshu.io/upload_images/15932532-cb246befed007789.png?imageMogr2/auto-orient/strip|imageView2/2/w/638)







每一个实例都有_proto_  每一个构造函数都有prototype 这俩个都指向原型对象，而原型对象也会有原型对象，直到proto指向null。

原型对象prototype里面有一个constructor属性，该属性指向原型对象所属的构造函数

## 14、require和import

https://www.jianshu.com/p/f1e54dde30c8

**`require`** 是赋值过程，其实`require`的结果就是对象、数字、字符串、函数等，再把结果赋值给某个变量。它是普通的值拷贝传递。
 **`import`** 是解构过程。使用`import`导入模块的属性或者方法是引用传递。且`import`是`read-only`的，值是单向传递的。`default`是ES6 模块化所独有的关键字，`export default {}` 输出默认的接口对象，如果没有命名，则在`import`时可以自定义一个名称用来关联这个对象

