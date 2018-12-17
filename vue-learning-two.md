# **学习 vue**

## **data 和 methode**

### **在创建 Vue 实例时，会将所有在 data 对象中找到的属性，都添加到 Vue 的响应式系统中。每当这些属性的值发生变化时，视图都会“及时响应”，并更新相应的新值。**

### **唯一的例外是，使用 Object.freeze（）来放置已有属性被修改，这也意味响应式系统能够无法追踪变化。**

> ```
> <div id="app">
>   <p>{{ foo }}</p>
>   <!-- 这将不再更新 `foo`! -->
>   <button v-on:click="foo = 'baz'">点我修改</button>
> </div>
> ```
>
> ```
> var obj = {
>   foo: 'bar'
> }
>
> Object.freeze(obj)
>
> new Vue({
>   el: '#app',
>   data: obj
> })
> ```

### **值得注意的是，如果实例已经创建，那么只有那些 data 中的原本就已经存在的属性，才是响应式的，而在实例创建后再添加的属性不会出发任何响应式更新**

### **除了 data 属性，Vue 实例还暴漏了一些有用的实例属性和方法。这些属性与方法都具有前缀\$，以便与用户定义的属性有所区分。例如：**

> ```
> var data = { a: 1 }
> var vm = new Vue({
>  el: '#example',
>  data: data
> })
>
> vm.$data === data // => true
> vm.$el === document.getElementById('example') // => true
>
> // $watch 是一个实例方法
> vm.$watch('a', function (newValue, oldValue) {
>  // 此回调函数将在 `vm.a` 改变后调用
> })
> ```

## **生命周期钩子函数**

### **每个 Vue 实例在被创建之前，都要经过一系列的初始化过程，Vue 实例需要设置数据观察、编译模板、在 Dom 挂载实例，以及在数据变化时更新 Dom。在这个过程中，Vue 实例还会调用执行一些生命周期钩子函数，这样用户能够在特地你那个阶段添加自己的代码。**

### **在实例创建后调用 created 钩子函数：**

> ```
> new Vue({
>  data: {
>    a: 1
>  },
>  created: function () {
>    // `this` 指向 vm 实例
>    console.log('a is: ' + this.a)
>  }
> })
> // 结果是 "a is: 1"
> ```

## **不要在选项属性或者回调函数中使用箭头函数。因为箭头函数会绑定父级上下文，所以 this 不会按照预期指向 Vue 实例，经常会产生错误**

# **模板语法**

## _插值表达式_

## **#文本**

### **数据绑定最基础的形式，就是使用“mustache”语法（双花括号）的文本插值**

> **`<span>Message: {{ msg }}</span>`**

### **双花括号标签将会被替换为 data 对象上对应的 msg 属性的值。只要绑定的数据对象上的 msg 属性发生改变，差值内容也会随之更新。**

### **也可以通过使用 v-once 指令，执行一次性插值，也就是说，在数据改变时，插值内容不会随之更新。但是请牢记，这也将影响到同一节点上的其他所有绑定：**

> **`<span v-once>这里的值永远不会改变：{{ msg }}</span>`**

## **#原始 HTML**

### **双花括号语法会将数据中的 HTML 转为纯文本后再进行插值。为了输出真正的 HTML，可以使用 V-HTML 指令**

> ```
>    <p>
>      <span v-html="rawHtml"></span>
>    </p>
> ```
>
> ```
>     new Vue({
>          el : "#app",
>          data:{
>             rawHtml : "<span style='color:red'>222222</span>"
>            }
>        })
> ```

### **span 中的内容，将会被替换为 rawHTML 属性的值，并且作为原始 HTML 插入，但是 v-html 无法用来组合局部模板，这是因为 Vue 不是基于字符串的模板引擎。繁殖对于用户界面，组件更适合作为可重用和可组合的基本单位，而且网站中动态渲染任意 HTML 是很危险的很容易受到 xss 攻击。**

## **#属性**

### **不能再 Vue 模板中的 HTML 属性上使用双花括号语法。而是应该使用 v-bind 指令**

> **`<div v-bind:id="dynamicld"></div>`**

### **在属性是布尔类型的一些情况中，v-bind 的作用有点不同，只要值存在就会隐含为 true**

> **`<button v-bind:disabled="isButtonDisabled">Button</button>`**

### **如果 isButtonDisabled 的值为 null，undefined 或 false，disabled 属性甚至不会被包含在渲染后的 button 元素中**

# **computed 属性和 watcher**

## **computed 属性**

### **在模版中使用表达式是非常方便直接的，然而这只适用于简单的操作。在模版中放入太多的逻辑，会使模板过度膨胀和难以维护。这个时候我们就可以使用 computed 属性。**

### **例子：将 hello 翻转**

> ```
> <div id="example">
>  <p>初始 message 是："{{ message }}"</p>
>  <p>计算后的翻转 message 是："{{ reversedMessage }}"</p>
> </div>
> ```
>
> ```
> var vm = new Vue({
>  el: '#example',
>  data: {
>    message: 'Hello'
>  },
>  computed: {
>    // 一个 computed 属性的 getter 函数
>    reversedMessage: function () {
>      // `this` 指向 vm 实例
>      return this.message.split('').reverse().join('')
>    }
>  }
> })
> ```

### **在这里我们声明了一个 computed 属性 reversedMessage。然后恩我 Ivm.reversedMessage 属性提供了一个函数，作为它返回值函数（getter 函数），通过这个例子我们可以看出，vm.reversedMessage 的值总是依赖于 vm.message 的值**
