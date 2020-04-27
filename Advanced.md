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

十二 面试题

1.	（必考） 你是如何理解 HTML 语义化的？
第一种举例，段落用 p，边栏用 aside，主要内容用 main 标签
第二种
2.	 最开始是 PHP 后端写 HTML，不会 CSS，于是就用 table 来布局。table 使用展示表格的。严重违反了 HTML 语义化。
3.	 后来有了专门的写 CSS 的前端，他们会使用 DIV + CSS 布局，主要是用 float 和绝对定位布局。稍微符合了 HTML 语义化。
4.	 再后来，前端专业化，知道 HTML 的各个标签的用法，于是会使用恰当的标签来展示内容，而不是傻傻的全用 div，会尽量使用 h1、ul、p、main、header 等标签
5.	 语义化的好处是已读、有利于SEO等。
第三种：对面试官说请看我的博客 https://zhuanlan.zhihu.com/p/32570423
6.	meta viewport 是做什么用的，怎么写？
死背： <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
控制页面在移动端不要缩小显示。
侃侃而谈
7.	 一开始，所有页面都是给PC准备的，乔布斯推出 iPhone 3GS，页面是不适应手机屏幕的，所以乔布斯的工程师想了一个办法，默认把手机模拟成 980px，页面缩小。
8.	 后来，智能手机普及，这个功能在部分网站不需要了，所以我们就用 meta:vp 让手机不要缩小我的网页。
9.	canvas 元素是干什么的？
项目丢给他。
看 MDN 的 canvas 入门手册。
