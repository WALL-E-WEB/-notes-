# MVVM

```js
mvvm是一种软件架构设计模式
v视图层
m数据层
vm视图数据模型和展现逻辑
```



# 深入响应式原理

1. 什么是深入响应式原理:（双向绑定原理）

    ```js
    深入响应式原理是利用了数据劫持和订阅发布的模式, 当数据模型发生改变的时候， 视图就会响应的进行更新
    
    其中响应式原理是利用
    Object.defineproperty中的geter,seter来进行数据劫持,
    当取值时触发get（）；
    当赋值时触发set（）
    vue在这两个方法中做依赖收集和派发更新的。
    依赖收集：收集监管data中的数据；
    派发更新：通知watch更新视图
    
    如何防止重复收集：
    	只有watch在执行get时，才会被收集。
    
    如何防止重复更新：
    	在queueWatcher中做了去重合异步更新
        
    
    http://www.52codes.net/develop/javascript/57691.html
    
    什么叫数据劫持:
    	Object.defineProperty中的getter/setter ， 数据改变就执行watcher
        
    订阅发布:事件
    
    订阅:事件声明的vm.on发布,触发的触发vm.emit
    
    非响应式情况:
    data以外定义的属性,
    
    非响应式属性如何变成响应式属性:
    	思路:将非响应式属性合并到响应式属性身上
        解决: 利用了Vue提供的 Vue.set/this.$set(vm.dataattr,prop,value)
    
    vue.set的原理:
    	是利用object.assign()合并对象
    ```

# vue-router路由

```js
Vue-Router 是vue官方的路由管理器。
通过路由地址的变换展现不同的页面;
路由导航有两种:
	声明式导航:router-link
    编程式导航:router.push(path:'url')

通过:router-view标签作为 页面展示区;





```

## 路由的原理

#### abstract模式:

```js
服务器端和Node.js. 如果没有浏览器API，路由器将自动强制进入此模式
```

#### hash模式

```
1.就是指 url 尾巴后的 # 号以及后面的字符, 
	请求的时候不会被包含在 http 请求中 只会携带#之前的，
	所以每次改变hash不会重新请求加载页面
2.hash 改变会触发 hashchange 事件
3.hash变化会被浏览器记录，浏览器的前进和后退都能用。
3.能兼容到ie8

监听事件:hashchange事件

https://developer.mozilla.org/zh-CN/docs/Web/API/Location
```

#### history模式

```js
1.页面请求时会带上整个链接，所以后台需要做相对处理，不然返回404
2.不带#号,请求时是整个链接,所以需要服务器的支持把所有路由都重定向到根页面
3.怕刷新,刷新请求,需要服务端配合;

监听事件:popstate

history.back()
history.forward()
history.go()
```

## 路由钩子

### 	路由解析流程?

```js
1、导航被触发
2、在失活的组件里调用离开守卫 beforeRouterleave
3、调用全局的 beforeEach 守卫
4、在重用的组件里调用 beforeRouteUpdate 守卫
5、在路由配置里调用 beforEnter //路由独享
6、解析异步路由组件
7、在被激活的组件里调用 beforeRouteEnter
8、调用全局的 beforeResolve 守卫
9、导航被确认
10、调用全局的 afterEach 钩子
11、触发 DOM 更新
12、在创建好的实例调用 beforeRouteEnter 守卫中传给 next 的回调函数

作者：woniu12
链接：https://www.jianshu.com/p/96cfc1b9ff21
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

 ![img](../image/20190616165857285.png) 

1. 全局守卫

    - router.beforeEach   全局前置守卫 

        ```js
        const router = new VueRouter({ ... })
          router.beforeEach((to, from, next) => {
          // ...
        })
        ```

        `to: Route:`即将要进入的目标 路由对象

        `from: Route:` 当前导航正要离开的路由

        next: Function:`一定要调用该方法来`resolve`这个钩子。执行效果`依赖 next 方法的调用参数。

    - router.beforeResolve 全局解析守卫

        ```js
        在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后，解析守卫就被调用。
        ```


    -  router. afterEach 全局后置钩子

    ```js
    不会接受 next 函数也不会改变导航本身：
    router.afterEach((to, from) => {
      // ...
    })
    ```

    

3. 路由独享守卫

    -  beforeEnter  

    ```js
    const router = new VueRouter({
      routes: [
        {
          path: '/foo',
          component: Foo,
          beforeEnter: (to, from, next) => {
            // ...
          }
        }
      ]
    })
    ```

    

4. 组件内守卫

    -  beforeRouteEnter  不能获取组件实例this;next(vm=>{可获取实例})
    -  beforeRouteUpdate  
    -  beforeRouteLeave 

```js
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  //不过，你可以通过传一个回调给 next来访问组件实例。
  //在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数。
  beforeRouteEnter (to, from, next) {
    next(vm => {
      // 通过 `vm` 访问组件实例
    })
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
    
    //  该组件离开跳转到另外的组件时触发该钩子,常应用于用户表单，当用户填了一部分内容，需要提醒用户是否离开页面
 beforeRouteLeave(to, from, next){
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```

## vue-router是如何响应 路由参数变化的:

```js
https://blog.csdn.net/weixin_41639609/article/details/88721627 
watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
    }
  }
```

```js
 beforeRouteUpdate (to, from, next) {
    // react to route changes...
    // don't forget to call next()
  }
```

## $route和$router的区别

```
答：$route是“路由信息对象”，包括path，params，hash，query，fullPath，matched，name等路由信息参数。而$router是“路由实例”对象包括了路由的跳转方法，钩子函数等。
```



# keep-alive

```js
是 Vue 内置的一个组件,防止重新渲染,把组件缓存;

参数解释
include - 字符串或正则表达式，只有名称匹配的组件会被缓存
exclude - 字符串或正则表达式，任何名称匹配的组件都不会被缓存

<!-- 逗号分隔字符串，只有组件a与b被缓存。 -->
<keep-alive include="a,b">
  <component></component>
</keep-alive>

<!-- 正则表达式 (需要使用 v-bind，符合匹配规则的都会被缓存) -->
<keep-alive :include="/a|b/">
  <component></component>
</keep-alive>

<!-- Array (需要使用 v-bind，被包含的都会被缓存) -->
<keep-alive :include="['a', 'b']">
  <component></component>
</keep-alive>

```



# vue高阶组件

 [http://hcysun.me/2018/01/05/%E6%8E%A2%E7%B4%A2Vue%E9%AB%98%E9%98%B6%E7%BB%84%E4%BB%B6/](http://hcysun.me/2018/01/05/探索Vue高阶组件/) 

 https://blog.csdn.net/z609373067/article/details/81258966 

```js
function WithConsole (WrappedComponent) {
  return {
    mounted () {
      console.log('I have already mounted')
    },
    props: WrappedComponent.props,
    render (h) {
      const slots = Object.keys(this.$slots)
        .reduce((arr, key) => arr.concat(this.$slots[key]), [])
        .map(vnode => {
          vnode.context = this._self
          return vnode
        })

      return h(WrappedComponent, {
        on: this.$listeners,
        props: this.$props,
        // 透传 scopedSlots
        scopedSlots: this.$scopedSlots,
        attrs: this.$attrs
      }, slots)
    }
  }
}
```

