一 JSONP

请求方：前端程序员（浏览器)                                                    </br>
响应方：后端程序员（服务器)                                                    </br>
1.	请求方创建 script，src 指向响应方，同时传一个查询参数 ?callbackName=yyy
2.	响应方根据查询参数callbackName，构造形如                                   </br>
        i.	yyy.call(undefined, '你要的数据')                                </br>
        ii.	yyy('你要的数据')                                                </br>
这样的响应
3.	浏览器接收到响应，就会执行 yyy.call(undefined, '你要的数据')
4.	那么请求方就知道了他要的数据
5.  jsonp 就是动态的创建script，所以只能发 get 请求

约定：                                                                       </br>
1.	callbackName -> callback
2.	yyy -> 随机数 ygzs123456789()

二 AJAX

1.  用 form 可以发请求，但是会刷新页面或新开页面                                </br>
    用 a 可以发 get 请求，但是也会刷新页面或新开页面                            </br>
    用 img 可以发 get 请求，但是只能以图片的形式展示                            </br>
    用 link 可以发 get 请求，但是只能以 CSS、favicon 的形式展示                 </br>
    用 script 可以发 get 请求，但是只能以脚本的形式运行                         </br>

2.  AJAX：异步的 JavaScript 和 XML                                           </br>
    使用 XMLHttpRequest 发请求                                              </br>
	服务器返回 XML 格式的字符串                                              </br>
	JS 解析 XML，并更新局部页面                                              </br>

3.  JSON是一门新的语言，只有 协议+端口+域名 一模一样才允许发 AJAX 请求（同源策略）

4.  CORS 跨域:                                                              </br>
    response.setHeader('Access-Control-Allow-Origin', 'https://xxx.com')

三 AJAX 2

1.  客户端的js发起请求，服务端的js发出响应                                      </br>
	JS 可以设置任意请求 header 吗                                             </br>
        第一部分 request.open('get', '/xxx')                                 </br>
        第二部分 request.setRequestHeader('content-type','x-www-form-urlencoded')
        第四部分 request.send('a=1&b=2')                                     </br>
	JS 可以获取任意响应 header 吗？                                           </br>
        第一部分 request.status / request.statusText                         </br>
        第二部分 request.getResponseHeader() / request.getAllResponseHeaders()<br>
        第四部分 request.responseText                                        

2.  callback(回调)                                                           </br>
    回调就是一个函数的调用过程。函数a有一个参数，这个参数是个函数b，当函数a执行完以后执行函数b。那么这个过程就叫回调。                                              </br>
    函数b是你以参数形式传给函数a的，那么函数b就叫回调函数。                      </br>
    一般与异步（不等结果就执行下面的代码）一起使用，返回异步的结果 

3.  promise                                                                  </br>
    防止命名的不同                                                            </br>
    同一状态多次处理                                                          </br>
    return new Promise(function(resolve,reject){...})                        </br>

四

1.	如何使用立即执行函数

(1) 我们不想要全局变量，我们要使用局部变量,                                     </br>
(2) ES 5 里面，只有函数有局部变量，于是我们声明一个 function xxx，然后 xxx.call()，

(3) 这个时候 xxx 是全局变量，所以我们不能给这个函数名字，function(){}.call()，   </br>
(4) 但是 Chrome 报错，语法错误，试出来一种方法可以不报错:                       </br>
i.	!function(){}.call() (我们不在乎这个匿名函数的返回值，所以加个!取反没关系)   </br>
ii.	(function(){}).call() 不推荐                                             </br>
iii.	 xxx                                                                 </br>
iv.	 (function(){}).call() 报错                                              </br>
v.	frank192837192463981273912873098127912378.call() 不推荐   

2.	如何使用闭包                                                              </br>
(1) 立即执行函数使得 person 无法被外部访问                                     </br>
(2)	闭包使得匿名函数可以操作 person                                            </br>
(3)	window.frankGrowUp 保存了匿名函数的地址                                   </br>
(4)	任何地方都可以使用 window.frankGrowUp                                     </br>
=> 任何地方都可以使用 window.frankGrowUp 操作 person，但是不能直接访问 person   </br>

五  this

1.  
```javascript
button.onclick = function f1(){
    console.log(this) 
}       // 触发事件的元素  button

button.onclick.call({name: 'xx'}) //button

button.addEventListener('click', function(){
    console.log(this) 
}       // 该元素的引用 button

$('ul').on('click', 'li' /*selector*/, function(){
    console.log(this) 
})          //this 则代表了与 selector 相匹配的元素 li 元素

```

2.  使用function定义的函数，this的指向随着调用环境的变化而变化的，而箭头函数中的this指向是固定不变的，一直指向的是定义函数的环境。

3.  
```javascript
function X(){
    return object = {
        name: 'object',
        options: null,
        f1(x){
            this.options = x
            this.f2()
        },
        f2(){
            this.options.f2.call(this)
        }
    }
}

var options = {
    name: 'options',
    f1(){},
    f2(){
        console.log(this) // this 是 onject
    }
}

var x = X()
x.f1(options)

```

六 new

1.  
```javascript
function 士兵(ID){
    //var temp = {}
    //this = temp
    //士兵.prototype = { constructor:士兵 }
    //this.__proto__ = 士兵.prototype
    
    this.ID = ID
    this.生命值 = 42   //自有属性 
  
    //return this
}

create士兵.prototype = {        //共有属性
  constructor:士兵，
  兵种:"美国大兵",
  攻击力:5,
  行走:function(){ /*######*/ }，
  奔跑:function(){ /*######*/ },
  死亡:function(){ /*######*/ },
  攻击:function(){ /*######*/ },
  防御:function(){ /*######*/ }
}
```

2.  var object = new Object()                                               </br>
    自有属性 空                                                              </br>
    object.proto === Object.prototype                                       </br>
    
    var array = new Array('a','b','c')                                      </br>
    自有属性 0:'a' 1:'b' 2:'c',length:3                                      </br>
    array.proto === Array.prototype                                         </br>
    Array.prototype.proto === Object.prototype                              </br>
    
    var fn = new Function('x', 'y', 'return x+y')                           </br>
    自有属性 length:2, 不可见的函数体: 'return x+y'                           </br>
    fn.proto === Function.prototype                                         </br> 
    
    Array is a function                                                     </br>
    Array = function(){...}                                                 </br>
    Array.proto === Function.prototype                                      </br>

七 Cookie

1.  服务器通过 Set-Cookie 响应头设置 Cookie
2.	浏览器得到 Cookie 之后，每次请求都要带上 Cookie
3.	服务器读取 Cookie 就知道登录用户的信息（email）
4.  在 Chrome 登录了得到 Cookie，用 Safari 访问，Safari 不会带上 Cookie 
5.  Cookie会被用户篡改（Session 来解决这个问题，防止用户篡改）
6.  Cookie 默认在用户关闭界面后失效（后台可以设置），通常大小为 4KB

八 Session

1.  将 SessionId（随机数）通过 Cookie 发给客户端
2.  客户端访问服务器时，服务器读取 SessionId 
3.  服务器中有一块内存（哈希表）保存了所有 Session
4.  通过 SessionId 我们可以得到对应用户的隐私信息（ID，Email）
5.  这块内存就是服务器上的 Session

九 localStorage

1.  localStorage 与 HTTP 无关
2.  HTTP 不会带上 localStorage 的值
3.  只有相同域名的页面才能互相读取 localStorage （没有同源那么严格）
4.  每个域名 localStorage 最大储存量为 5MB 左右
5.  常用场景：记录有没有提示过用户
6.  localStorage 永久有效，除非清理缓存

十 SessionStroage

1.  1,2,3,4 同上
2.  SessionStroage 在用户关闭界面（会话结束）后失效

十一 Cache-Control

1.  chrome 先 server 发请求，server 返回文本的同时，还有响应头 max-age
2.  在设置的时间内刷新页面（请求同样的 URL ），
3.  chrome 不会先 server 发请求，直接在内存中返回
4.  如果 js,css 改变，可以添加查询参数请求新的 

十二 手机调试方法

1.  手机电脑连接到同一wifi下，启动http-server
2.  因为手机上不能像在网页上一样直接使用console.log进行调试，（无法打开控制台）
3.  使用 alter() 与 onerrow 结合使用
```javascript
window.onerror = function(message,file,row) {
    alert(message)
    alert(file)
    alert(row)
}
```
4.  自己写一个控制台，再结合 onerrow 也可以直接安装腾讯的vConsole使用
```javascript
<div id="consoleOutput" style="position:fixed;width:100%;left:0;bottom:0;height:100px;border:1px solid black;background:red;overflow: auto;">
</div>
<script>
    window.console = {
        log(x) {
            let p = document.createElement('p')
            p.innerText = x
            consoleOutput.appendChild(p)
        }
    }
</script>
```

十三 面试题 html

1.	（必考） 你是如何理解 HTML 语义化的？
    <pre>
    第一种:
    举例，段落用 p，边栏用 aside，主要内容用 main 标签
    第二种:
    最开始是 PHP 后端写 HTML，不会 CSS，于是就用 table 来布局。table 使用展示表格的。严重违反了 HTML 语义化。
    后来有了专门的写 CSS 的前端，他们会使用 DIV + CSS 布局，主要是用 float 和绝对定位布局。稍微符合了 HTML 语义化。
    再后来，前端专业化，知道 HTML 的各个标签的用法，于是会使用恰当的标签来展示内容，而不是傻傻的全用 div，会尽量使用 h1、ul、p、main、header 等标签
    语义化的好处是已读、有利于SEO等。
    参考 https://zhuanlan.zhihu.com/p/32570423
    </pre>

2.	meta viewport 是做什么用的，怎么写？
    ```html
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    // 控制页面在移动端不要缩小显示
    ```
    <pre>
    一开始，所有页面都是给PC准备的，乔布斯推出 iPhone 3GS，页面是不适应手机屏幕的，所以乔布斯的工程师想了一个办法，默认把手机模拟成 980px，页面缩小。
    后来，智能手机普及，这个功能在部分网站不需要了，所以我们就用 meta:vp 让手机不要缩小我的网页。
    </pre>

3.	canvas 元素是干什么的？

十四 面试题 css

1.	（必考） 说说盒模型。
	<pre>
    举例：
    box-sizing: content-box: width == 内容区宽度
    box-sizing: border-box: width == 内容区宽度 + padding 宽度 + border 宽度
    </pre>

2.	css reset 和 normalize.css 有什么区别？
    <pre>
    reset 重置，之前的样式我不要，a{color: red;}，抛弃默认样式
    normalize 让所有浏览器的标签都跟标准规定的默认样式一致，各浏览器上的标签默认样式基本统一。
    </pre>

3.	（必考）如何居中？
    <pre>
    水平居中：
    内联：爸爸身上写 text-align:center;
    块级：margin-left: auto; margin-right: auto;

    垂直居中： https://jscode.me/t/topic/1936
    </pre>

4.	选择器优先级如何确定？
    <pre>
    选择器越具体，优先级越高。 #xxx 大于 .yyy
    同样优先级，写在后面的覆盖前面的。
	color: red !important; 优先级最高。
    </pre>

5.	BFC 是什么？
    <pre>
    overflow:hidden 清除浮动。（推荐用 .clearfix 清除浮动）
    overflow:hidden 取消父子 margin 合并。（推荐用 padding-top: 1px;）
    </pre>

6.	如何清除浮动？
    <pre>
    overflow: hidden （不推荐）
    .clearfix 清除浮动写在爸爸身上
    </pre>
    ```css
    .clearfix::after{
	    content: ''; display: block; clear:both;
    }
    ```

十五 面试题 js

1.	JS 有哪些数据类型？
    string number bool undefined null object symbol
    object 包括了数组、函数、正则、日期等对象
    一旦出现（数组、函数、正则、日期、NaN）直接0分

2.	（必考） Promise 怎么使用？
    <pre>
    then
    $.ajax(...).then(成功函数, 失败函数)
	
    链式 then
    $.ajax(...).then(成功函数, 失败函数).then(成功函数2, 失败函数2)
    
    如何自己生成 Promise 对象
    </pre>
    ```javascript
        function xxx(){
            return new Promise(function(resolve, reject){
                setTimeout(()=>{
                    resolve() 或者 reject()
                },3000)
            })
        }
        xxx().then(...)
    ```

3.	（必考） AJAX 手写一下？
    ```javascript
        let xhr = new XmlHttpRequest()
        xhr.open('POST','/xxx')
        xhr.onreadystatechange = ()=>{
            if(xhr.readystate === 4 && xhr.status === 200){
                 console.log(xhr.responseText)      
            }
        }
        xhr.send('a=1&b=2')
    ```

4.	（必考）闭包是什么？
    ```javascript
    function Adder (){
        var n = 0
        return function(){
            n += 1
        }
    }
    let  adder = Adder()
    adder() // n === 1
    adder() // n === 2
    console.log(n) // n is undefined
    ```
    正确参考：https://zhuanlan.zhihu.com/p/22486908

5.  （必考）这段代码里的 this 是什么？
    <pre>
    function() 里面的 this 就是 window
    function() 是 strict mode，this 就是 undefined
    a.b.c.function() 里面的 this 就是 a.b.c
    new Function() 里面的 this 就是新生成的实例
    () => console.log(this) 里面 this 跟外面的 this 的值一模一样
    
    正确参考：https://zhuanlan.zhihu.com/p/23804247
    使用function定义的函数，this的指向随着调用环境的变化而变化的，
    而箭头函数中的this指向是固定不变的，一直指向的是定义函数的环境。
    </pre>

6.  必考）什么是立即执行函数？使用立即执行函数的目的是什么？
    ```javascript
    ;(function(){
        var xx
    }())
    ;(function(){
        var xx
    })()
    !function(){
        var xx
    }()
    ~function(){
        var xx
    }()
    ```
    造出一个函数作用域，防止污染全局变量
    ```javascript
    {
        let  name
    }

    ```

7.	async/await 语法了解吗？目的是什么？
    ```javascript
    function resolveAfter2Seconds() {
        return new Promise(resolve => {
            setTimeout(() => {
                resolve('resolved')
            }, 2000)
        })
    }
    async function asyncCall() {
        console.log('calling')
        const result = await resolveAfter2Seconds()
        console.log(result)
        // expected output: 'resolved'
    }
    asyncCall();
    ```
    把异步代码写成同步代码。

8.  如何实现深拷贝？
    <pre>
    JSON 深拷贝
    缺点：JSON 不支持函数、引用、undefined、RegExp、Date……
    </pre>
    ```javascript
    let a = {...}
    let b = JSON.parse(JSON.stringify(a))
    ```
    <pre>
    递归拷贝
    </pre>
    ```javascript
    function copy(obj){
        let newobj = null;      //声明一个变量用来储存拷贝之后的内容

        if(typeof(obj) == 'object' && obj !== null){
            //判断数据类型是否是复杂类型，如果是则调用自己，再次循环，如果不是，直接赋值即可，
            //由于null不可以循环但类型又是object，所以这个需要对null进行判断
        
            newobj = obj instanceof Array? [] : {};   
            //声明一个变量用以储存拷贝出来的值,根据参数的具体数据类型声明不同的类型来储存
            
	        //循环obj 中的每一项，如果里面还有复杂数据类型，则直接利用递归再次调用copy函数
            for(var i in obj){  
                newobj[i] = copy(obj[i])
            }
        }else{
            newobj = obj
        }    
        
        return newobj;    //函数必须有返回值，否则结构为undefined
   }

    ```

9.  如何实现数组去重？
    计数排序的逻辑（只能正整数）
    ```javascript
    let a = [4,2,5,6,3,4,5]
    let hash = {}
    for(let i=0;i<a.length;i++){
        if(a[i] in hash){
            //
        }else{
            hashTab[ a[i] ] = true
        }
    }
    //hash: {4: true, 2: true, 5: true, 6:true, 3: true}
    console.log(Object.keys(hash))

    function unique2(array){ 
    var newArray = []
    array.forEach((x,y)=>{
    if(!(array[y] in newArray)) {
    newArray.push(x)
    }
    })
    return newArray
    }

    let mySet = new Set([1,5,2,3,4,2,3,1,3,4])
    function unique3() {
    let a = []
    mySet.forEach((x)=>{a.push(x)}) 
    return a
    }

    ```
    Set去重
    ```javascript
    Array.from(new Set(a))
    ```

10.	如何用正则实现 string.trim() ？
    ```javascript
    function trim(string){
        return string.replace(/^\s+|\s+$/g, '')
    }
    ```

11. js原型是什么
    <pre>
    var a = [1,2,3]
    a 只有0、1、2、length 4 个key
    为什么可以 a.push(4) ，push 是哪来的？
    a.__proto__ === Array.prototype
    push 就是沿着 a.__proto__ 找到的，也就是 Array.prototype.push
    Array.prototype 还有很多方法，如 join、pop、slice、splice
    Array.prototype 就是 a 的原型（proto）
    
    参考：https://zhuanlan.zhihu.com/p/23090041
    </pre>

12.	ES 6 中的 class 了解吗？
    ```javascript
    class Rectangle {
        // constructor
        constructor(height, width) {
            this.height = height;
            this.width = width;
        }
        // Getter
        get area() {
            return this.calcArea()
        }
        // Method
        calcArea() {
            return this.height * this.width;
        }
    }
    const square = new Rectangle(10, 10);

    console.log(square.area); // 100
    ```

13.	JS 如何实现继承？
    原型链
    ```javascript
    function Animal(){
        this.body = '重量'
    }
    Animal.prototype.move = function(){ }

    function Human(name){
        Animal.apply(this,arguments)
        this.name = name
    }

    // Human.prototype.__proto__ = Animal.prototype // 非法
    var fn = function(){}
    fn.prototype = Animal.prototype
    Human.prototype = new fn()

    Human.prototype.useTools = function(){}
     var xiaoming = new Human()
    ```
    extends关键字
    ```javascript
    class Animal{
        constructor(){
            this.body = '重量'
        }
        move(){}
    }

    class Human extends Animal{
        constructor(name){
            super()
            this.name = name
        }
        useTools(){}
    }

    var xiaoming = new Human()
    ```