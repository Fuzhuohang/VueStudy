# 基础介绍
## 什么是Vue.js
* Vue 是一套用于构建用户界面的**渐进式框架**。  
* 与其他大型框架不同的是，Vue 被设计为**可以自底向上**的**逐层式应用**。  

## 准备工作
* 在项目中使用vue.js的方法有很多，例如通过&lt;script&gt;使用本地URL或者网络工具库URL地址、通过npm安装、或者使用Vue CLI命令行工具来进行安装。  
* ***ps1：在初学 Vue 时，不推荐直接使用 Vue-cli，尤其是在对基于Node.js的构建工具不熟悉的时候。***  
* ***ps2：在开发环境中最好使用开发版本而不要去使用压缩后的生产版本，否则将失去开发版本中所有常见错误相关的警告。***  

## 声明式渲染
* Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进DOM的系统 [示例：Hello Vue!](../../src/html/01_03_Vue_DeclarativeRendering.html/#app-01)  
```html
<div id="app">
    {{ message }}
</div>
```  
```Javascript
var app = new Vue({
    el: '#app',
    data:{
        message: 'Hello Vue!'
    }
})
```  
* 页面数据看似是直接渲染在页面当中，但实际上现在的数据是通过 Vue 与 DOM 建立了关联性，作用的数据都是**响应式的**，我们可以通过 JavaScript 控制台修改相关的属性值，页面上的展示数据也会响应的发生变化。 
* Vue 应用实例不仅可以绑定文本插值，也可以绑定元素的 attribute [示例：Vue实例绑定元素属性](../../src/html/01_03_Vue_DeclarativeRendering.html/#app-02)
```html
<div id="app-2">
    <span v-bind:title="message">
        鼠标停留几秒钟查看此处动态绑定的提示信息！
    </span>
</div>
```
```javascript
var app2 = new Vue({
    el: '#app-2',
    data: {
        message: '页面加载于 ' + new Date().toLocaleString()
    }
})
```  
* Vue 指令：Vue 指令带有 “v-” 前缀，以表示它们是 Vue 提供的特殊 attribute，例如上例中用到的 v-bind。Vue 指令会在渲染的DOM上应用特殊的响应式行为。在上例中，v-bind 指令的意思是：“将这个元素节点的 ‘title’ 属性和 Vue 实例的 ‘message’ 值保持一致”。  

## 条件与循环
* Vue 指令在开发过程中非常常见，例如用来自如控制一个元素是否显示的v-if 指令 [示例：v-if 指令控制元素显示](../../src/html/01_04_Vue_Condition&Loop.html/#app-03)
```html
<div id="app-3">
    <p v-if="seen">现在你可以看到我了</p>
</div>
```
```javascript
var app3 = new Vue({
    el: '#app-3',
    data: {
        seen: true,
    }
})
```
* 从上面的例子中，可以看出，通过Vue 实例，我们不仅能够将数据绑定到 DOM 文本或者 DOM 元素属性，还可以将数据绑定到 DOM 的文本结构当中。  
* 此外，Vue 还提供了一个强大的过渡效果系统，可以在 Vue 插入/更新/移除元素时自动应用过度效果。  
* 除了v-if指令常用来控制元素显示以外，v-for 指令也常被用来对一个项目列表进行渲染 [示例：v-for 指令渲染项目列表](../../src/html/01_04_Vue_Condition&Loop.html/#app-04)  
```html
<div id="app-4">
    <ol>
        <li v-for="todo in todos">
            {{ todo.text }}
        </li>
    </ol>
</div>
```
```javascript
var app4 = new Vue({
    el: '#app-4',
    data: {
        todos: [
            { text: '学习 JavaScript' },
            { text: '学习 Vue' },
            { text: '整个牛项目' }
        ]
    }
})
```  

## 处理用户输入
* 我们可以通过 v-on 指令为元素添加一个事件监听器，来调用定义在 Vue 实例中的方法。[示例：v-on 指令绑定字符串反转事件](../../src/html/01_05_Vue_UserInteraction.html/#app-05)
```html
<div id="app-5">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">反转消息</button>
</div>
```
```javascript
var app5 = new Vue({
    el: '#app-5',
    data: {
        message: 'Hello Vue.js'
    },
    methods: {
        reverseMessage: function() {
            this.message = this.message.split(' ').reverse().join(' ')
        }
    }
})
```
* 除了 v-on 指令外，Vue 还提供了 v-model 指令，它可以轻松的实现表单输入和应用状态之间的双向绑定。[示例：v-model 指令实现输入框内容和展示内容的同步](../../src/html/01_05_Vue_UserInteraction.html/#app-06)
```html
<div id="app-6">
    <p>{{ message }}</p>
    <input v-model="message">
</div>
```
```javascript
var app6 = new Vue({
    el: '#app-6',
    data: {
        message: 'Hello Vue!'
    }
})
```