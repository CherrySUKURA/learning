# **使用 vue-cli 3.X 构建项目**

## **安装 vue-cli 3.X 需要 node.js>=8.9 版本,可以使用命令查看版本**

> **`node -v`**

## **1.使用命令全局安装 vue-cli 3.X**

> **`npm install -g @vue/cli`**

## **查看是否安装成功**

> **`vue -V`**

## **构建项目**

> **`vue create <Project Name>`**

### **这时候出现一个选项让你选择 npm 包（辅助功能），这个是选择是使用默认设置还是自己配置，default（默认）、Manually select features 是手动配置，如果有其他的选项，那个是你们自己保存的配置**

### **如果选择了手动配置会在选择完后遇到几个问答：**

### **1.是否使用 history router：**

### **Vue-Router 利用了浏览器自身的 hash 模式和 history 模式的特性来实现前端路由（通过调用浏览器提供的接口）**

### **hash： 浏览器 url 址栏 中的 # 符号（如这个 URL：http://www.abc.com/#/hello，hash 的值为“ #/hello”），hash 不被包括在 HTTP 请求中（对后端完全没有影响），因此改变 hash 不会重新加载页面**

### **history：利用了 HTML5 History Interface 中新增的 pushState( ) 和 replaceState( ) 方法（需要特定浏览器支持）。单页客户端应用，history mode 需要后台配置支持（详细参见：https://router.vuejs.org/zh/guide/essentials/history-mode.html）**

### **2.css 预处理器**

### **主要为 css 解决浏览器兼容、简化 CSS 代码 等问题，这个随自己编码习惯**

### **3.ESLint**

### **提供一个插件化的 javascript 代码检测工具**

### **4.何时检测**

### **5.单元测试**

### **6.如何存放配置 **

### **7. 是否保存本次配置（之后可以直接使用）**

## **搭建完成**

### **cd 到你搭建的项目文件夹**

> **`cd <File Name>`**

### **运行项目**

> **`npm run serve`**

### <img src="https://upload-images.jianshu.io/upload_images/5814981-e532bc879ad294ef.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/767/format/webp" />
