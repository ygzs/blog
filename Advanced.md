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

十三 正则

1.  <table>
    <tr>
    <th>元字符</th>
    <th>描述</th>
    </tr>
    <tr><td>.</td><td>匹配任意单个字符除了换行符</td></tr>
    <tr><td>[ ]</td><td>字符种类.匹配方括号内的任意字符</td></tr>
    <tr><td>[^ ]</td><td>否定字符类.匹配除了方括号里的任意字符</td></tr>
    <tr><td>*</td><td>匹配>=0个重复的在*号之前的字符</td></tr>
    <tr><td>+</td><td>匹配>=1个重复的+号前的字符</td></tr>
    <tr><td>?</td><td>匹配前面一个表达式0次或者1次</td></tr>
    <tr><td>{n,m}</td><td>匹配前面的字符至少n次，最多m次</td></tr>
    <tr><td>(xyz)</td><td>字符集，匹配与 xyz 完全相等的字符串</td></tr>
    <tr><td>|</td><td>或运算符，匹配符号前或后的字符</td></tr>
    <tr><td>\</td><td>转义字符,用于匹配一些保留的字符</td></tr>
    <tr><td>^</td><td>从开始行开始匹配
    例如，/^A/ 并不会匹配 "an A" 中的 'A'，但是会匹配 "An E" 中的 'A'</td></tr>
    <tr><td>$</td><td>从末端开始匹配
    例如，/t$/ 并不会匹配 "eater" 中的 't'，但是会匹配 "eat" 中的 't'</td></tr>
    </table>

2. <pre>
        "*?"  重复任意次，但尽可能少重复 
        如 "acbacb"  正则  "a.*?b" 只会取到第一个"acb" 原本可以全部取到但加了限定符后，只会匹配尽可能少的字符 ，而"acbacb"最少字符的结果就是"acb" 

    　　"+?"  重复1次或更多次，但尽可能少重复，与上面一样，只是至少要重复1次

    　　"??"  重复0次或1次，但尽可能少重复
        如 "aaacb" 正则 "a.??b" 只会取到最后的三个字符"acb"

    　　"{n,m}?"  重复n到m次，但尽可能少重复
        如 "aaaaaaaa"  正则 "a{0,m}" 因为最少是0次所以取到结果为空

    　　"{n,}?"  重复n次以上，但尽可能少重复
        如 "aaaaaaa"  正则 "a{1,}" 最少是1次所以取到结果为 "a"
    </pre>  

3.  <pre>
    "(exp)"    匹配exp,并捕获文本到自动命名的组里  
    "(?<name>exp)"     匹配exp,并捕获文本到名称为name的组里
    "(?:exp)"   匹配exp,不捕获匹配的文本，也不给此分组分配组号
    x(?=y)      匹配'x'仅仅当'x'后面跟着'y'.这种叫做先行断言。
    (?<=y)x     匹配'x'仅当'x'前面是'y'.这种叫做后行断言。
    x(?!y)      仅仅当'x'后面不跟着'y'时匹配'x'，这被称为正向否定查找。
    (?<!y)x     仅仅当'x'前面不是'y'时匹配'x'，这被称为反向否定查找。
    </pre> 

4.  参考：https://github.com/ziishaned/learn-regex/blob/master/translations/README-cn.md

