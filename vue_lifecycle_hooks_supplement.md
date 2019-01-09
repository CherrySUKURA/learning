# 本章为对生命周期钩子的补充
## 生命周期钩子是在vue实例执行的各种情况下使用的方法，是vue让我们在vue的生命周期中插入自己的代码的方法
- beforeCreate钩子：在实例创建之后，初始化之前。实例里面的数据没有加载的时候
- created钩子：实例初始化之后，已经加载了数据
- beforeMount钩子：数据挂载到节点之前
- Mounted钩子：数据挂载到节点之后
- beforUpdate钩子：数据更新之前
- updated钩子：数据更新之后
- beforeDestoy钩子：数据销毁前
- destroyed钩子：数据销毁后
```html
<div id="app">
    <div>{{message}}</div>
</div>
```
```javascript
var vm = new Vue({
    el: "#app",
    data() {
        return {
            message: "hello vue"
        }
    },
    beforeCreate() {
        //在最开始的时候实例创建之后，初始化之前。实例里面的数据没有加载的时候
        console.log(this.$el);
        console.log(this.$data);
    },
    created() {
        //实例初始化之后，已经加载了数据
        console.log(this.$el);
        console.log(this.$data);
    },
    beforeMount() {
        //数据挂载到节点之前
        console.log(this.$el);
        console.log(this.$data);
    },
    mounted() {
        //数据挂载到节点之后
        setTimeout(() => {
            this.message = "hi javascript";
        }, 2000)
        console.log(this.$el);
        console.log(this.$data);
    },
    beforeUpdate() {
        //数据更新之前
        console.log("更新前")
    },
    updated() {
        //数据更新之后
        console.log("更新后")
    },
    beforeDestroy() {
        //对象销毁前
        console.log("销毁前")
    },
    destroyed() {
        //对象销毁后
        console.log("销毁后")
        //vm.$destroy() 销毁对象
    },
})
```