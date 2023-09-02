---
{"title":"组件-vue学习","slug":"02-component","description":"vue组件","author":"six","created":"2023-03-27","updated":"2023-09-02","cover":"https://picsum.photos/720/400","tags":["vue"],"categories":["vue","js"],"dg-publish":true,"permalink":"/front/vue/02-component/","dgPassFrontmatter":true}
---

# 目标

- 单文件组件（SFC）学习
- 组件通信
- 组件属性和事件处理
- 组件组合

# 概念

![](https://s.sixmillions.cn/img/2023/03/25/145741ou6g.png)

## 注意

- 尽量不用单个单词的组件
- 用小写加中划线或者大驼峰命名
- 使用的时候建议用小写字母加中划线分隔这种方式
- 分为全局和局部组件

![](https://s.sixmillions.cn/img/2023/03/25/150856ec33.png)

# 组件通信

why?

![](https://s.sixmillions.cn/img/2023/03/25/150959eeun.png)

![](https://s.sixmillions.cn/img/2023/03/25/151041ii5s.png)

## 父传子

通用属性props实现

App.vue

```vue
<template>
  <h1>{{ msg }}</h1>
  <comp :count="num"/>
</template>

<script>
import Comp from './Comp.vue'
export default {
  data() {
    return {
      msg: 'Hello World!',
      num: 222
    }
  },
  components: {
    Comp
  }
}
</script>
```

Comp.vue

```vue
<template>
{{ msg }} : {{ count }}
</template>

<script>
export default {
  data() {
    return {
      msg: "子组件1"
    }
  },
  props: ['count'],
}
</script>
```

## 子传父

通过自定义事件实现

App.vue

```vue
<template>
  <h1>{{ msg }}</h1>
  <h2>
    子组件传递过来的数据：{{ comp1Data }}
  </h2>
  <comp1 @app-click="handleClick"/>
</template>

<script>
import Comp1 from './Comp1.vue'
export default {
  data() {
    return {
      msg: 'Hello World!',
      comp1Data: ''
    }
  },
  methods:{
    handleClick(data) {
      this.comp1Data = data
    }
  },
  components: {
    Comp1
  }
}
</script>
```

Comp1.vue

```vue
<template>
{{ msg }}
 <button @click="foo">给父组件传递数据</button>
</template>

<script>
export default {
  data() {
    return {
      msg: "子组件1"
    }
  },
  methods: {
    foo: function() {
      //调用父组件方法传值$emit,第一个是方法名，第二个是参数
      this.$emit('app-click', "Comp1 Value")
    }
  },
  //自动注册，可以不写，但是建议写上，方便知道注册了哪些事件
  emits: ['app-click'],
}
</script>
```

## 注意

- props可以写成对象形式，然后可以自定义类型和默认值
- 父组件传过来的数据是只读的。如果子组件想修改，需要定义一个变量接受传过来的值
- 数据双向流动可以用v-model实现

# slot

![](https://s.sixmillions.cn/img/2023/03/25/163710zm4l.png)


app.vue

```vue
<template>
  <h1>{{ msg }}</h1>
  <!-- 默认插槽 -->
  <comp2>
	<h2>{{ msg }}</h2>  
  </comp2>
  <!-- 具名插槽 -->
  <comp3>
    <template v-slot:title1>
      <h2>{{ msg }}</h2>
    </template>
    <!-- 简写 -->
    <template #title2>
      <h3>{{ msg }}</h3>
    </template>
  </comp3>
</template>

<script>
import Comp2 from './Comp2.vue'
import Comp3 from './Comp3.vue'
export default {
  data() {
    return {
      msg: 'Hello World!'
    }
  },
  components: {
    Comp2, Comp3
  }
}
</script>
```

Comp2.vue

```vue
<template>
  <slot></slot>
</template>
```

Comp3.vue

```vue
<template>
  <slot name="title1"></slot>
  <slot name="title2"></slot>
</template>
```

## 作用域插槽

为了拿到子组件的数据

```vue
<template>
  <h1>{{ msg }}</h1>
  <div>作用域外边的数据 {{ myData }}</div>
  <comp4>
    <!-- 拿到数据myData，这个变量命名需要满足js变量命名规范 -->
    <template #my-slot="{myData}">
      <h2>{{ msg }}</h2>
      <div>拿到的值如果和父作用域的变量重名，优先使用拿到的{{ myData }}</div>
      <ul>
        <li v-for="item in myData">{{ item }}</li>
      </ul>
    </template>
  </comp4>
</template>

<script>
import Comp4 from './Comp4.vue'
export default {
  data() {
    return {
      msg: 'Hello World!',
      myData:'2222'
    }
  },
  components: {
    Comp4
  }
}
</script>
```

Comp4.vue

```vue
<template>
<slot name="my-slot" :myData="list"></slot>
</template>

<script>
export default {
  data() {
    return {
      list: ['A', 'B', 'C']
    }
  },
}
</script>
```

## 其他

es6动态key

```js
//普通
let obj = {}
obj.name = 'six'
obj[age] = 13

//计算出来key
obj['my'+'work'] = 'it coder'

//简洁写法
let me = {
  name: 'six',
  age: 13,
  ['my'+'work']: 'it coder'
}
```

# SFC

单文件组件: Single-File Component

![](https://s.sixmillions.cn/img/2023/03/25/171621hryh.png)

# 补充：模块

> [彻底搞清楚javascript中的require、import和export - 最骚的就是你 - 博客园 (cnblogs.com)](https://www.cnblogs.com/libin-1/p/7127481.html)

# 开发插件

![](https://s.sixmillions.cn/img/2023/03/25/174810iru5.png)
