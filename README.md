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

十 全局对象

ECMAScript 规定全局对象叫做 global，但是浏览器把 window 作为全局对象。window里面有很多属性，都是全局变量，分为两类：
1.  ECMAScript 规定的，     </br>
	global.parseInt     </br>
    global.parseFloat     </br>
	global.Number     </br>
	global.String     </br>
    global.Boolean     </br>
	global.Object     </br>
2.	一种是浏览器自己加的属性     </br>
	window.alert     </br>
	window.prompt     </br>
	window.comfirm     </br>
	window.console.log     </br>
	window.console.dir     </br>
	window.document     </br>
	window.document.createElement     </br>
	window.document.getElementById     </br>

十一 全局函数

Number()    <br>
```javascript
var n1 = 1   //内存中就是1
var n2 = new Number(1)   //创建了一个对象，包含了一些函数
n1.tostring() // 把n1临时转换成一个对象
```
String()    Boolean()   Object()    同上，其中
```javascript
var n1 = {}   
var n2 = new object()
// n1 n2没有区别   但是
n1 ===n2  //false
```

十二 公用属性

见图一

十三 公式

```
var 对象 = new 函数()
对象.__proto__ === 函数.prototype

函数.prototype.__proto__ === object.prototype
函数.__proto__ === function.prototype
function.__proto__ === function.prototype
function.prototype.__proto__ === object.prototype
```

十四 数组

1.  任何类型的数据，都可以放入数组。
2.  用数值和字符串作为键名，结果都能读取数组，原因是数值键名被自动转为了字符串。这点在赋值时也成立，一个值总是先转成字符串，再作为键名进行赋值。
3.  length属性是一个动态的值，等于键名中的最大整数加1。length属性是可写的。设置一个小于当前成员个数的值，该数组的成员会自动减少到length设置的值。
```javascript
var arr = [ 'a', 'b', 'c' ];
arr.length = 0;
arr   // []    清空一个数组
```
设置length大于当前元素个数，则数组的成员数量会增加到这个值，新增的位置都是空位。读取新增的位置都会返回undefined。

4.  ```javascript
    var a = [];
    a['p'] = 'abc';
    a.length // 0
    a[2.1] = 'abc';
    a.length // 0
    ```
上面代码将数组的键分别设为字符串和小数，结果都不影响length属性

5.  in检查某个键名是否存在，for...in循环遍历数组（不仅会遍历数组所有的数字键，还会遍历非数字键。）

6.  当数组的某个位置是空元素，即两个逗号之间没有任何值，我们称该数组存在空位，数组的空位不影响length属性。数组的空位是可以读取的，返回undefined。数组的空位是可以读取的，返回undefined。使用数组的forEach方法、for...in结构、以及Object.keys方法进行遍历，空位都会被跳过，undefined不会

7.  ```javascript
    var obj = {
    0: 'a',
    1: 'b',
    2: 'c',
    length: 3}
    ```
只要有length属性，就可以认为这个对象类似于数组，但是length属性不是动态值
```javascript
var arr = Array.prototype.slice.call(arrayLike);
```
数组的slice方法可以将“类似数组的对象”变成真正的数组。

十五 Array 对象

1.  ```javascript
    var a = new Array(2)
    //等同于
    var a = Array(2)

    var a = array(1,2,3)   //[1,2,3]
    ```
Array作为构造函数，行为很不一致.推荐 var arr = [1, 2];

2.  join()方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。不改变原数组
```javascript
var a = [1, 2, 3, 4];

a.join(' ')     // '1 2 3 4'
a.join(' | ')   // "1 | 2 | 3 | 4"
a.join()    // "1,2,3,4"
```
如果数组成员是undefined或null或空位，会被转成空字符串。

3.  concat方法用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。
```javascript
['hello'].concat(['world'], ['!'])      // ["hello", "world", "!"]
[1, 2, 3].concat(4, 5, 6)       // [1, 2, 3, 4, 5, 6]

var obj = { a: 1 };
var oldArray = [obj];
var newArray = oldArray.concat();
obj.a = 2;
newArray[0].a       // 2

//原数组包含一个对象，concat方法生成的新数组包含这个对象的引用。所以，改变原对象以后，新数组跟着改变。
```

4.  sort方法对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。
```javascript
['d', 'c', 'b', 'a'].sort()     // ['a', 'b', 'c', 'd']
[11, 101].sort()        // [101, 11]
```
如果想让sort方法按照自定义方式排序，可以传入一个函数作为参数。
```javascript
[10111, 1101, 111].sort(function (a, b) {
  return a - b;
})      // [111, 1101, 10111]

//如果该函数的返回值大于0，表示第一个成员排在第二个成员后面；其他情况下，都是第一个元素排在第二个元素前面。
```

5.  map方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。
```javascript
var numbers = [1, 2, 3];
numbers.map(function (n) {
  return n + 1;
});     // [2, 3, 4]

numbers     // [1, 2, 3]  原数组不变
```
如果数组有空位，map方法的回调函数在这个位置不会执行，会跳过数组的空位。

6. forEach与map方法很想，但是不返回值，只用来操作数据
```javascript
function log(element, index, array) {
  console.log('[' + index + '] = ' + element);
}

[2, 5, 9].forEach(log);     // [0] = 2  [1] = 5 [2] = 9
```

7. filter方法用于过滤数组成员，满足条件的成员组成一个新数组返回。它的参数是一个函数，所有数组成员依次执行该函数，返回结果为true的成员组成一个新数组返回。该方法不会改变原数组。
```javascript
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
})      // [4, 5]
```

8. reduce方法和reduceRight方法依次处理数组的每个成员，最终累计为一个值。它们的差别是，reduce是从左到右处理（从第一个成员到最后一个成员），reduceRight则是从右到左（从最后一个成员到第一个成员），其他完全一样。
```javascript
[1, 2, 3, 4, 5].reduce(function (a, b) {
    console.log(a, b);  //  a为累积变量，默认为数组的第一个成员
    return a + b;       //   b为当前变量，默认为数组的第二个成员
})      // 1 2      3 3     6 4     10 5    最后结果：15
```
```javascript
[1, 2, 3, 4, 5].reduce(function (a, b) {
  return a + b;
}, 10);
// 25  从指定值相加
```
