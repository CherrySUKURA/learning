# 在 pie 项目中放入表格组件

## 首先需要在 cmd 中安装 ElementUI 组件库

### cd 到项目文件目录下，输入：

> **`npm i element-ui -S`**

### 安装完成后在 mainjs 将其引入

```javascript
import element from "element-ui";
import "element-ui/lib/theme-chalk/index.css";

Vue.use(element);
```

### 由于项目的需求（需要将表格中的数据显示在饼图上）我们将 meEcharts 中的 data（）删除并在父组件 Home.vue 中写入 data（），方便我们进行组件中的传值。

```html
//Home.vue
<template>
  <div class="home">
    <img alt="Vue logo" src="~@/assets/logo.png" />
    <meEcharts :tableData="tableData" msg="Welcome to Your Vue.js App" />
    <meTable :tableData="tableData"></meTable>
    <meform @divSub="handleSubInput"></meform>
  </div>
</template>
```

```javascript
//Home.vue
import meEcharts from "@/components/cp-wzh-Echarts/index.js";
import meTable from "@/components/cp-wzh-Table/index.js";
import meform from "@/components/cp-wzh-form/index.js";

export default {
  name: "home",
  components: {
    meEcharts,
    meTable,
    meform
  },
  data() {
    return {
      tableData: [
        { name: "A", value: "20000" },
        { name: "B", value: "11111" },
        { name: "C", value: "20000" },
        { name: "D", value: "20000" }
      ]
    };
  },
  methods: {
    handleSubInput({ index, val }) {
      console.log("zhi", index);
      this.setValue(index, val);
    },
    setValue(index, val) {
      this.tableData.push({
        name: index,
        value: val
      });
    }
  }
};
</script>

```

```javascript
//meEcharts
<script>
var echarts = require("echarts");
export default {
  props: ["tableData"],
  //在vue渲染到都没元素时启用回调函数
  mounted() {
    this.draw();
  },
  watch: {
    tableData: function() {
      this.draw();
    }
  },
  methods: {
    //指定图表的配置项和数据
    draw() {
      //导入echar依赖，在node_modules里面，这里说一下import和require的区别，import需要具体到相对地址，而require则不用，会自动安装
      var myChart = echarts.init(document.getElementById("main"));
      myChart.setOption({
        title: {},
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        }, //提示框
        series: [
          {
            type: "pie",
            data: this.tableData
          }
        ]
      });
      console.log(this.tableData);
    }
  }
};
</script>
```

### 由于所有的数据在父组件 Home.vue 中，需要先在 Home.vue 中注册子组件在通过父子组件传值的方法将数据传入子组件中，在子组件中通过 props 来接受父组件的数据，这样我们就将 Home 组件中的数据传入到 meEcharts 中并使用了

### 接下来我们新创建一个组件起名叫做 meTable.vue，并在这个组件中放入我们要添加的表格组件

```html
<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="name" label="日期" width="180"></el-table-column>
    <el-table-column prop="value" label="姓名" width="180"></el-table-column>
  </el-table>
</template>
```

### 和 meEcharts 一样我们在 Home.vue 中注册了 meTable 组件后，在 meTable 中通过 props 接收数据，由于组建中已经将所有的数据写入其中，所以我们只需要将数据接收就好了

```javascript
<script>
export default {
  props: {
    tableData: {
      type: Array
    }
  }
};
</script>
```

### 接下来我们需要再次创建一个子组件 meform 以更改我们的数据来让我们的项目变成可以随时增加数据的项目

### 和 meTable 组件一样我们先新建一个 meform.vue 文件，然后在父组件中注册一下，不过和 meTable 不一样的是这一回我们要做的事从子组件传值给父组件，所以并不需要将 data（）传送给 meform

```html
<template>
  <div style="margin-top: 15px;">
    <el-input placeholder="请输入销量" v-model="select"></el-input>
    <el-input placeholder="请输入销量" v-model="input5"></el-input>
    <el-button
      slot="append"
      icon="el-icon-upload"
      @click="divclick"
      id="el-button-from"
      >确定</el-button
    >
  </div>
</template>
```

```javascript
<script>
export default {
  data() {
    return {
      input5: "",
      select: ""
    };
  },
  methods: {
    divclick: function() {
      let index = this.select;
      let val = this.input5;
      this.$emit("divSub", { index, val });
    }
  }
};
</script>
```

### 首先我们将 input 框中的值通过双向绑定和 input5，select 属性绑定，以此来将我们输入的值存储起来，并且通过监听 button 中的绑定事件来执行 divclick 函数，将我们输入的值存入变量 index 和 val 中，并通过子组件向父组件传值

> **`this.$emit("divSub",{index,val})`**

### 通过自定义事件$emit我们将index和val传入到了父组件当中，在父组件中我们通过监听到$emit 所设定的 divSub 事件来执行方法 handleSubIput，因为传过来的是一个对象所以我们并不能直接使用，需要另外执行一个方法 setValue（index，val），我们在这个方法中通过 push（{name：index，value:val}）来将我们上传的数据添加到 data（）中。
