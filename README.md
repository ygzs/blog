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

1.  所有数字都是以64位浮点数形式存储的          </br>
    第1位：符号位，0表示正数，1表示负数     </br>
    第2位到第12位（共11位）：指数部分       </br>
    第13位到第64位（共52位）：小数部分（即有效数字）        </br>
    （如果指数部分的值在0到2047之间（不含两个端点），那么有效数字的第一位默认总是1，不保存在64位浮点数之中。）

2.  数值范围
    数值范围为21024到2-1023（开区间） </br>
    如果一个数大于等于2的1024次方，这时就会返回Infinity。
    如果一个数小于等于2的-1075次方，这时会直接返回0。

3.  进制
    八进制：有前缀0o或0O的数值，或者有前导0。       </br>
    十六进制：有前缀0x或0X的数值。      </br>
    二进制：有前缀0b或0B的数值。        </br>

4.  特殊数值
    NAN 表示“非数字”（Not a Number）,主要出现在将字符串解析成数字出错的场合。</br>
    Infinity表示“无穷”

5.  用法
    parseInt 方法用于将字符串转为整数。  </br>
    parseFloat方法用于将一个字符串转为浮点数。      </br>
    isNaN方法可以用来判断一个值是否为NaN。      </br>
    isFinite方法返回一个布尔值，表示某个值是否为正常的数值。        </br>

三 null, undefined，boolean

1.  null是一个表示“空”的对象，转为数值时为0；       </br>
    undefined是一个表示"此处无定义"的原始值， 转为数值时为NaN。     </br> 
    变量没有值--undefined       </br>
    有一个object没有给值--null      </br>
    有一个非对象没有给值--nudefined     </br>

2.  “真”用关键字true表示，“假”用关键字false表示。  </br>
    undefined  null  false  0  NaN  ""或''（空字符串）会被视为false     </br>
    空数组（[]）和空对象（{}）对应的布尔值，都是true。      </br>

四 字符串

1.  约定 JavaScript 语言的字符串只使用单引号

2.  （+）可以连接多个单行字符串

3.  \0 ：null（\u0000）         </br>
    \b ：后退键（\u0008）       </br>
    \f ：换页符（\u000C）       </br>
    \n ：换行符（\u000A）       </br>
    \r ：回车键（\u000D）       </br>
    \t ：制表符（\u0009）       </br>
    \v ：垂直制表符（\u000B）       </br>
    \\' ：单引号（\u0027）      </br>
    \\" ：双引号（\u0022）      </br>
    \\\ ：反斜杠（\u005C）      </br>

4.  符串内部的单个字符无法改变和增删，这些操作会默认地失败

5.  对于码点在U+10000到U+10FFFF之间的字符，JavaScript 总是认为它们是两个字符（length属性为2）。所以处理的时候，必须把这一点考虑在内，也就是说，JavaScript 返回的字符串长度可能是不正确的。

五 对象

1.  对象的所有键名都是字符串

2.  如果键名是数值，会被自动转为字符串。

3.  如果键名不符合标识名的条件，且也不是数字，则必须加上引号，否则会报错。

4.  可以在定义完后再给对象添加属性

5.  如果不同的变量名指向同一个对象，修改其中一个变量，会影响到其他所有变量。如果取消某一个变量对于原对象的引用，不会影响到另一个变量。（这种引用只局限于对象，不适用于原始类型）

6.  可以使用点运算符，方括号运算符引用对象。   </br>
    如果使用方括号运算符，键名必须放在引号里面，否则会被当作变量处理。  </br>
    数字键可以不加引号，因为会自动转成字符串。   </br>
    数值键名不能使用点运算符（因为会被当成小数点），只能使用方括号运算符。  </br>
    
7.  delete命令用于删除对象的属性
    in运算符用于检查对象是否包含某个属性
    for...in循环用来遍历一个对象的全部属性。
```javascript
var classes = {'a':true,'b':false,'c':true}
	for(var key in classes){
		var value = classes[key]//不能使用 . 会被当成classes中的属性，返回undefined
		console.log(value)
	}
```

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
    length: 3 //不是动态值}
    ```
伪数组就是原型链(_proto_)中没有Array.prototype
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

十六 函数

1.  函数的声明方式      </br>
```javascript
function f(x,y){
	return x+y
}
f.name      // 'f'
//具名函数
```
```javascript
var f = function(x,y){
	return x+y
}
f.name      // 'f'
//匿名函数
```
```javascript
var f = function f2(x,y){ return x+y }
	f.name // 'f2'
console.log(f2) // undefined
//具名函数赋值
```
```javascript
var f = new Function('x','y','return x+y')
	f.name // "anonymous"
// new Function
```
```javascript
var f = (x,y) => {
	return x+y
}
//箭头函数
```

2.  f.call(asThis, input1,input2)
其中 asThis 会被当做 this（通常是undefined），[input1,input2] 会被当做 arguments

3.  调用栈(call stack)：调用栈的主要功能是保存调用的返回地址。每次函数执行完，返回到当前调用函数的位置执行下面的代码

4.  按照语法树，就近原则（只看声明语句）        </br>
我们只能确定变量是哪个变量，但是不能确定变量的值          </br>
它的作用域与变量一样，就是其声明时所在的作用域，与其运行时所在的作用域无关。    </br>
a=3,并不是在声明全局变量。如果在其父作用域中有声明a，那么仅仅是赋值。如果都没有就是声明加赋值
```javascript
var a = 1
function f1(){
    alert(a)    //变量提升，a是undefined
    var a = 2
}
f1.call()
```
```javascript
var a = 1
function f1(){
    var a = 2
    f2.call()
}
function f2(){
    console.log(a)  // a=1
}
f1.call()
```
```javascript
var liTags = document.querySelectorAll('li')
for(var i = 0; i<liTags.length; i++){
    liTags[i].onclick = function(){
        console.log(i) // 点击第3个 li 时，打印出6（此时for循环执行完毕）
    }
}
```

5.  如果一个函数使用了特作用域外的变量，那么（这个函数+这个变量）就叫做闭包

十七 DOM API

1.  文档对象模型 (DOM) 是HTML和XML文档的编程接口。它给文档（结构树）提供了一个结构化的表述并且定义了一种方式—程序可以对结构树进行访问，以改变文档的结构，样式和内容。

2.  DOM 提供了一种表述形式将文档作为一个结构化的节点组以及包含属性和方法的对象。从本质上说，它将web 页面和脚本或编程语言连接起来了。（图）

3.  innerText 和 textContent 区别：        </br>
textContent 会获取所有元素的内容，包括 script 和 style 元素，然而 innerText 只展示给人看的元素        </br>
textContent 会返回节点中的每一个元素。相反，innerText 受 CSS 样式的影响，并且不会返回隐藏元素的文本       </br>
nextSibling,previousSibling 可能会获取到文本（回车）        </br>
nodeType的值：1表示元素；3表示文本          </br>
node.cloneNode(deep)  : deep是否采用深度克隆,如果为true,则该节点的所有后代节点也都会被克隆,如果为false,则只克隆该节点本身.

4.  document.location : 属性返回一个只读对象，提供了当前文档的URL信息 </br>
Document.referrer : 返回跳转或打开到当前页面的页面的 URI。如果用户直接打开了这个页面（不是通过页面跳转，而是通过地址栏或者书签等打开的），则该属性为空字符串   </br>

5.  getAttribute()  用于获取元素的attribute(属性)值      </br>
innerText是一个可写属性，返回元素内包含的文本内容，在多层次的时候会按照元素由浅到深的顺序拼接其内容      </br>
innerHTML属性作用和innerText类似，但是不是返回元素的文本内容，而是返回元素的HTML结构，在写入的时候也会自动构建DOM            </br>

十八 jquery 1

1.  封装                    </br>
```javascript
//查找一个节点的兄弟节点
function getsiblings(node){
	var brothers = node.parentNode.children
	var array = {length:0}
	for(var i=0;i<brothers.length;i++){
 		if(brothers[i] !== node){
    	    array[array.length] = brothers[i] 
    	    array.length += 1
  		}
	}
	return array
}

//给一个节点添加class
function addclass(node，classes){
	for(var key in classes){
		var value = classes[key]
        var method = value ? 'add' : 'remove'
        node.classList[method](key)
	}
}
```

2.  命名空间   </br>
```javascript
dom(){}
dom.getsiblings =  getsiblings
dom.addclass = addclass

dom.getsibling(node)
dom.addclass(node, {a: true, b: false})
```

3.  node在前：
方法一：直接在 Node.prototype 上加函数
方法二：新的接口 BetterNode
```javascript
window.jquery = function(NodeOrSelector){
	let nodes = {}
	if(typeof NodeOrSelector === 'string'){
		let temp =document.querySelectorAll(NodeOrSelector)
		for (let i = 0; i < temp.length; i++) {
			nodes[i] = temp[i]
			nodes.length = temp.length
		}
	}       //如果是选择器返回所有节点
	else if(NodeOrSelector instanceof node){
		nodes = {
			0:NodeOrSelector,
			length:1
		}
	}       //返回当前一个节点
	nodes.getsiblings = function(){}
	nodes.addclass = function(classes){
		classes.forEach( value => {
			for (let i = 0; i < nodes.length; i++) {
				nodes[i].classList.add(value) 
			}
		})
	}
    nodes.test = function(text){
		if(text === undefined){
			var texts = []
			for (let i = 0; i < nodes.length; i++) {
				texts.push( nodes[i].textContent )
			}
		return texts
		}
		else{
			for (let i = 0; i < nodes.length; i++) {
				nodes[i].textContent = text
			}
			return texts
		}
	}
    return nodes
}		
	var node2 = jquery('ul > li')
	node2.addclass(['a'])
    node2.text('hi')
```

十九 DOM事件

1.  ```html
     <script>
        function print(){
            console.log('hi');    
        }
    </script>
    <button id="X" onclick="print">A</button>
    <button id="Y" onclick="print()">B</button>
    <button id="Z" onclick="print.call()">C</button>
    ```
B C 是对的，onclick='要执行的代码',用户一旦点击，浏览器就eval('要执行的代码')

2.  ```javascript
        function(){
            console.log('hi');
        }
        X.onclick = print //相当于给X添加一个函数类型的属性
        X.onclick = print()
        X.onclick = print.call()
    ```
一旦用户点击，浏览器就调用这个函数

3.  ```javascript
        xxx.addEventListener('click',f1)
        xxx.addEventListener('click',f1)
    ```
可以添加多个时间监听事件

4.  事件冒泡：事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的元素 </br>
    事件捕获：不太具体的节点更早接收事件，而最具体的元素最后接收事件，和事件冒泡相反 

addEventListener    removeEventListener   </br>
第三个参数如果是true表示在捕获阶段调用事件处理程序，如果是false，则是在事件冒泡阶段处理
如果最后一个事件既有捕获阶段又有冒泡阶段，则按照顺序执行