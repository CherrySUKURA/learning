# 知识补充

## 插值表达式

```html
<div id="app">
  {{message}}
  <!-- 中间的并不是一个字符串而是js表达式语法-->
</div>
```

##vue 响应式渲染的原理 (date 属性)

```html
<div id="div1"></div>
```

```javascript
var div1 = document.getElementById("div1");

var obj = {
  message: "hello"
};

div1.innerHTML = obj.message;

Object.defineProperty(obj, "message", {
  set(val) {
    //一旦改变了就会触发set
    div1.innerHTML = val;
  },
  get() {
    return div1.innerHTML;
  }
});
```

### Object.defineProperty(obj, prop, descriptor)方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。这个方法并不能用在变量上，他只能用在对象上

```
obj
要在其上定义属性的对象。
prop
要定义或修改的属性的名称。
descriptor
将被定义或修改的属性描述符。
```

## 方法简写

### 在 es6 当中提供了对于方法提供了一种简写的操作

```javascript
//未简写
//如果在全局定义了变量并且调用
var name = "hello";
var obj = {
  //name : 'hello',
  name: name,
  showName: function() {},
  showAge: function() {}
};
```

```javascript
//简写
//如果全局定义了变量并且调用，可以简写
var name = "hello";
var obj = {
  //name : 'hello',
  name,
  showName() {},
  showAge() {}
};
```

### 属性解析成变量

```javascript
var name = "hello"
var setKey = "age"
var obj = {
    name,
    //setKey : "20"//如果直接这么写变零setKey是没有值的
    [steKey] ：”20“，//加上中括号就可以让setKey=age=20
    showName(){

    },
    showAge(){

    }
}
```

## 计算属性 vs 插值表达式 （写法更加简单易用）

```html
<div id="app">{{message.split('').reverse(),join('')}} {{reversemessage}}</div>
```

```javascript
var vm = new Vue({
  el: "#app",
  data: {
    message: "Hello World"
  }
});
```

```javascript
var vm = new Vue({
  el: "#app",
  data: {
    message: "Hello World"
  },
  computed: {
    reversemessage() {
      return this.message.split(""), reverse(), join("");
    }
  }
});
```

### split() 方法用于把一个字符串分割成字符串数组。

```javascript
var str = "How are you doing today?";

document.write(str.split(" ") + "<br />"); //How,are,you,doing,today?
document.write(str.split("") + "<br />"); //H,o,w, ,a,r,e, ,y,o,u, ,d,o,i,n,g, ,t,o,d,a,y,?
document.write(str.split(" ", 3)); //How,are,you
```

### reverse() 方法用于颠倒数组中元素的顺序。

### join() 方法用于把数组中的所有元素放入一个字符串,元素是通过指定的分隔符进行分隔的。

## 计算属性 vs methods

### 计算属性只有在相关依赖发生改变的时候才会重新执行方法，否则只会返回上次计算的结果缓存。

### 而 methods 不管相关依赖有没有发生改变都会执行一次，调用几次就执行几次

## v-if 补充（v-else）

```html
<div id="app">
  <div v-if="show">aaaa</div>
  <!--如果show为true就显示aaaa否则就显示bbbb-->
  <div v-else>bbbb</div>
</div>
```

```javascript
var vm = new Vue({
  el: "#app",
  data: {
    show: "true"
  }
});
```

### 还可以这么写

```html
<div id="app">
  <div v-if="num == 1">AAAA</div>
  <div v-else-if="num == 2">BBBB</div>
  <div v-else>CCCC</div>
</div>
```

```javascript
var vm = new Vue({
  el: "#app",
  data: {
    num: 1
  }
});
```

## <template></template>不会被浏览器解析

## v-for （for in 和 for of 的区别）

### 在 vue 中没有区别，但是在原生中有区别，在原生中 for in 用来遍历对象的属性，而不是数值本身，这也就是说如果遍历的是个对象如：

```javascript
var obj = {
  name: "hello",
  age: "20",
  job: "it"
};
```

### 那么他所遍历出来的只有 name，age，it 这些对里的属性，而对于数组来说，它的下标就是它的属性

### for of 是 es6 中新的遍历方法，和 for in 不同的是 for of 所遍历的正是数值本身，而 for of 不能遍历 Object 对象，除非给 Object 增加一个遍历器，当然你也可以将 Object 对象转换成一个数组

```javascript
//Object.values(obj) //把对象转成值的数组 -> ['hello','20','it']
//Object.keys(obj)//把对象转成属性的数组 -> ['name','age','job']
for(var v od Object keys(obj)){
    console.log(v);
}
```

```
shift:从集合中把第一个元素删除，并返回这个元素的值。
unshift: 在集合开头添加一个或更多元素，并返回新的长度
push:从集合最后一个添加元素，并返回新的长度
pop:从集合中把最后一个元素删除，并返回这个元素的值。
```

## splice() 方法向/从数组中添加/删除项目，然后返回被删除的项目

```javascript
arrayObject.splice(index,howmany,item1,.....,itemX)
/*
index	必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
howmany	必需。要删除的项目数量。如果设置为 0，则不会删除项目。
item1, ..., itemX	可选。向数组添加的新项目。
*/
```
