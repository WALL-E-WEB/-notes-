# manifest

# web worker

线程

# service worker

模拟服务器 可操作缓存

## 生命周期 

	1.	install : 注册成功时触发;ws.js发生改变｀install｀会重新出发
 	2.	activate :　激活时触发；当前状态结束时才能出发,否则等待!
 	3.	fetch：事件发送请求时触发，主要用于操作缓存；

```js
this.addEventListener('install',e=>{
    
    e.waitUntil(this.skipWaiting()) 
})

this.addEventListener('activate',e=>{
    //激活后, 立即获取控制权
     e.waitUntil(this.clients.claim())
})

this.addEventListener('fetch',e=>{
    //请求发送的时候触发
})
```

this.skipWaiting() : 跳过等待,直接进入activate;返回promise对象;

event.waitUntil() : 防止skipWaiting未执行;

```js
e.waitUntil(this.skipWaiting()) 
```

# fetch api



# caches storage