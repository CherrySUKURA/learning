# **创建一个与表格内容同步的饼图**

## **首先配置环境，打开 cmd 窗口**

### **使用 vue-cli 将工程化文件创建出来**

### **再将路径 cd 到工程的文件夹下**

### **安装 echarts（图表组件）**

> **`npm install echarts --save`**

### **安装 Element UI （饿了么组件）**

> **`npm i element-ui -S`**

## **将环境配置完成后，就将组件引入进来**

### **因为所使用的组件不同所以使用的引入方式也不同，我们先将 Echarts 引入**

### **通过 npm 上安装的 ECharts 会放在 node_modules 目录下。可以直接在项目代码中 require('echarts') 得到 ECharts。**

```html
<div id="main" style="width: 600px;height:400px;"></div>
```

```javascript
xport default {
 //在vue渲染到都没元素时启用回调函数
 mounted() {
   this.draw();
 },
 methods: {
   draw() {
      var echarts = require('echarts');

      // 基于准备好的dom，初始化echarts实例
      var myChart = echarts.init(document.getElementById('main'));
      // 绘制图表
      myChart.setOption({
          title: {
              text: 'ECharts 入门示例'
          },
         ooltip: {
              trigger: "item",
              formatter: "{a} <br/>{b} : {c} ({d}%)"//显示百分比
              },//提示框
          xAxis: {},//X轴线
          yAxis: {},//Y轴线
          series: [{
              type: 'pie',//类型为饼图
              data: [
                      {name : "阴天" ,value : 22222}//注意value里面只能放数字，他是根据对比value值的大小来决定所占比的
                  ]
              }]
           });
        }
   }
}
```

### **将饼图引入进来后，我们的到了这么一个代码，现在先将我们预设的数据删除，这样我们就可以将我们的数据源 Element ui 中的 table 组件引入进来**

## **首先要在 main.js 中将 Element UI 引入进来,使用以下语句，注意样式文件需要另外的 import 引入**

```javascript
import ElementUI from "element-ui";
import "element-ui/lib/theme-chalk/index.css";
Vue.use(ElementUI);
```

# **注意这两种组件都有两种引入方式，一种为全局引入，一种为按需引入，这里我们使用的都是全局引入**

## **将两个组件放入后我们需要将其引入到 Home.vue 中，因为这两个组件都属于 Home 路由中的组件,而 Home 是 app.vue 中的路由**

```html
<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <tablel></tablel>
  </div>
</template>
```

```javascript
<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import tablel from "@/components/table.vue";

export default {
 name: "home",
 components: {
   HelloWorld,
   tablel
 }
};
</script>
```

### **引入进来后我们就可以将 Tabe 组件写入进来了，新建一个 vue 文件，写入我们的代码**

```html
<template>
  <el-table :data="tableData3" style="width: 100%">
    <el-table-column prop="name" label="姓名" width="120"></el-table-column>
    <el-table-column prop="zip" label="邮编" width="120"></el-table-column>
  </el-table>
</template>
```

```javascript
<script>
export default {
 data() {
   return {
     tableData3: [
       {
         name: "A",
         zip: 20000
       },
       {
         name: "B",
         zip: 20000
      },
       {
         name: "B",
         zip: 20333
       },
       {
         name: "D",
         zip: 20088
       },
       {
         name: "E",
         zip: 20666
       },
       {
         name: "F",
         zip: 20033
       },
       {
         name: "G",
         zip: 20035
       }
     ]
   };
 },
};
</script>
```

### **这样我们就将 table 组件引入了进来，接下来我们需要将表格中的数据通过数值传输传输到并图纸中，为此我们需要先将两个 vue 组件关联起来，也就是说我们要将 HelloWorld.vue 作为 Table.vue 的子组件来讲父组件中的数据 props 到子组件中**

### **首先要注册一个子组件，通过路由将子组件指向 HelloWorld.vue,然后通过 v-bind 为 tableData 赋值，值为父组件中 tableData3**

```html
<HelloWorld :tableData="tableData3"></HelloWorld>
```

```javascript
import HelloWorld from "@/components/HelloWorld.vue";
erprot default{
     components: {
       HelloWorld
    }
};
```

### **当我们的值传输完成后，我们并不能在子组件中直接使用，因为组件之间是互相独立的所以要使用 props 来接受传输过来的数据，有因为饼图组件所使用的数据必须是数组形式，所以我们为接收设置一个验证，让其只能接收数组形式的数据**

```javascript
export default {
  props: {
    //接收数据
    tableData: {
      type: Array, //验证
      default: function() {
        return [];
      }
    }
  }
};
```

## **接收到数据以后将饼图组件中的 data 中的数据替换成{name：this.tableData[0].name，value：this.tableData[0].zip 的形式}**

```javascript
data: [
  {
    name: this.tableData[0].name,
    value: this.tableData[0].zip
  }
];
```
