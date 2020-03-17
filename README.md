# blog

This is my first commit.

<h1>css小结：</h1>
1.  水平居中的  margin:0 auto   用于块级元素上。
2.  水平居中    内联元素添加 display:inline-block 后    在父元素上添加 text-align:center 
3.  水平垂直居中    设置padding和margin的值使其居中，一般相对方向同时添加一样的值。
4.  水平垂直居中    确定宽度的    margin：0px auto
5.  水平垂直居中 直接添加   display: flex;  justify-content: center;    align-items: center;




<h1>JS 数据类型</h1>
一 简介

1.  数值（number）：整数和小数（比如1和3.14）
    字符串（string）：文本（比如Hello World）
    布尔值（boolean）：表示真伪的两个特殊值，即true（真）和false（假）
    undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
    null：表示空值，即此处的值为空
    对象（object）：各种值组成的集合
2.  typeof运算符可以返回一个值的数据类型。

二 数据

1.  所有数字都是以64位浮点数形式存储的

    第1位：符号位，0表示正数，1表示负数
    第2位到第12位（共11位）：指数部分
    第13位到第64位（共52位）：小数部分（即有效数字）
    （如果指数部分的值在0到2047之间（不含两个端点），那么有效数字的第一位默认总是1，不保存在64位浮点数之中。）

2.  数值范围
    数值范围为21024到2-1023（开区间）
    如果一个数大于等于2的1024次方，这时就会返回Infinity。
    如果一个数小于等于2的-1075次方，这时会直接返回0。

3.  进制
    八进制：有前缀0o或0O的数值，或者有前导0。
    十六进制：有前缀0x或0X的数值。
    二进制：有前缀0b或0B的数值。

4.  特殊数值
    NAN 表示“非数字”（Not a Number）,主要出现在将字符串解析成数字出错的场合。
    Infinity表示“无穷”

5.  用法
    parseInt 方法用于将字符串转为整数。
    parseFloat方法用于将一个字符串转为浮点数。
    isNaN方法可以用来判断一个值是否为NaN。
    isFinite方法返回一个布尔值，表示某个值是否为正常的数值。

三 null, undefined，boolean

1.  null是一个表示“空”的对象，转为数值时为0；
    undefined是一个表示"此处无定义"的原始值， 转为数值时为NaN。    
    变量没有值--undefined
    有一个object没有给值--null
    有一个非对象没有给值--nudefined

2.  “真”用关键字true表示，“假”用关键字false表示。
    undefined  null  false  0  NaN  ""或''（空字符串）会被视为false
    空数组（[]）和空对象（{}）对应的布尔值，都是true。

四 字符串

1.  约定 JavaScript 语言的字符串只使用单引号

2.  （+）可以连接多个单行字符串

3.  \0 ：null（\u0000）
    \b ：后退键（\u0008）
    \f ：换页符（\u000C）
    \n ：换行符（\u000A）
    \r ：回车键（\u000D）
    \t ：制表符（\u0009）
    \v ：垂直制表符（\u000B）
    \\' ：单引号（\u0027）
    \\" ：双引号（\u0022）
    \\\ ：反斜杠（\u005C）

4.  符串内部的单个字符无法改变和增删，这些操作会默认地失败

5.  对于码点在U+10000到U+10FFFF之间的字符，JavaScript 总是认为它们是两个字符（length属性为2）。所以处理的时候，必须把这一点考虑在内，也就是说，JavaScript 返回的字符串长度可能是不正确的。

五 对象

1.  对象的所有键名都是字符串

2.  如果键名是数值，会被自动转为字符串。

3.  如果键名不符合标识名的条件，且也不是数字，则必须加上引号，否则会报错。

4.  可以在定义完后再给对象添加属性

5.  如果不同的变量名指向同一个对象，修改其中一个变量，会影响到其他所有变量。如果取消某一个变量对于原对象的引用，不会影响到另一个变量。（这种引用只局限于对象，不适用于原始类型）

6.  可以使用点运算符，方括号运算符引用对象。
    如果使用方括号运算符，键名必须放在引号里面，否则会被当作变量处理。
    数字键可以不加引号，因为会自动转成字符串。
    数值键名不能使用点运算符（因为会被当成小数点），只能使用方括号运算符。
    
7.  delete命令用于删除对象的属性
    in运算符用于检查对象是否包含某个属性
    for...in循环用来遍历一个对象的全部属性。

<hr>

六 类型转换

1.  任意类型转数字 <br>
    1.	Number(x)
    2.	parseInt(x, 10) 
    3.	parseFloat(x) 
    4.	x - 0
    5.	+x
2.  任意类型转字符串 <br>
    1.	String(x)
    2.	x.toString()   //null,undefined 会报错
    3.	x + ''   //1+'1'==='11'
3.  任意类型转布尔
    1.	Boolean(x)
    2.	!!x

七 内存图

1.	Chrome 打开即占用 1G 内存
2.	Chrome 各每个网页分配一定数量的内存
3.	这些内存要分给页面渲染器、网络模块、浏览器外壳和 JS 引擎（V8引擎）
4.	JS 引擎将内存分为代码区和数据区
5.	我们只研究数据区
6.	数据区分为 Stack（栈内存） 和 Heap（堆内存）
7.	简单类型的数据直接存在 Stack 里
8.	复杂类型的数据是把 Heap 地址存在 Stack 里
    （遇到问题就画图，不要分析。）
<br>

```javascript
var a = 1
var b = a
b = 2
a   //1
```

```javascript
var a = {name: 'a'}
var b = a
b = {name: 'b'}
a.name //'a'
```

```javascript
var a = {name: 'a'}
var b = a
b.name = 'b'
a.name //'b'
```
```javascript
var a = {name: 'a'}
var b = a
b = null
a // {name: 'a'}
```

八 面试题

```javascript
var a={n:1};
var b=a;
a.x=a={n:2};//关键代码

console.log(a.x);//undefined
console.log(b.x);//[object Object]
```

九 垃圾回收

如果一个对象没有被引用，特就是垃圾，将会被回收。<br>
1.  
```javascript
var a = 1
var b = a
b = 2 //这个时候改变 b,a 完全不受 b 的影响
```
那么我们就说这是一个深复制,对于简单类型的数据来说，赋值就是深拷贝。对于复杂类型的数据（对象）来说，才要区分浅拷贝和深拷贝。

2.  这是一个浅拷贝的例子
```javascript
var a = {name: 'frank'}
var b = a
b.name = 'b'
a.name === 'b' // true,因为我们对 b 操作后，a 也变了
```
3.  什么是深拷贝了，就是对 Heap 内存进行完全的拷贝。
```javascript
var a = {name: 'frank'}
var b = deepClone(a) // deepClone 没有学
b.name = 'b'
a.name === 'a' // true
```



