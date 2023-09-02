---
{"title":"基本概念-VUE学习","slug":"01-start","description":"VUE基本概念","author":"six","created":"2023-03-27","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["vue"],"categories":["vue","js"],"dg-publish":true,"permalink":"/front/vue/01-start/","dgPassFrontmatter":true}
---


# MVVM思想

- 由前端框架完成复杂的DOM操作
- MVVM由后端MVC架构演变而来
  ![](https://s.sixmillions.cn/img/2023/03/25/112004ae01.png)
- 前后端分离，前端拿到的不是视图了，而是数据，所以前端也需要将数据渲染数据到页面
  后端数据和试图不直接关联，而是由中间的VM关联起来，这就是MVVM
  VM完成了数据的绑定和监听
  ![](https://s.sixmillions.cn/img/2023/03/25/112256vcfp.png)
# Hello World

> 在线演示 https://play.vuejs.org/

```vue
<script>
export default {
  data() {
    return {
      msg: 'Hello World!'
    }
  } 
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <input v-model="msg">
</template>
```

# 选项式API优缺点

![](https://s.sixmillions.cn/img/2023/03/25/113333cfjg.png)

es6语法，解构的时候可以添加默认值

```js
var obj = {name: "xiaoming", age: 18, height: 181};
var ccc = 123;
var { name, age, height, color=ccc } = obj;
// name = "xiaoming" age=18 height=181 color=123
// 这里color在obj中没有值，使用的默认值ccc
```

缺点，不够灵活

# 声明式渲染

只要在页面声明该数据就行，不用关系数据是怎么跑到页面的，不用管数据改变为什么页面也变

声明式编程：不需要编写具体实现，只需要调用声明就可以实现功能。类似的还有sql语句

```vue
<template>
  <h1>{{ msg }}</h1>
  <input v-model="msg">
  <button @click="change">改变</button>
</template>

<script>
export default {
  data() {
    return {
      msg: 'Hello World!'
    }
  },
  methods: {
    change: function () {
      this.msg = "1111"
    }
  }
}
</script>
```

双大括号中写的是JS表达式，JS表达是就是能赋值的表达式

![](https://s.sixmillions.cn/img/2023/03/25/1157244st8.png)

修改数据，页面也能随着变化原理：使用了ES6的Proxy对象

修改数据出触发set方法，获取数据触发get方法

## 其他

> [js中可以直接使用id而不用获取id - 程序媛李李李李蕾 - 博客园 (cnblogs.com)](https://www.cnblogs.com/daysme/p/6273562.html)

直接使用id操作DOM

```
<div id="app">Hello</div>
<script>
home.innerHTML="你好"
</script>
```

# VUE指定系统和事件方法

> 常用的指定: https://cn.vuejs.org/api/built-in-directives.html

- v-text
- v-show
- v-if
- v-for
- v-on，调用vue的方法，可以简写为 `@`
- v-bind，让便签属性变成响应式，可以简写为`:`
- v-model，双向数据绑定

**this指向的就是vm对象**

```vue
<template>
  <h1 :title="msg">{{ msg }}</h1>
  <button @click="change">改变</button>
  <button @click="foo(2222)">传参</button>
  <button @click="bar($event,3333)">event+传参</button>
</template>

<script>
export default {
  data() {
    return {
      msg: 'Hello World!'
    }
  },
  methods: {
    change: function (event) {
       //this指向的就是vm对象
       this.msg = "1111"
       console.log(event)
    },
    foo: function (param) {
       this.msg = "2222"
       console.log(param)
    },
    //有参数和event的时候，event被vue封装到了$event中
    bar: function (event, param) {
       this.msg = "3333"
       console.log(event)
       console.log(param)
    }
 }
}
</script>
```

# 计算属性和侦听器

## 计算属性和方法

- 方法需要加括号调用，计算属性可以直接写
- 计算属性可以有缓存特性，而方法每次都会调用
- 计算属性是只读的，如果要修改，需要修改计算属性依赖的属性

## 计算属性和侦听器

![](https://s.sixmillions.cn/img/2023/03/25/123511hixu.png)

```vue
 watch: {
   msg(newVal, oldVal) {
     console.log(newVal, oldVal)
   }
 }
```

- 多个值影响一个值适合用计算属性
- 一个值影响多个值适合用监听器
- 侦听器可以使用异步处理，但是计算属性因为有return所以不能用异步

# 条件渲染/列表渲染


![](https://s.sixmillions.cn/img/2023/03/25/1422254qgp.png)

![](https://s.sixmillions.cn/img/2023/03/25/1424068hmy.png)

![](https://s.sixmillions.cn/img/2023/03/25/1427005002.png)

# class属性操作

## 普通字符串

![](https://s.sixmillions.cn/img/2023/03/25/142831wcii.png)

属性操作不够灵活

## 数组

![](https://s.sixmillions.cn/img/2023/03/25/142916mywf.png)

## 对象

![](https://s.sixmillions.cn/img/2023/03/25/143009f6p2.png)

## style属性操作

也是三种

![](https://s.sixmillions.cn/img/2023/03/25/143126p15n.png)

# 表单和双向数据绑定

v-model，对数据和视图进行双向绑定

常用表单控件：input（输入，复选框，单选框），select（下拉菜单），textarea

```vue
<script>
export default {
  data() {
    return {
      msg: 'Hello World!'
    }
  }
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <input v-model="msg">
</template>
```

# 声明周期函数

> [生命周期钩子 | Vue.js (vuejs.org)](https://cn.vuejs.org/guide/essentials/lifecycle.html)

![](https://s.sixmillions.cn/img/2023/03/25/1442391dmj.png)

-   **beforeCreate** —— 在实例初始化之后、进行数据侦听和事件/侦听器的配置之前同步调用。
-   **created** —— 在实例创建完成后被立即同步调用。
-   **beforeMount** —— 在挂载开始之前被调用：相关的 render 函数首次被调用。
-   **mounted** —— 在实例挂载完成后被调用。
-   **beforeUpdate** —— 在数据发生改变后，DOM 被更新之前被调用。
-   **updated** —— 在数据更改导致的虚拟 DOM 重新渲染和更新完毕之后被调用。
-   **beforeDestroy** —— vue实例销毁之前调用。
-   **destroyed** —— vue实例销毁之后调用

![](https://s.sixmillions.cn/img/2023/03/25/144438qucw.png)
