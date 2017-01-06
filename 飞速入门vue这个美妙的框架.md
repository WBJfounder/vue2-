#期待中飞翔的vue.js

##首先是介绍vuejs
在夸赞vue之前要提醒大家一下那就是兼容性
Vue.js 不支持 IE8 及其以下版本，因为 Vue.js 使用了 IE8 不能实现的 ECMAScript 5 特性。 
Vue.js支持所有兼容ECMAScript5的浏览器（我会在图片资料告诉大家兼容ECMAScript5的浏览器有哪些）

###vue.js是什么
vue.js是一套构建用户界面的渐进式框架。与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。
（不理解上面的渐进式框架和自底向上增量开发？对吧宝贝！其实呢就是一种思想和开发模式也是vue的优点：
 就是vue框架不会限制你的开发，你可以在页面的一部分当成jq类库似的使用vue，或者整个页面都用vue重构）
Vue 的核心库只关注视图层，并且非常容易学习，非常容易与其它库或已有项目整合。
另一方面，Vue 完全有能力驱动采用单文件组件和Vue生态系统支持的库开发的复杂单页应用。
Vue.js 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件

### vueJS的目的：
1.解决数据绑定的问题
2.vue框架产生的主要目的是为了开发大型单页面应用
3.它还支持组件化，也就是可以将页面封装成若干个组件，采用积木式编程，这样使页面复用性达到最高（支持组件化）

###VueJS的特性：
1.MVVM模式（我已经在写angular的时候说过MVVM模式了我的github上呢https://github.com/WBJfounder/AngularJS-）
 使用MVVM模式有几大好处：
　　1. 低耦合。View可以独立于Model变化和修改，一个ViewModel可以绑定到不同的View上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。
　　2. 可重用性。可以把一些视图的逻辑放在ViewModel里面，让很多View重用这段视图逻辑。
　　3. 独立开发。开发人员可以专注与业务逻辑和数据的开发(ViewModel)。设计人员可以专注于界面(View)的设计。
　　4. 可测试性。可以针对ViewModel来对界面(View)进行测试

2.组件化
3.指令系统
4.vue2.0版本开始支持虚拟dom
（下面都会提到,别急）

##步入vue.js（前面那么多铺垫终于开始了）

###安装vuejs（我装好了大家直接用就行）
我的下载方式是  $ npm install vue （或者用bower下啊 或者github上下载，开发版的提示友好）

###初入vue，想起了好多技术的第一手代码（Hello World）
1.数据绑定
  <div id="app">
        {{message}}
    </div>
    <script src="vue.min.js"></script>
    <script>
    //好多人vue模块报错在这一定注意new Vue  V大写
        new Vue({
            el:'#app',
            data:{
                message:'Hello World!'
            }
        })
    </script>

2.数据的双向绑定(比angular的简单多了省代码啊)
  <div id="app">
        <p>{{message}}</p>
        <input placeholder="请输入内容" autofocus="autofocus" v-model="message">
    </div>
    <script src="vue.min.js"></script>
    <script>
        new Vue({
            el:'#app',
            data:{
                message:''
            }
        })
    </script>    

3.绑定属性利用了vue中的v-bind:属性名='message'
  <div id="app-2">
      <span v-bind:title="message">
          Hover your mouse over me for a few seconds to see my dynamically bound title!
      </span>
  </div>
    <script src="vue.min.js"></script>
    <script>    
        var app2 = new Vue({
             el:'#app-2',
             data:{
                 message:'你是我的小呀小苹果'+ new Date()
             }   
        })
    </script>
    我没事干又尝试下绑定style属性也是可以的哦但是注意不能直接写width：100px会报错
    
     <div id="app-2">
      <div v-bind:style="message">
          Hover your mouse over me for a few seconds to see my dynamically bound title!
      </div>
  </div>
    <script src="vue.min.js"></script>
    <script>    
        var app2 = new Vue({
             el:'#app-2',
             data:{
                 message:{
                   //这样写才行拼个单位这可是官网没有的自己闲的
                     width:100+'px',   
                     background:'red'
                 }
             }   
        })
    </script>

4.条件：v-if
 <div id="app-3">
        <p v-if="see">你能看到我</p>
    </div>
    <script src="vue.min.js"></script>
    <script>
        var app3 = new Vue({
            el:'#app-3',
            data:{
                //改变see后面为true就能看到跟angular很像哦
                see:false
                //或者拿它用来做判断做一些事情也是可以的
                //see:alert(1)
            }
        })
    </script>  

 5.循环：v-for 是不是觉得都和angular很像呢
      <div id="app-4">
        <ol>
            <li v-for="w in wbj" id="d">
                {{w.text}}
            </li>
        </ol>
    </div>
    <script src="vue.min.js"></script>
    <script>
        var app4 = new Vue({
            el:'#app-4',
            data:{
                wbj:[
                    {text:'人工弹幕'},
                    {text:'哈哈哈哈'},
                    {text:'人工'}
                ]
            }
        })
    </script>   

6.处理用户输入：v-on  或者@ 代替 v-on
     <div id="app-5">
        <p>{{message}}</p>
        <!--<button v-on:click="reverseMessage">我会翻转</button>-->
        <button @click="reverseMessage">我会翻转</button>
    </div>
    <script src="vue.min.js"></script>
    <script>
        var app5 = new Vue({
            el:'#app-5',
            data:{
                message:'人工弹幕',
            },
            methods:{
                reverseMessage:function(){
                    this.message = this.message.split('').reverse().join('')
                }
            }
        })
    </script>
 在 reverseMessage 方法中，我们在没有接触 DOM 的情况下更新了应用的状态 - 所有的 DOM 操作都由 Vue 来处理，
 你写的代码只需要关注基本逻辑。

 7.用组建构建（应用）先看下后面有专业组件化详细讲解
  7.1先简单体会一下
      <div id="app">
        <ol>
            <todo-item></todo-item>
        </ol>
    </div>
    <script src="vue.min.js"></script>
    <script>
    //先定义注册再 渲染
        Vue.component('todo-item',{
            template:'<li>简单的体验</li>'
        })
         new Vue({
            el:'#app'
        })
    </script>
    7.2 props用于父组件向子组件传递数据。
        <div id="app">
        <ol>
            <todo-item v-for="item in lists" v-bind:todo="item"></todo-item>
        </ol>
        <div>
            <todo-item v-for="item in lists" v-bind:todo="item"></todo-item>
        </div>
    </div>
    <script src="vue.min.js"></script>
    <script>
      //先定义注册再 渲染
        Vue.component('todo-item',{
            props:['todo'],
            template:'<li>{{todo.text}}</li>'
        })
         new Vue({
            el:'#app',
            data:{
                lists:[
                    {text:'人工弹幕'},
                    {text:'工弹幕'},
                    {text:'弹幕'}
                ]
            }
        })
    </script>

##上面介绍完了vue的一些概念那么下面就开始说点技术的
###Vue实例 
1.构造器
每个Vue.js应用都是通过构造函数Vue创建一个Vue的根实例启动的 ：
 var vm = new Vue({
     //选项
 })
 在实例化 Vue 时，需要传入一个选项对象，它可以包含数据、模板、挂载元素、方法、生命周期钩子等选项。
 全部的选项可以在 API 文档中查看。 
 可以扩展 Vue 构造器，从而用预定义选项创建可复用的组件构造器：（这里就是为了让你知道所有Vue.js组件其实都是被扩展的Vue实例）
 var MyComponent = Vue.extend({
  // 扩展选项
})
// 所有的 `MyComponent` 实例都将以预定义的扩展选项被创建
var myComponentInstance = new MyComponent() 

2.属性与方法
每个 Vue 实例都会代理其 data 对象里所有的属性：
 <script>        
        var data = { a: 1 }
        var vm = new Vue({
        data: data
        })
        console.log(vm.a)
        vm.a === data.a // -> true
        // 设置属性也会影响到原始数据
        vm.a = 2
        data.a // -> 2
        // ... 反之亦然
        data.a = 3
        vm.a // -> 3        
    </script>
    注意只有这些被代理的属性是响应的。如果在实例创建之后添加新的属性到实例上，它不会触发视图更新。
    我们将在后面详细讨论响应系统。

    除了 data 属性， Vue 实例暴露了一些有用的实例属性与方法。
    这些属性与方法都有前缀 $，以便与代理的 data 属性区分。例如：
    <script>
        var data = {
            a: 1
        }
        var vm = new Vue({
            el: '#example',
            data: data
        })
        vm.$data === data // -> true
        //记住这个获取省事哦
        vm.$el === document.getElementById('example') // -> true
            // $watch 是一个实例方法
            //注意不要在这里乱用箭头函数（因为this指向不同)
        vm.$watch('a', function (newVal, oldVal) {
            // 这个回调将在 `vm.a`  改变后调用
        })
    </script>

3.实例的生命周期
  每个 Vue 实例在被创建之前都要经过一系列的初始化过程。例如，实例需要配置数据观测(data observer)、编译模版、挂载实例到 DOM ，然后在数据变化时更新 DOM 。
  在这个过程中，实例也会调用一些 生命周期钩子 ，这就给我们提供了执行自定义逻辑的机会。例如，created 这个钩子在实例被创建之后被调用：  
  var vm = new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// -> "a is: 1"
也有一些其它的钩子，在实例生命周期的不同阶段调用，如 mounted、 updated 、destroyed 。
钩子的 this 指向调用它的 Vue 实例。一些用户可能会问 Vue.js 是否有“控制器”的概念？答案是，没有。组件的自定义逻辑可以分布在这些钩子中。
##模板语法
Vue.js 使用了基于 HTML 的模版语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML ，所以能被遵循规范的浏览器和 HTML 解析器解析。
在底层的实现上， Vue 将模板编译成虚拟 DOM 渲染函数。结合响应系统，在应用状态改变时， Vue 能够智能地计算出重新渲染组件的最小代价并应用到 DOM 操作上。
如果你熟悉虚拟 DOM 并且偏爱 JavaScript 的原始力量，你也可以不用模板，直接写渲染（render）函数，使用可选的 JSX 语法。
###插值
1.文本
数据绑定最常见的形式就是使用 “Mustache” 语法（双大括号）的文本插值：
<span>Message:{{msg}}</span>
Mustache 标签将会被替代为对应数据对象上 msg 属性的值。
无论何时，绑定的数据对象上 msg 属性发生了改变，插值处的内容都会更新。
通过使用 v-once 指令，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。
但请留心这会影响到该节点上所有的数据绑定：
<span v-once>This will never change: {{ msg }}</span>

2.纯HTML(不建议用)
双大括号会将数据解释为纯文本 ，而非HTML。为了输出真正的HTML，你需要使用v-html指令：
<div v-html="rawHtml"></div>

3.属性
Mustache 不能在 HTML 属性中使用，应使用 v-bind 指令：
<div v-bind:id="dynamicId"></div>

4.使用 JavaScript 表达式
迄今为止，在我们的模板中，我们一直都只绑定简单的属性键值。但实际上，对于所有的数据绑定， Vue.js 都提供了完全的 JavaScript 表达式支持。
{{ number + 1 }}
{{ ok ? 'YES' : 'NO' }}
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id"></div>
这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含单个表达式，所以下面的例子都不会生效。
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}
<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
注意：模板表达式都被放在沙盒中，只能访问全局变量的一个白名单，如 Math 和 Date 。
你不应该在模板表达式中试图访问用户定义的全局变量。

5.指令
指令（Directives）是带有 v- 前缀的特殊属性。指令属性的值预期是单一 JavaScript 表达式（除了 v-for，之后再讨论）。指令的职责就是当其表达式的值改变时相应地将某些行为应用到 DOM 上。让我们回顾一下在介绍里的例子：
<p v-if="seen">Now you see me</p>
这里， v-if 指令将根据表达式 seen 的值的真假来移除/插入 <p> 元素。

6.参数
一些指令能接受一个“参数”，在指令后以冒号指明。例如， v-bind 指令被用来响应地更新 HTML 属性：
<a v-bind:href="url"></a>
在这里 href 是参数，告知 v-bind 指令将该元素的 href 属性与表达式 url 的值绑定。
另一个例子是 v-on 指令，它用于监听 DOM 事件：
<a v-on:click="doSomething">
在这里参数是监听的事件名。我们也会更详细地讨论事件处理。

7.修饰符
修饰符（Modifiers）是以半角句号 . 指明的特殊后缀，用于指出一个指定应该以特殊方式绑定。例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()：
<form v-on:submit.prevent="onSubmit"></form>
之后当我们更深入地了解 v-on 与 v-model时，会看到更多修饰符的使用。

8.过滤器
Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。过滤器应该被添加在 mustache 插值的尾部，由“管道符”指示：
{{ message | capitalize }}
<!-- in mustaches -->
{{ message | capitalize }}
<!-- in v-bind -->
<div v-bind:id="rawId | formatId"></div>
注意：Vue 2.x 中，过滤器只能在 mustache 绑定和 v-bind 表达式（从 2.1.0 开始支持）中使用，因为过滤器设计目的就是用于文本转换。
为了在其他指令中实现更复杂的数据变换，你应该使用计算属性。
过滤器函数总接受表达式的值作为第一个参数。
new Vue({
  // ...
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
过滤器可以串联：
{{ message | filterA | filterB }}
过滤器是 JavaScript 函数，因此可以接受参数：
{{ message | filterA('arg1', arg2) }}
这里，字符串 'arg1' 将传给过滤器作为第二个参数， arg2 表达式的值将被求值然后传给过滤器作为第三个参数。

9.缩写
v- 前缀在模板中是作为一个标示 Vue 特殊属性的明显标识。当你使用 Vue.js 为现有的标记添加动态行为时，它会很有用，但对于一些经常使用的指令来说有点繁琐。
同时，当搭建 Vue.js 管理所有模板的 SPA 时，v- 前缀也变得没那么重要了。因此，Vue.js 为两个最为常用的指令提供了特别的缩写：
v-bind 缩写

<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
v-on 缩写

<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
它们看起来可能与普通的 HTML 略有不同，但 : 与 @ 对于属性名来说都是合法字符，在所有支持 Vue.js 的浏览器都能被正确地解析。而且，它们不会出现在最终渲染的标记。
缩写语法是完全可选的，但随着你更深入地了解它们的作用，你会庆幸拥有它们。

##计算属性
在模板中绑定表达式是非常便利的，但是它们实际上只用于简单的操作。在模板中放入太多的逻辑会让模板过重且难以维护。例如：
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
在这种情况下，模板不再简单和清晰。在实现反向显示 message 之前，你应该确认它。这个问题在你不止一次反向显示 message 的时候变得更加糟糕。
这就是为什么任何复杂逻辑，你都应当使用计算属性。

1.基础例子
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // a computed getter
    reversedMessage: function () {
      // `this` points to the vm instance
      return this.message.split('').reverse().join('')
    }
  }
})
这里我们声明了一个计算属性 reversedMessage 。我们提供的函数将用作属性 vm.reversedMessage 的 getter 。
console.log(vm.reversedMessage) // -> 'olleH'
vm.message = 'Goodbye'
console.log(vm.reversedMessage) // -> 'eybdooG'
你可以打开浏览器的控制台，修改 vm 。 vm.reversedMessage 的值始终取决于 vm.message 的值。
你可以像绑定普通属性一样在模板中绑定计算属性。 Vue 知道 vm.reversedMessage 依赖于 vm.message ，因此当 vm.message 发生改变时，依赖于 vm.reversedMessage 的绑定也会更新。
而且最妙的是我们是声明式地创建这种依赖关系：计算属性的 getter 是干净无副作用的，因此也是易于测试和理解的。

2.计算缓存
