# manifest

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <!-- 引入了引用程序清单文件 -->
    <link rel="manifest" href="manifest.json" />
  </head>
  <body>
    <h1>hello pwa</h1>
  </body>
</html>
```

```json
{
  "name": "APP-PWA",
  "short_name": "APP",
  "start_url": "/index.html",
  "icons": [
    {
      "src": "images/logo.png",
      "sizes": "144x144",
      "type": "image/png"
    }
  ],
  "background_color": "skyblue",
  "theme_color": "yellow",
  "display": "standalone"
}
```



# web worker

线程;用http-server模拟运行

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <script>
      console.log('start')

      // 1. 创建一个web worker
      const worker = new Worker('work.js')
      //接收
      worker.addEventListener('message', e => {
        console.log(e.data)
      })

      console.log('end')
    </script>
  </body>
</html>
```

```js

// 注意：web worker是一个独立的进程，不能操作DOM和BOM
// 适合做大量的运算
let total = 0
for (var i = 0; i < 100000000; i++) {
  total += i
}

// 发消息给主线程，把结果给他
self.postMessage({ total: total })

```



# service worker

模拟服务器 可操作缓存

## 生命周期 

	1.	install : 注册成功时触发;ws.js发生改变｀install｀会重新出发
 	2.	activate :　激活时触发；当前状态结束时才能出发,否则等待!
 	3.	fetch：事件发送请求时触发，主要用于操作缓存；

```js
self.addEventListener('install', event => {
  // 111
  console.log('install', event)
  // 会让service worker跳过等待，直接进入到activate状态
  // 等待skipWaiting结束，才进入到activate
  event.waitUntil(self.skipWaiting())
})

self.addEventListener('activate', event => {
  console.log('activate', event)

  // 表示service worker激活后，立即获取控制权
  event.waitUntil(self.clients.claim())
})

// 注释：fetch事件会在请求发送的时候触发
self.addEventListener('fetch', event => {
  console.log('fetch', event)
})

```

this.skipWaiting() : 跳过等待,直接进入activate;返回promise对象;

event.waitUntil() : 防止skipWaiting未执行;

```js
e.waitUntil(this.skipWaiting()) 
```

监测是否支持

```js
window.addEventListener('load', () => {
        // 2. 能力检测
        if ('serviceWorker' in navigator) {
          navigator.serviceWorker
            .register('./sw.js')
            .then(registration => {
              console.log(registration)
            })
            .catch(err => {
              console.log(err)
            })
        }
      })
```



# fetch api



# caches storage

静态资源缓存优先;

http请求网路优先;

```js

this.addEventListener('install',async e=>{
    
    
    e.waitUntil(this.skipWaiting()) 
})

//主要清除旧的缓存
this.addEventListener('activate',e=>{
    //激活后, 立即获取控制权
     e.waitUntil(this.clients.claim())
})

this.addEventListener('fetch',e=>{
    //请求发送的时候触发
})
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <!-- 引入了引用程序清单文件 -->
    <link rel="manifest" href="manifest.json" />
    <link rel="stylesheet" href="index.css" />
  </head>
  <body>
    <h1>hello pwa</h1>
    <script>
      window.addEventListener('load', async () => {
        if ('serviceWorker' in navigator) {
          try {
            const registration = await navigator.serviceWorker.register(
              './sw.js'
            )
            console.log('注册成功', registration)
          } catch (e) {
            console.log('注册失败')
          }
        }
      })

      /* 
        如果页面一进来，我们发下用户没有联网，给用户一个通知
      */
      if (Notification.permission === 'default') {
        Notification.requestPermission()
      }
      if (!navigator.onLine) {
        new Notification('提示', { body: '你当前没有网络，你访问的是缓存' })
      }

      // offline: 断线
      window.addEventListener('online', () => {
        new Notification('提示', {
          body: '你已经连上网络了，请刷新访问最新的数据'
        })
      })
    </script>
  </body>
</html>

```

```js
// 主要就是缓存内容
const CACHE_NAME = 'cache_v2'
self.addEventListener('install', async event => {
  // 开启一个cache, 得到了一个cache对象
  const cache = await caches.open(CACHE_NAME)
  // cache对象就可以存储的资源
  // 等待cache把所有的资源存储起来
  await cache.addAll(['/', '/images/logo.png', '/manifest.json', '/index.css'])
  await self.skipWaiting()
})

// 主要清除就的缓存
self.addEventListener('activate', async event => {
  // 会清除掉旧的资源, 获取到所有的资源的key
  const keys = await caches.keys()
  keys.forEach(key => {
    if (key !== CACHE_NAME) {
      caches.delete(key)
    }
  })
  await self.clients.claim()
})

// 注释：fetch事件会在请求发送的时候触发
// 判断资源是否能够请求成功，如果能够请求成功，就响应成功的结果，如果断网，请求失败了，读取caches缓存即可
self.addEventListener('fetch', async event => {
  // 请求对象
  // 给浏览器响应
  event.respondWith(networkFirst(event.request))
})

// 网络优先
async function networkFirst(req) {
  try {
    // 先从网络读取最新的资源
    const fresh = await fetch(req)
    return fresh
  } catch (e) {
    // 去缓存中读取
    const cache = await caches.open(CACHE_NAME)
    const cached = await cache.match(req)
    return cached
  }
}

```



# Notification

```js
if (Notification.permission === 'default') {
  Notification.requestPermission()
}
if (!navigator.onLine) {
  new Notification('提示', { body: '你当前没有网络，你访问的是缓存' })
}

// offline: 断线
window.addEventListener('online', () => {
  new Notification('提示', {
    body: '你已经连上网络了，请刷新访问最新的数据'
  })
})
```

