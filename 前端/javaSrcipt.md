<h1>javaSrcipt</h1>

## 条件语句

#1 if else

#2 else if

## 比较运算符

- `===` 和 `!==` — 判断一个值是否严格等于，或不等于另一个。
- `<` 和 `>` — 判断一个值是否小于，或大于另一个。
- `<=` 和 `>=` — 判断一个值是否小于或等于，或者大于或等于另一个。

## 逻辑表达式

&&逻辑与；俩个或更多的表达式，只有这些表达式每一个都返回true ，整个表达式才返回true

||逻辑或；当俩个或跟多个表达式有一个返回true，整体返回true

！逻辑非；对一个布尔值取反

## switch

```html
switch (expression) {
  case choice1:
    run this code
    break;

  case choice2:
    run this code instead
    break;
  
  // include as many cases as you like

  default:
    actually, just run this code
}
```

## 三元运算符

```html
( condition ) ? run this code : run this code instead
```

## for循环

```html
for (initializer; exit-condition; final-expression) {
  // code to run
}
```

break退出循环

continue 跳过迭代

## while 循环

```js
var i = 0;

while (i < cats.length) {
  if (i === cats.length - 1) {
    info += 'and ' + cats[i] + '.';
  } else {
    info += cats[i] + ', ';
  }

  i++;
}
```

do while

```html
initializer
do {
  // code to run

  final-expression
} while (exit-condition)
```

## JavaScript线程

javaSrcipt是单线程的

```html
Task A --> Task B --> Task C
```

callbacks 异步函数

待录

## JavaScript Api

api可以做什么

1. 操作文档的api https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents
2. 从服务器获取数据的Api https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data
3. 用于绘制图形的api  <canvas>
4. 音频和视频的api

https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Audio_API

https://developer.mozilla.org/zh-CN/docs/MDN/Doc_status/API/WebRTC

5. 操作设备的api

https://developer.mozilla.org/zh-CN/docs/Web/API/Notifications_API

6. 客户端储存的api

https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Storage_API

api的可识别入口

使用API时，应确保知道API入口点的位置。 在Geolocation API中，这非常简单 - 它是 [`Navigator.geolocation`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/geolocation) 属性, 它返回浏览器的 [`Geolocation`](https://developer.mozilla.org/zh-CN/docs/Web/API/Geolocation) 对象，所有有用的地理定位方法都可用。

文档对象模型 (DOM) API有一个更简单的入口点 —它的功能往往被发现挂在 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 对象, 或任何你想影响的HTML元素的实例，例如：

```js
var em = document.createElement('em'); // create a new em element
var para = document.querySelector('p'); // reference an existing p element
em.textContent = 'Hello there!'; // give em some text content
para.appendChild(em); // embed em inside para
```

其他API具有稍微复杂的入口点，通常涉及为要编写的API代码创建特定的上下文。例如，Canvas API的上下文对象是通过获取要绘制的 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/canvas) 元素的引用来创建的，然后调用它的[`HTMLCanvasElement.getContext()`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement/getContext)方法：

## promises对象（es6 特性）

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise

## proxy and reflect

### in关键词

let arr = [1, 2, 34, 5]

let obe = { name: "zyt" }

console.log(3 in arr) //true

console.log('name' in obe)//true

## moudule 模块化

# ES6

## let 和const


| let | var |
| :-: | :-: |
| 只在声明代码块内有效 | 全局有效 |
| 不存在变量提升（即变量可以在声明之前使用，值为`undefined`） | 存在变量提升 |
| 暂时性死区 | 无暂时性死区 |
| `let`不允许在相同作用域内，重复声明同一个变量。 | 允许重复声明同一个变量 |

```javascript
//变量提升
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

```javascr
//暂时性死区

var a=1;

f(){
a=2 //ReferenceError
let a=3
}
```

const:

`const`声明一个只读的常量。一旦声明，常量的值就不能改变。

const 同样不可重复声明

补充：es6 六种声明方式

import

class

const

let

var

function

## 解构赋值

### 数组解构赋值

```javas
//例
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []

//默认值
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```

对对象建构

不同，数组解构通过顺序，对象解构是匹配相同的属性名

如解构失败则为 undefined

```javascript
// 例一
let { log, sin, cos } = Math;

// 例二
const { log } = console;
log('hello') // hello
```

超强功能，获取math中 对数,正玄等方法

```javascript
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world'
```

这实际上说明，对象的解构赋值是下面形式的简写（参见《对象的扩展》一章）。

```javascript
let { foo: foo, bar: bar } = { foo: 'aaa', bar: 'bbb' };
```

也就是说，对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

## str

对string的扩展

JavaScript 共有 6 种方法可以表示一个字符。

```javascript
'\z' === 'z'  // true
'\172' === 'z' // true
'\x7A' === 'z' // true
'\u007A' === 'z' // true
'\u{7A}' === 'z' // true
```

```
iterator
```

```javascript
 for (const iterator of 'object') {
        console.log(iterator)
      }
```

为了确保返回的是合法的 UTF-8 字符，[ES2019](https://github.com/tc39/proposal-well-formed-stringify) 改变了`JSON.stringify()`的行为。如果遇到`0xD800`到`0xDFFF`之间的单个码点，或者不存在的配对形式，它会返回转义字符串，留给应用自己决定下一步的处理。

```javascript
JSON.stringify('\u{D834}') // ""\\uD834""
JSON.stringify('\uDF06\uD834') // ""\\udf06\\ud834""
```

template string

## String Function


| es5           formCharCode | es6          fromCodePoint |
| - | - |
| 不能识别大于0xffff码点 | 可以大于 |
|   |   |

`fromCodePoint`方法定义在`String`对象上，而`codePointAt`方法定义在字符串的实例对象上。

## 实例方法：includes(), startsWith(), endsWith()

传统上，JavaScript 只有`indexOf`方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6 又提供了三种新方法。

- **includes()**：返回布尔值，表示是否找到了参数字符串。
- **startsWith()**：返回布尔值，表示参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，表示参数字符串是否在原字符串的尾部。

```javascript
let s = 'Hello world!';

s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
```

这三个方法都支持第二个参数，表示开始搜索的位置。

```javascript
let s = 'Hello world!';

s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```

上面代码表示，使用第二个参数`n`时，`endsWith`的行为与其他两个方法有所不同。它针对前`n`个字符，而其他两个方法针对从第`n`个位置直到字符串结束。

`repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

```javascript
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""
```

[ES2019](https://github.com/tc39/proposal-string-left-right-trim) 对字符串实例新增了`trimStart()`和`trimEnd()`这两个方法。它们的行为与`trim()`一致，`trimStart()`消除字符串头部的空格，`trimEnd()`消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串。

```javascript
const s = '  abc  ';

s.trim() // "abc"
s.trimStart() // "abc  "
s.trimEnd() // "  abc"
```

`matchAll()`方法返回一个正则表达式在当前字符串的所有匹配，详见《正则的扩展》的一章。

```javascript
Number.isInteger(3.0000000000000002) // true
```

上面代码中，`Number.isInteger`的参数明明不是整数，但是会返回`true`。原因就是这个小数的精度达到了小数点后16个十进制位，转成二进制位超过了53个二进制位，导致最后的那个`2`被丢弃了。

JavaScript 能够准确表示的整数范围在`-2^53`到`2^53`之间（不含两个端点），超过这个范围，无法精确表示这个值。

Number.SafeInteger()

### Math.sign()

`Math.sign`方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。

它会返回五种值。

- 参数为正数，返回`+1`；
- 参数为负数，返回`-1`；
- 参数为 0，返回`0`；
- 参数为-0，返回`-0`;
- 其他值，返回`NaN`。

Math.imul()

`Math.imul`方法返回两个数以 32 位带符号整数形式相乘的结果，返回的也是一个 32 位的带符号整数。

不同

```javascript
(0x7fffffff * 0x7fffffff)|0 // 0
Math.imul(0x7fffffff, 0x7fffffff) // 1
```

## 数组的扩展~~~~

## Array.from()

`Array.from`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。

下面是一个类似数组的对象，`Array.from`将它转为真正的数组。

只能将类似数组对象转换

## for

* for
* forerch
* for in~~~~
* for of

## set


| set | WeakSet |
| - | - |
|   | WeakSet成员只能是对象 |
|   | WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。 |
|   | WeakSet 不能遍历，因为是弱引用，不能保证每个成员存在 |
