# 1 基础介绍
## 1.1 什么是Vue.js
* Vue 是一套用于构建用户界面的**渐进式框架**。  
* 与其他大型框架不同的是，Vue 被设计为**可以自底向上**的**逐层式应用**。  

## 1.2 准备工作
* 在项目中使用vue.js的方法有很多，例如通过&lt;script&gt;使用本地URL或者网络工具库URL地址、通过npm安装、或者使用Vue CLI命令行工具来进行安装。  
* ***ps1：在初学 Vue 时，不推荐直接使用 Vue-cli，尤其是在对基于Node.js的构建工具不熟悉的时候。***  
* ***ps2：在开发环境中最好使用开发版本而不要去使用压缩后的生产版本，否则将失去开发版本中所有常见错误相关的警告。***  

## 1.3 声明式渲染
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

## 1.4 条件与循环
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

## 1.5 处理用户输入
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

## 1.6 组件化应用构建
* 组件系统是 Vue 当中的一个重要的抽象概念，它允许我们使用小型的、独立可复用的组件来构建大型应用
* 在实际开发过程中，几乎任意类型的应用界面都可以被抽象为一个组件树
* 在 Vue 中，一个组件在本质上是一个拥有预定义选项的一个 Vue 实例。[示例：简单 Vue 组件的注册](../../src/html/01_06_Vue_Component.html/#app-07)  
```html
<div id="app-7">
    <ol>
        <!-- 创建一个 todo-item 组件的实例 -->
        <todo-item></todo-item>
    </ol>
</div>
```
```javascript
Vue.component('todo-item', {
    template: '<li>这是一个待办项</li>'
})

var app = new Vue({
    el: "#app-7",
});
```
* 通过 v-bind 指令可以将待办项循环输出到每个组件中，同时不需要重复调用组件。[示例：使用 v-bind 指令通过组件生成列表项](../../src/html/01_06_Vue_Component.html/#app-08)
```html
<div id="app-8">
    <ol>
        <!-- 创建一个 todo-item 组件的实例 -->
        <todo-item
         v-for="item in groceryList"
         v-bind:todo="item"
         v-bind:key="item.id"
        ></todo-item>
    </ol>
</div>
```
```javascript
Vue.component('todo-item', {
    props: ['todo'],
    template: '<li>{{ todo.text }}</li>'
})

var app8 = new Vue({
    el: '#app-8',
    data: {
        groceryList: [{
            id: 0,
            text: '蔬菜'
        }, {
            id: 1,
            text: '奶酪'
        }, {
            id: 2,
            text: '随便其他什么人吃的东西'
        }, ]
    }
})
```

# 2 Vue 实例
## 2.1 Vue 实例的创建
* Vue 实例的创建很简单，只需要通过 ```Vue``` 函数来创建一个 Vue 对象即可。
```javascript
var vm = new Vue({
    //选项
})
```
* 在创建 Vue 实例时，可以向 Vue 函数中传入一个**选项对象**，这个选项对象定义了我们希望这个 Vue 实例实现的行为。
* 一个 Vue 应用，由一个通过 ```new Vue``` 创建的**根 Vue 实例**，以及可选的嵌套的、可复用的组件树组成。

## 2.2 数据与方法
* 当一个 Vue 实例被创建时，它将传入的选项对象中所有的 property（属性）加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“相应”，即匹配更新为新的值。
```javascript
// 我们的数据对象
var data = { a: 1 }

// 该对象被加入到一个 Vue 实例中
var vm = new Vue({
  data: data
})

// 获得这个实例上的 property
// 返回源数据中对应的字段
vm.a == data.a // => true

// 设置 property 也会影响到原始数据
vm.a = 2
data.a // => 2

// ……反之亦然
data.a = 3
vm.a // => 3
```  
* ***ps1：只有在 Vue 实例被创建时就传入的数据对象的 property 才是响应式的。如果实例已经创建，再添加新的 property，新的 property 改动不会触发任何的视图更新。***
* ***ps2：如果对传入的数据对象使用了 ```Object.freeze()```，将会阻止对现有 property 的修改，从而使响应系统无法响应数据变化。[示例：Object.freeze() 阻断响应系统](../../src/html/02_02_Vue_Data&Function.html/#app-09)***
```javascript
var obj = {
    foo: 'bar'
}

Object.freeze(obj)

new Vue({
    el: '#app',
    data: obj
})
```
```html
<div id="app">
    <p>{{ foo }}</p>
    <!-- 这里的 `foo` 不会更新！ -->
    <button v-on:click="foo = 'baz'">Change it</button>
</div>
```  
* 在 Vue 实例当中，除了用户所定义的数据对象的 property 以外，还有一些有用的实例 property 以及实例方法。它们由前缀 ```$``` 开头，以区分用户定义的数据 property。

## 2.3 实例生命周期钩子
* **生命周期钩子**是一些运行于 Vue 实例创建初始化过程中的一系列绑定回调函数。
* 这些函数会在 Vue 实例创建的过程中依次被执行，用户可以在这些函数中添加自己的代码，跟踪 Vue 实例对象的创建，或者实现一些特殊的效果。
* 生命周期钩子的 ```this``` 上下文指向调用它的 Vue 实例。
* ***ps:** 不要在选项 property 或者回调上使用 **箭头函数**。*

## 2.4 实例生命周期图示
![image](../imgs/lifecycle.png)

# 3 模板语法
* Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定到底层的 Vue 实例的数据。
## 3.1 插值
### 3.1.1 文本
* 数据绑定最常见的形式就是使用 “Mustache” 语法（双花括号）的文本插值
```html
<span>Message:{{ msg }}</span>
```  
* Mustache 标签会替代对应数据对象上的 ```msg``` 属性的值。当绑定数据对象上的 ```msg``` 属性值发生变化时，插值处的内容会自动更新。
* *ps：通过 ```v-once``` 指令，可以实现一次性插值，即当数据发生变化时，插值处的内容不会更新。不过需要注意的是，这样可能会影响到该节点上其他数据的绑定。*
```html
<span v-once>这个将不会改变：{{ msg }}</span>
```  

### 3.1.2 原始HTML
* 双大括号会将数据解释为普通文本，而非 HTML 代码。
* 为了输出真正的 HTML，你需要使用 ```v-html``` 指令：
```html
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```
* *ps1：不能使用 ```v-html``` 来复合局部模板，因为 Vue 不是基于字符串的模板引擎。反之，对于用户界面 (UI)，组件更适合作为可重用和可组合的基本单位。* 
* *ps2：动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 **XSS 攻击**。因此，请只对可信内容使用 HTML 插值，**绝不要**对用户提供的内容使用插值。*  

### 3.1.3 Attribute
* HTML 标签属性值的动态设置不能通过 Mustache 语法，而应该使用 ```v-bind``` 指令
```html
<div v-bind:id="dynamicId"></div>
```  
* 对于布尔属性值 （它们只要存在就意味着值为 ```true```），```v-bind``` 工作起来略有不同，在下面这个例子中，如果 ```isButtonDisabled``` 的值是 ```null```、```undefined``` 或 ```false```，则 ```disabled``` 属性值甚至不会被包含在渲染出来的 ```<button>``` 元素中。
```html
<button v-bind:disabled="isButtonDisabled">Button</button>
```

### 3.1.4 使用 Javascript 表达式
* 对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持。
```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```
* *ps1：这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式**，所以下面的例子都**不会**生效。*
```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```
* *ps2：模板表达式都被放在沙盒中，只能访问**全局变量的一个白名单**，如 ```Math``` 和 ```Date``` 。你不应该在模板表达式中试图访问用户定义的全局变量。*   

## 3.2 指令
* 指令是带有 ```v-``` 前缀的特殊属性。
* 指令属性的值预期是**单个 JavaScript 表达式**（v-for 是例外情况）。
* 指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

### 3.2.1 参数
* 一些指令能够接收一个“参数”，在指令名称之后以冒号表示。
* 例如：```v-bind``` 指令和 ```v-on``` 指令，可以响应式的更新 HTML 属性值或者监听 DOM 事件。

### 3.2.2 动态参数
* 从 Vue.js 2.6.0 开始，我们可以使用方括号括起来的 JavaScript 表达式作为一个指令的参数。
* 下面的例子中的 ```attributeName``` 会被作为一个 JavaScript 表达式进行动态求值，求得的值将会作为最终的参数来使用。例如，如果你的 Vue 实例有一个 ```data``` 属性 ```attributeName```，其值为 “```href```”，那么这个绑定将等价于 ```v-bind:href```。
```html
<a v-bind:[attributeName]="url"> ... </a>
```
* 在 DOM 中使用模板时 (直接在一个 HTML 文件里撰写模板)，还需要避免使用大写字符来命名键名，因为浏览器会把 attribute 名全部强制转为小写。
* 动态参数预期会求出一个字符串，异常情况下值为 ```null```。这个特殊的 ```null``` 值可以被显性地用于移除绑定。任何其它非字符串类型的值都将会触发一个警告。
* 动态参数表达式有一些语法约束，**因为某些字符，如空格和引号，放在 HTML attribute 名里是无效的**。

### 3.2.3 修饰符
* 修饰符 (modifier) 是以半角句号 ```.``` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。
* 例如下面的代码，```.prevent``` 修饰符告诉 ```v-on``` 指令对于触发的事件调用 ```event.preventDefault()```：
```html
<form v-on:submit.prevent="onSubmit">...</form>
```

## 3.3 缩写
* `v-` 前缀作为一种视觉提示，用来识别模板中 Vue 特定的 attribute。
* 在构建由 Vue 管理所有模板的**单页面应用程序 (SPA - single page application)** 时，`v-` 前缀也变得没那么重要了。
* 因此，Vue 为 `v-bind` 和 `v-on` 这两个最常用的指令，提供了特定简写：

### 3.3.1 `v-bind` 缩写
```html
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a :[key]="url"> ... </a>
```

### 3.3.2 `v-on` 缩写
```html
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

# 4 计算属性和侦听器
## 4.1 计算属性
* 模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。
* 在模板中放入太多的逻辑会让模板过重且难以维护。
* 这时，我们可以使用**计算属性**来代替这些复杂逻辑，使我们的代码更加的简洁易读。

### 4.1.1 基础例子
```html
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```
```javascript
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})
```

### 4.1.2 计算属性缓存 vs 方法
* 将一个函数定义成一个方法，和将其定义成一个计算属性所得到的最终结果是完全相同的。
* 不过，**计算属性是基于属性之间的响应式依赖进行缓存的**，只有在相关的响应式依赖发生变化的时候，计算属性才会重新求值。
* 计算属性的这一特点意味着只要相关属性的值没有发生改变，多次访问计算属性时都会立即返回之前的计算结果，而不需要再次执行函数，这就减少了程序运行时的资源消耗，提高了属性访问效率。
* 当然，如果不希望由缓存存在，仍然可以使用方法来代替计算属性。

### 4.1.3 计算属性 vs 侦听属性
* 侦听属性同样可以实现属性之间的响应式依赖。
* 不过，对于与多个属性相互依赖的属性而言，使用侦听属性会导致大量的代码重复，而使用计算属性可以更好的实现相关的效果。
* 换言之，假设多个属性之间的关系是 `“A = A1 + A2 + A3 + ... + An”` ，那么计算属性是直接响应式计算 `A` 的值，而侦听属性是分别对 `An` 的值变化进行监听。

### 4.1.4 计算属性的 setter
* 计算属性默认只有 getter， 不过在需要的时候，我们也可以设置一个 setter。
* 设置 setter 可以实现反向响应，即通过计算属性来对相关属性的值进行修改。

## 4.2 侦听器
* 虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。
* 例如，当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

# 5 class 以及 style 的绑定
* 元素的 class 列表和内联样式都属于 attribute，因此我们可以很方便的使用 `v-bind` 指令来处理样式的绑定。
* 在工作中直接处理字符串的拼接是麻烦且易错的，因此 vue.js 对于元素的 `class` 和 `style` 属性增加了一些专门的用法。
## 5.1 绑定 HTML Class
### 5.1.1 对象语法
* vue.js 允许通过 `v-bind:class` 绑定一个对象，对象中的属性标签为类选择器的名称，属性值为Vue 对象中定义的数据属性。通过数据属性的 **“真”** 或者 **“假”** 可以动态的控制类选择器的切换。
* `v-bind:class` 指令同样可以与普通的 class 属性共存。
```html
<div 
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>
```
```javascript
new Vue({
    data: {
        isActive: true,
        hasError: false,
    }
})
```
```html
<!-- 渲染结果 -->
<div class="static active"></div>
```
* `v-bind:class` 绑定的数据对象可以不被内联定义在模板当中，同样可以直接定义在 Vue 对象的属性中。
```html
<div v-bind:class="classObject"></div>
```
```javascript
new Vue({
    data: {
        classObject: {
            active: true,
            'text-danger': false
        }
    }
})
// 或者定义成计算属性
new Vue({
    data: {
        isActive: true,
        error: null
    },
    computed: {
        classObject: function () {
            return {
                active: this.isActive && !this.error, 
                'text-danger': this.error && this.error.type === 'fatal'
            }
        }
    }
})
```

### 5.1.2 数组语法
* vue.js 允许通过 `v-bind:class` 绑定一个数组，数组中的元素对应的 Vue 对象中的属性的值为类选择器的名称。
```html
<div v-bind:class="[activeClass, errorClass"></div>
```
```javascript
new Vue({
    data: {
        activeClass: 'active',
        errorClass: 'text-danger'
    }
})
```
```html
<!-- 渲染结果 -->
<div class="active text-danger"></div>
```
* 如果需要根据条件切换列表中的类，可以在数组中对元素使用三元表达式，或者使用对象语法对单个数组元素进行微调。
```html
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
<!-- 或者 -->
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```

### 5.1.3 用在组件上
* 当在一个自定义组件上使用 `class` 属性时，这些 class 将被添加到该组件的根元素上面。这个元素上已经存在的 class 不会被覆盖。
```javascript
Vue.component('my-component', {
    template:'<p class="foo bar">Hi</p>'
})
```
```html
<my-component class="baz boo"></my-component>
<!-- 渲染结果 -->
<p class="foo bar baz boo">Hi</p>
```

## 5.2 绑定内联样式
### 5.2.1 对象语法
* `v-bind:style` 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名。
```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize +'px' }"></div>
```
```javascript
new Vue({
    data:{
        activeColor: 'red',
        fontSize: 30,
    }
})
```
* 通常情况下，直接绑定样式对象可以使得模板更清晰，同样的，对象语法通常结合返回对象的计算属性来使用。

### 5.2.2 数组语法
* `v-bind:style` 的数组语法可以将多个样式对象应用到同一个元素上
```html
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

### 5.2.3 自动添加前缀
* 当 `v-bind:style` 使用需要添加浏览器引擎前缀的 CSS property 时，如 transform，Vue.js 会自动侦测并添加相应的前缀。

### 5.2.4 多重值
* 从 Vue.js 2.3.0 起你可以为 style 绑定中的 property 提供一个包含多个值的数组，常用于提供多个带前缀的值。
```html
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
<!-- 如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 display: flex -->
```

# 6 条件渲染
## 6.1 `v-if`
* `v-if` 指令会在指令表达式返回真值时渲染添加了当前指令的元素内容。
```html
<h1 v-if="swesome">Vue is awesome!</h1>
```

### 6.1.1 在 `<template>` 元素上使用 `v-if` 条件渲染分组
* `v-if` 指令作用与单个元素上，如果需要切换多个元素，可以将一个 `<template>` 元素当作不可见的包裹元素，并使用 `v-if` 指令，最终渲染的结果不会包含 `<template>` 元素。
```html
<temlpate v-if="ok">
    <h1>Title</h1>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
</temlpate>
```

### 6.1.2 `v-else`
* `v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别。
```html
<h1 v-if="swesome">Vue is awesome!</h1>
<h1 v-else>Oh no `(*>﹏<*)′!!!</h1>
```

### 6.1.3 `v-else-if`
* Vue.js 2.1.0 新增了 `v-else-if` 指令，类似于 if 语句和 else if 语句的关系，`v-else-if` 指令也就是 `v-if` 语句的 “else if” 块。
* 类似于 `v-else`，`v-else-if` 也必须紧跟在带 `v-if` 或者 `v-else-if` 的元素之后。
```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

### 6.1.4 用 `key` 管理可复用的元素
* Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。
* 这样也不总是符合实际需求，所以 Vue 为你提供了一种方式来表达“这两个元素是完全独立的，不要复用它们”。只需添加一个具有唯一值的 `key` 属性。

## 6.2 `v-show`
* 另一个用于根据条件展示元素的选项是 `v-show` 指令。
* 不同的是带有 `v-show` 的元素始终会被渲染并保留在 DOM 中。`v-show` 只是简单地切换元素的 CSS 属性 `display`。
* 同时，`v-show` 不支持 `<template>` 元素。
```html
<h1 v-show="ok">Hello!</h1>
```

## 6.3 `v-if` 和 `v-show` 的区别
* `v-if` 是 “真正” 的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
* `v-if` 也是**惰性**的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
* 相比之下，`v-show` 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
* 一般来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好。

## 6.4 同时使用 `v-if` 和 `v-for`
* 当 `v-if` 与 `v-for` 一起使用时，`v-for` 具有比 `v-if` 更高的优先级。
* 具体细节将在 7.8 节中叙述。
* ***ps：不推荐同时使用 `v-if` 和 `v-for` 指令。***  
  
# 7 列表渲染
## 7.1 用 `v-for` 把一个数组对应为一组元素
* `v-for` 指令可以基于一个数组来渲染一个列表。
* `v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 `items` 是源数据数组，而 `item` 则是被迭代的数组元素的**别名**。
* 在 `v-for` 块中，我们可以访问所有父作用域的属性。
* `v-for` 还支持一个可选的第二个参数，即当前项的索引。
```html
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```
```javascript
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```
* 另外，也可以用 `of` 替代 `in` 作为分隔符。
```html
<div v-for="item of items"></div>
```

## 7.2 在 `v-for` 里使用对象
* `v-for` 指令也可以被用来遍历一个对象的属性。
* 同样，在遍历对象的时候，也支持提供第二个参数，即属性名（键名），还可以使用第三个参数作为索引。
```html
<div v-for="(value, name, index) in object">
  {{ index }}. {{ name }}: {{ value }}
</div>
```
```javascript
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
})
```
* ***ps: 在遍历对象时，会按 `Object.keys()` 的结果遍历，但是不能保证它的结果在不同的 JavaScript 引擎下都一致。***

## 7.3 维护状态
* 当 Vue 正在更新使用 `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。即：如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。
* 这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。
* 为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，我们需要为每项提供一个唯一 `key` 属性。
* *ps:不要使用对象或数组之类的非基本类型值作为 `v-for` 的 key。请用字符串或数值类型的值。*

## 7.4 数组更新检测
### 7.4.1 变更方法
* Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。
* 这些方法包括：`push()`、`pop()`、`shift()`、`unshift()`、`splice()`、`sort()`、`reverse()`。

### 7.4.2 替换数组
* 对于数组操作，除了变更方法，还有一些非变更方法，它们执行时不会变更原始数组，而是**返回一个新数组**。
* 常见的非变更方法有：`filter()`、`concat()`、`slice()`。

### 7.4.3 注意事项
* 由于 JavaScript 的限制，Vue 不能检测数组和对象的变化。

## 7.5 显示过滤/排序后的结果
* 有时，我们想要显示一个数组经过过滤或排序后的版本，而不实际变更或重置原始数据。在这种情况下，可以创建一个计算属性，来返回过滤或排序后的数组。
```html
<li v-for="n in evenNumbers">{{ n }}</li>
```
```javascript
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
computed: {
  evenNumbers: function () {
    return this.numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```
* 在计算属性不适用的情况下 (例如，在嵌套 `v-for` 循环中) 可以使用一个方法来实现过滤。
```html
<ul v-for="set in sets">
  <li v-for="n in even(set)">{{ n }}</li>
</ul>
```
```javascript
data: {
  sets: [[ 1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]]
},
methods: {
  even: function (numbers) {
    return numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```

## 7.6 在 `v-for` 里使用值范围
* `v-for` 也可以接受整数。在这种情况下，它会把模板重复对应次数。

## 7.7 在 `<template>` 上使用 `v-for`
* 类似于 `v-if`，你也可以利用带有 `v-for` 的 `<template>` 来循环渲染一段包含多个元素的内容。
```html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

## 7.8 `v-for` 和 `v-if` 同时使用
* ***ps：不推荐在同一元素上使用 `v-if` 和 `v-for`。***
* 当它们处于同一节点，`v-for` 的优先级比 `v-if` 更高，这意味着 `v-if` 将分别重复运行于每个 `v-for` 循环中。
```html
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
```
* 而如果你的目的是有条件地跳过循环的执行，那么可以将 `v-if` 置于外层元素 (或 `<template>`) 上。
```html
<ul v-if="todos.length">
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ul>
<p v-else>No todos left!</p>
```

## 7.9 在组件上使用 `v-for`
* 在组件上使用 `v-for` 指令时，key 属性是必须的。
* 同时，由于组件有自己独立的作用域，我们定义的外部数据并不会自动传递到组件当中，因此，我们需要使用 prop 参数组来将迭代数据传递到组件当中。
* 不自动将 `item` 注入到组件里的原因是，这会使得组件与 `v-for` 的运作紧密耦合。明确组件数据的来源能够使组件在其他场合重复使用。

# 8 事件处理
## 8.1 监听事件
* Vue.js 中通过使用 `v-on` 指令来给元素事件（点击、聚焦……）绑定 Vue 对象中定义的方法或者简单的Javascript 代码。
```html
<div id="example-1">
  <button v-on:click="counter += 1">Add 1</button>
  <p>The button above has been clicked {{ counter }} times.</p>
</div>
```
```javascript
var example1 = new Vue({
  el: '#example-1',
  data: {
    counter: 0
  }
})
```

## 8.2 事件处理方法
* 然而许多事件处理逻辑会更为复杂，所以直接把 JavaScript 代码写在 `v-on` 指令中是不可行的。因此 `v-on` 还可以接收一个需要调用的方法名称。
```html
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
```
```javascript
var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})

// 也可以用 JavaScript 直接调用方法
example2.greet() // => 'Hello Vue.js!'
```

## 8.3 内联处理器中的方法
* 除了直接绑定到一个方法，也可以在内联 JavaScript 语句中调用方法。
```html
<div id="example-3">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>
```
```javascript
new Vue({
  el: '#example-3',
  methods: {
    say: function (message) {
      alert(message)
    }
  }
})
```
* 有时也需要在内联语句处理器中访问原始的 DOM 事件。可以用特殊变量 `$event` 把它传入方法
```html
<button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>
```
```javascript
// ...
methods: {
  warn: function (message, event) {
    // 现在我们可以访问原生事件对象
    if (event) {
      event.preventDefault()
    }
    alert(message)
  }
}
```

## 8.4 事件修饰符
* Vue.js 为 `v-on` 提供了事件修饰符。
* 通过使用事件修饰符，可以不需要在定义的方法中专门去处理 DOM 事件细节
* 常用的事件修饰符有：`.stop`、`.prevent`、`.capture`、`.self`、`.once`、`.passive`、`.once`（2.1.4新增）、`.passive`（2.3.0新增）等。
```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>

<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>

<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```
* ***ps：使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生，从而产生不同的效果。***

## 8.5 按键修饰符
* 在监听键盘事件时，我们经常需要检查详细的按键。
* Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符，我们可以直接将 `KeyboardEvent.key` 暴露的任意有效按键名转换为 kebab-case 来作为修饰符。
* 按键修饰符的格式为 `keyup.key`。
```html
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```

### 8.5.1 按键码
**ps：`keyCode` 的事件用法已经被废弃了并可能不会被最新的浏览器支持。**

* 使用 `keyCode` 属性，同样可以对键盘按键进行监听
```html
<input v-on:keyup.13="submit">
```
* 为了在必要的情况下支持旧浏览器，Vue 提供了绝大多数常用的按键码的别名：`.enter`、`.tab`、`.delete`（捕获 “删除” 和 “退格” 键）、`.esc`、`.space`、`.up`、`.down`、`.left`、`.right`。
* *ps：有一些按键 (`.esc` 以及所有的方向键) 在 IE9 中有不同的 `key` 值, 如果你想支持 IE9，这些内置的别名应该是首选。*
* 除了官方定义的按键修饰符别名，我们还可以通过全局对象—— `config.keyCodes` 来自定义按键修饰符别名。
```javascript
// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112
```

## 8.6 系统修饰键
* `.ctrl`、`.alt`、`.shift`、`.meta` 等修饰符被用来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。
* ***ps：在 Mac 系统键盘上，meta 对应 command 键 (⌘)。在 Windows 系统键盘 meta 对应 Windows 徽标键 (⊞)。在 Sun 操作系统键盘上，meta 对应实心宝石键 (◆)。在其他特定键盘上，尤其在 MIT 和 Lisp 机器的键盘、以及其后继产品，比如 Knight 键盘、space-cadet 键盘，meta 被标记为“META”。在 Symbolics 键盘上，meta 被标记为“META”或者“Meta”。***
```html
<!-- Alt + C -->
<input v-on:keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div v-on:click.ctrl="doSomething">Do something</div>
```
* *ps：请注意修饰键与常规按键不同，在和 `keyup` 事件一起用时，事件触发时修饰键必须处于按下状态。换句话说，只有在按住 `ctrl` 的情况下释放其它按键，才能触发 `keyup.ctrl`。而单单释放 `ctrl` 也不会触发事件。如果你想要这样的行为，请为 `ctrl` 换用 `keyCode`：`keyup.17`。*

### 8.6.1 .exact 修饰符
* `.exact` 修饰符允许你控制由精确的系统修饰符组合触发的事件。
```html
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button v-on:click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button v-on:click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button v-on:click.exact="onClick">A</button>
```

### 8.6.2 鼠标按钮修饰符
* `.left`、`.right`、`.middle` 等修饰符会限制处理函数仅响应特定的鼠标按钮。

# 9 表单输入绑定
## 9.1 基础用法
### 9.1.1 文本


### 9.1.2 多行文本


### 9.1.3 复选框


### 9.1.4 单选按钮


### 9.1.5 选择框


## 9.2 值绑定
### 9.2.1 复选框


### 9.2.2 单选按钮


### 9.2.3 选择框的选项


## 9.3 修饰符
### 9.3.1 `.lazy`


### 9.3.2 `.number`


### 9.3.3 `.trim`


## 9.4 在组件上使用 `v-model`