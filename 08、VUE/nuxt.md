https://www.nuxtjs.cn/

https://zh.nuxtjs.org/examples

## 中间件

### 1.路由中间件

1. middleware中创建js文件；
2. nuxt.config.js注册中间件；

```js
nuxt.config.js

export default {
  router: {
    middleware: ['class']
  }

```

```js
middleware/class.js

export default function ({ store, route }) {
  store.commit('class/SetClass', route.name)
}
```

### 2.指定中间件

1. middleware中创建js文件；
2. 组件中引入；

```js
// middleware/class.js

export default function ({ store, route }) {
  store.commit('class/SetClass', route.name)
}
```

```js
// home.vue

<template>
  <div>...</div>
</template>
<script>
export default {
  middleware: 'class',
}
</script>
```

### 3.匿名

1. 组件中直接使用；

```js
<template>
  <div>
  </div>
</template>
<script>
export default {
  middleware({ store }) {
    store.commit('analytics/increment')
  }
}
</script>
```

