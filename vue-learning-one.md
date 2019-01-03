# **学习 vue**

## **挂载点与 Vue 实例化**

```html
<div id="app"></div>
```

```javascript
var vm = new Vue({
  el: "#app"
});
```

_这就是 Vue 实例化_

> **`el : "#app"`**  
> _设置一个挂载点，挂载点的选择就是 dom 节点可以用标签名也可以用 class 或者 id 选择器_

## **v-model 双向绑定**

```html
<div id="vueInstance">输入您的姓名： <input type="text" v-model="name" /></div>
```

```javascript
    <script>
        var vm = new Vue({
            el : "#vueInstance",
            data : {
                name : "_Appian"
            }
        })
    </script>
```

### **v-model 我理解的大概的意思是，可以将数据绑定在节点上，你可以让数据显示在页面上，也可以由页面改变数据，这是双向的，她是一个双向通道**

## **v-on 进行事件监听**

### **v-on 可以监听事件的触发并执行函数，比说它监听到了点击事件并触发了弹出框函数**

```html
<button v-on:click="say">欢迎点击</button>
```

```javascript
<script>
    var vm = new Vue({
        el : "#vueInstance",
        data : {}
        methods : {
            say : function (){
               alert("欢迎" + this.name)
            }
       }
    })
```

## **v-if 与 v-show 进行条件判断**

### v-if 和 v-show 基本上一样他们都是由布尔类型来判断节点是否显示的，但是也有区别，他们的区别在于 v-if 在进行变化的时候会将消失掉的模块删除，从代码上删除，而 v-show 只是隐藏，因此 v-if 的切换消耗会比 v-show 更高，而 v-show 的初始渲染消耗会比 v-if 更高，也因此如果需要频繁的切换用 v-show 更好一些，而其他时候用 v-if 会更好一些

```html
<div id="vueInstance">
  <!-- loginStatus为true时会显示section -->
  <selection v-if="loginStatus">
    输入您的姓名： <input type="text" v-model="name" />
    <button v-on:click="say">欢迎点击</button>
    <button @click="switchLoginStatus">退出登录</button>
  </selection>

  <!-- loginStatus为false时会显示section -->
  <section v-if="!loginStatus">
    登录用户： <input type="text" /> 登录密码： <input type="password" />
    <button @click="switchLoginStatus">登录</button>
  </section>
</div>
```

```javascript
    <script>
        //创建一个新的vue实例，并设置挂载点
        var vm = new Vue({
            el : "#vueInstance",
            data : {
                name : "_Appian",
                loginStatus : false
            },
            methods : {
                say : function (){
                    alert("欢迎" + this.name)
                },
                switchLoginStatus : function(){
                    this.loginStatus = !this.loginStatus
                }
            }
        })
    </script>
```

## **v-for 输出列表**

### **v-for 会循环出 data 中 products 数组的每一个节点并根据节点的数量来遍历出同等数量的 li 用插值表达式来将节点中的数据输出到 li 标签中，**

```html
<div id="vueInstance">
  <ul>
    <li v-for="(el,index) in products">
      <!-- element in arrayObj 循环arrayObj这个数据对象里的每一个element -->
      <!-- (el,index)可以将下标一起循环出来 -->
      {{index}}-{{el.name}}-￥{{el.price}}-{{el.category}}
    </li>
  </ul>
</div>
```

```javascript
    <script>
        //创建一个新的vue实例，并设置挂载点
        var vm = new Vue({
            el : "#vueInstance",
            data : {
                   products : [
                         {name: 'microphone', price: 25, category: 'electronics'},
                         {name: 'laptop case', price: 15, category: 'accessories'},
                         {name: 'screen cleaner', price: 17, category: 'accessories'},
                         {name: 'laptop charger', price: 70, category: 'electronics'},
                         {name: 'mouse', price: 40, category: 'electronics'},
                         {name: 'earphones', price: 20, category: 'electronics'},
                         {name: 'monitor', price: 120, category: 'electronics'}
                    ]
                }
        })
    </script>
```

## **计算属性 computed**

### **计算属性的应用场景，一般是在有一个变量的值需要其他变量计算得到的时候，会用到**

```html
<div id="vueInstance">
  输入一个数字：<input type="text" v-model="value" />
  <p>它的平方是：{{square}}</p>
</div>
```

```javascript
    <script>
        var vm = new Vue({
            el : "#vueInstance",
            data : {
                value : 1
            },
            computed : {
                square : function () {
                    return this.value * this.value;
                    // Vue中的this指的就是实例
                }
            }
        })
    </script>
```
