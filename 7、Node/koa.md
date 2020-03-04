### 一、![\color{red}{Koa}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7BKoa%7D) 简介

文档地址：[https://koa.bootcss.com](https://links.jianshu.com/go?to=https%3A%2F%2Fkoa.bootcss.com%2F)

​    ![\color{red}{Koa}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7BKoa%7D) 是一个新的 web 框架，由 Express 幕后的原班人马打造， 致力于成为 web 应用和 API 开发领域中的一个更小、更富有表现力、更健壮的基石。 通过利用 async 函数，Koa 帮你丢弃回调函数，并有力地增强错误处理。 Koa 并没有捆绑任何中间件， 而是提供了一套优雅的方法，帮助您快速而愉快地编写服务端应用程序。

### 二、![\color{red}{Koa}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7BKoa%7D) 之hello world

- **（1）新建koa-demo文件夹，初始化package.json**

```kotlin
      npm init -y
```

- **（2）安装Koa模块**

```undefined
      npm i koa -S
```

- **（3）在项目根目录新建app.js，app.js代码如下：**

```tsx
    // 导入koa模块
    const Koa = require('koa');
    // 创建koa的实例app
    const app = new Koa();

    app.use(async ctx => {
        ctx.body = "Hello World"
    })
    // 监听端口
    app.listen(3000, () => {
        console.log("服务器已启动，http://localhost:3000");
    })
```

- **（3）使用node命令启动服务器，并访问本地地址端口3000**

```undefined
    node app
```

### 三、服务器自动重新部署

- **（1）、 nodejs开发辅助工具![\color{red}{nodemon}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7Bnodemon%7D)**
       修改代码后，需要重新启动 Koa应用，所做的修改才能生效。若之后的每次代码修改都要重复这样的操作，势必会影响开发效率，使用了nodemon后，它会监测项目中的所有文件，一旦发现文件有改动，![\color{red}{nodemon}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7Bnodemon%7D)会自动重启应用
- **（2）全局安装nodemon**

```undefined
   npm i nodemon -g
```

- **（3）启动服务的时候用nodemon app.js 代替node app.js**

```undefined
    nodemon app
```

### 四、Koa中间件

- **（1）什么是koa中间件**
       koa对网络请求采用了中间件的形式处理,中间件可以介入请求和相应的处理,是一个轻量级的模块,每个中间负责完成某个特定的功能。中间件的通过next函数联系,执行next()后会将控制权交给下一个中间件,如果没有中间件没有执行next后将会沿路折返,将控制权交换给前一个中间件。
       每个中间件都是一个函数(不是函数将报错)，接收两个参数，第一个是![\color{red}{ctx}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7Bctx%7D)上下文对象，另一个是![\color{red}{next}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7Bnext%7D)函数
- **（2）中间件的使用**

```ruby
    app.use((ctx, next) => {
        // 在ctx上放入username,后面的所有请求的ctx里都会有username这个变量
        ctx.username = '我是Grayly';
        // 处理完之后放行,不使用next()的话,程序会被挂起来不动了
        next();
    })
```

- **（3）中间件有先后顺序**

### 五、Koa路由配置

```js
const Router = require('koa-router')
const router = new Router()

router.get('/user', ctx => {
    ctx.body = '哈哈哈'
})

module.exports = router
```

```js
// 导入koa模块
const Koa = require('koa');
// 创建koa的实例app
const app = new Koa();

const user = require('./router/user')
app.use(user.routes())
// 监听端口
app.listen(3000, () => {
    console.log("服务器已启动，http://localhost:3000");
})
```



- **（1）安装koa-router**

```undefined
    npm i koa-router -D
```

- **（2）导入koa-router模块并实例化**

```jsx
    // 导入koa-router模块
    const Router = require('koa-router');
    // 创建koa-router的实例router
    const router = new Router();
```

- **（3）配置，并访问本地地址端口3000**

```php
    router.get('/', ctx => {
        ctx.body = "哈哈哈"
    })
    app.use(router.routes());
```

- （4）koa-router 提供了 .get、.post、.put 和 .del 接口来处理各种请求，但实际业务上，我们大部分只会接触到 POST 和 GET，所以接下来只针对这两种请求类型来说明。

  - （4.1）get：用于接收GET请求

  ```php
      router.get('/get', ctx => {
          ctx.body = "哈哈哈"
      })
      app.use(router.routes());
  ```

  - （4.2）post：用于接收POST请求

  ```php
      router.post('/', ctx => {
          ctx.body = "哈哈哈"
      })
      app.use(router.routes());
  ```

  - （4.3）all：用于接收GET与POST请求

  ```php
      router.all('/', ctx => {
          ctx.body = "哈哈哈"
      })
      app.use(router.routes());
  ```

- （5）获取请求参数

  - （5.1）获取get请求参数：`ctx.query`

  ```dart
        router.get('/get', ctx => {
            ctx.body = ctx.query
        })
  ```

  - （5.2）获取post请求参数：

    ```
    ctx.request.body
    ```

    - 当用 post 方式请求时，我们会遇到一个问题：post 请求通常都会通过表单或 JSON 形式发送，而无论是 Node 还是 Koa，都 没有提供 解析 post 请求参数的功能。
    - **获取post请求需要使用koa-body模块**

    ```undefined
      npm i koa-body --save
    ```

    ```dart
        router.get('/get', ctx => {
            ctx.body = ctx.request.body
        })
    ```

  - （5.3）使用中间件封装请求参数：**把get请求参数和post请求参数都放入params对象**

  ```jsx
        app.use((ctx, next) => {
            ctx.params = {
                ...ctx.query,
                ...ctx.request.body
            }
            next();
        });
  ```

### 六、设置静态目录![\color{red}{koa-static}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7Bkoa-static%7D)

- **（1）在目录中创建目录public，在public下创建文件demo.html，访问[http://localhost:3000/public/demo.html](https://links.jianshu.com/go?to=http%3A%2F%2Flocalhost%3A3000%2Fpublic%2Fdemo.html)是无法访问得到，因为我们还没有设置静态资源目录,设置静态资源目录要用到koa-static模块**
- **（2）安装koa-static**

```cpp
    npm i koa-static -D
```

- **（3）在app.js里加入如下代码**

```php
    const koaStatic = require('koa-static');
    app.use(koaStatic(__dirname + '/public'));
```

### 七、使用模板引擎![\color{red}{koa-views}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7Bkoa-views%7D)

- **（1）安装koa-views**

```undefined
    npm i koa-views -D
    npm i underscore -D
```

- **（2）模板编写：在根目录创建views目录，在views目录下创建tpl.html,代码如下**

```xml
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
    </head>
    <body>
        <h3><%=title %></h3>
    </body>
    </html>
```

- **（3）在app.js配置模板引擎中间件**

```jsx
  const path = require('path');
  const views = require("koa-views");
  app.use(views(path.join(__dirname, "views"), {
    map: {
      html: 'underscore'
    }
  }));
```

- **（4）使用模板引擎**

```dart
    router.get("/html", async ctx => {
        await ctx.render("tpl", {
            title: "Grayly"
        })
    })
```

### 八、Vue SSR（vue服务器渲染）

- **（1）安装vue和vue服务器渲染插件**

```undefined
  npm install vue vue-server-renderer -S
```

- **（2）渲染**

```tsx
    router.get('/ssr', async ctx => {
        第 1 步：创建一个 Vue 实例
        const Vue = require('vue')
        const app = new Vue({
            template: `<div>Hello World</div>`
        })
        第 2 步：创建一个 renderer
        const renderer = require('vue-server-renderer').createRenderer();
        第 3 步：将 Vue 实例渲染为 HTML
        renderer.renderToString(app, (err, html) => {
            if (err) throw err
            console.log(html)
            ctx.body = html;
            // => <div data-server-rendered="true">Hello World</div>
        })
    })
```

### 九、![\color{red}{Koa}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7BKoa%7D) 跨域设置

- **使用中间件编写跨域设置**

```dart
    app.use((ctx, next) => {
    // 设置允许跨域
        ctx.set("Access-Control-Allow-Origin", "*");
        ctx.set("Access-Control-Allow-Methods", "PUT, POST, GET, DELETE, OPTIONS");
        // 请求头设置
        ctx.set(
            "Access-Control-Allow-Headers",
            `Content-Type, Content-Length, Authorization, Accept, X-Requested-With , yourHeaderFeild,x-token,sessionToken,token`
        );
        if (ctx.method == "OPTIONS") {
            ctx.body = 200;
        } else {
            next();
        }
    })
```

