# 组件
## 在开发项目的过程，无可避免的我们需要写一写重复的标签，而组件提供了我们更加便利的开发，通过组件我们可以把页面分成不同的模块，通过免一模块的需求，我们来进行组件的开发，组件拥有很高的可复用性，这样就可以避免在实际项目中进行重复开发。
## 注册组件
### 我们在component中注册一个组件，组件内的第一个参数为一个名字，第二个参数是一个对象，对象中我们放入template属性，属性的值就是我们要封装的标签,在HTML中，我们在需要放置组件的地方写入一个标签，标签就是我们在组件中写入的第一个参数
```html
<div id="app">
  <my-header></my-header>
</div>
```
```javascript
Vue.component("my-header",{
  template : '<h2>我是头部</h2>'
})

var vm = new Vue({
  el : "#app",
})
```
## 全局组件
### 组件分为全局组件与局部组件，全局组件可以再页面的任何一个地方来调用。
```html
<div id="app">
  <my-header></my-header>
</div>
<div id="app2">
  <my-header></my-header>
</div>
```
```javascript
Vue.component("my-header",{
  template : '<h2>我是头部</h2>'
})

var vm = new Vue({
  el : "#app",
})

var vm = new Vue({
  el : "#app2",
})
```
## 局部组件
### 局部组件只能在定义了他的el的组件中调用
```html
<div id="app">
  <my-header></my-header>
</div>
```
```javascript
var vm = new Vue({
  el : "#app",
  component : {
    'my-header':{
      template : '<h2>我是头部</h2>'
    }
  }
})
```
## 对于组件来说，我们所定义的vue实例就是一个组件，他是一个父组件，而我们另外写的组件则是他的子组件，父组件与子组件之间有一个继承的关机，所以在实例中所用的data，methods等都可以在子组件中书写。这样就不会导致所有的逻辑都写在父组件中而造成逻辑混乱了，每个组件都是相互独立的。
## 为什么要在子组件中的data中写入return
```javascript
Vue.component("my-addcount",{
        template :'',
        data(){
            return {
                
            }
        }
    })
```
## 在子组件的data中如果不写入return的话我们所用的数据就是全局数据，这会造成数据污染，其根本的结果就是组件之间的不独立，数据相互干扰，，加上return之后数据就会变成局部数据，数据之间不会干扰，没有数据污染，组件变得互相独立起来。
## 在组建中我们有五种方法可以书写标签，让其变得更加的符合规范
# 1. \
```javascript
Vue.component("my-addcount",{
        template :'<div @click="add">{{count}}\
                        <ul>\
                             <li>222222</li>\
                        </ul>\
                    </div>',
})
```
# 2. ``
```javascript
Vue.component("my-addcount",{
  template:`<div @click="add">{{count}}
               <ul>
                  <li>2222222</li>
               </ul>
            </div>`,
})
```
# 3.
```html
  <template id="temp">
        <div @click="add">{{count}}
            <ul>
                <li>2222222</li>
                    </ul>
        </div>
  </template>
```
```javascript
Vue.component("my-addcount",{
  template : "#temp",
})
```
# 4.
```html
<script id="temp" type="text/x-template">
    <div @click="add">{{count}}
            <ul>
                <li>2222222</li>
                    </ul>
        </div>
</script> 
```
```javascript
Vue.component("my-addcount",{
  template : "#temp",
})
```
# 5.
## 最后一种写法就是在vue文件中书写