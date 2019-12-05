# webpack

```js
打包压缩混淆代码工具
官网:webpack.js.org
打包:npm run build  //vue-cli中打包
安装简写:npm i -D webpack webpack-cli

安装:
npm install --save-dev webpack
npm install --save-dev webpack@<版本号>
    
打包本地运行方法:
 nodejs:	npm install http-server -g
打包后目录:http-server
后端口运行即可 要在地址后面加 index.html#/

http://www.pianshen.com/article/1996316392/
```

## 入口出口

```js
创建webpack.config.js文件中

const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js', //入口
  output: {
    path: path.resolve(__dirname, 'dist'), //出口绝对路径拼接
    filename: 'my-first-webpack.bundle.js'
  }
};
```



## vue_cli打包项目

> 为什么要打包？
>
> ​	浏览器不认识.vue文件
>
> ​	代码需要被压缩
>
> ​	浏览器不认识很多ES6的语法 例如： import xxx from '路径'，要不要把ES6翻译成ES5让浏览器认识
>
> ​	我在index.vue里导入了 a.js  a.js 也有可能导入了b.js  然后b.js里也导入了c.js  有多重依赖，我们需要把这些路径好好管理并解决依赖问题，要记得先要导入c，再导入b，再导入a，自己要注重导入顺序
>
> ​    .......
>
> 如果自己做，挺麻烦的，这些东西通过webpack可以帮我们解决
>
> vue_cli其实是基于webpack的，webpack如果自己用有一堆要配置，比较复杂。所以vue官方提供了一个      vue-cli这样的东西，它可以方便我们不用做什么配置，就能帮我们打包项目

- 命令：

```node
npm run build
```

- 项目上线

> 把打包后的代码，上传到自己服务器的根目录就能通过这个服务器的ip地址来访问了





## webpack的介绍

- `webpack` 就是一个打包工具，类似的工具还有 `gulp` 这之类的
- 现在要打包都是用 `webpack` 会在一些老项目里遇到别的工具
- 下载webpack模块

```npm
npm i -D webpack webpack-cli
```

- -D 是 --save-dev 的缩写

> 如果安装慢用淘宝镜像（cnpm）



- 打包命令

```$
npx webpack
```

> webpack会帮你打包src里面的文件，默认找的是src里index.js
>
> 它只会打包index.js这一个文件，如果发现index.js里面有对其他文件的依赖，那么才会其他文件
>
> 它也可以打包模块化的JS，让浏览器认识





## 入口和出口

- 入口： 打包从哪个文件开始打，默认从src里的index.js开始

- 出口：打包后生成到哪，默认是dist文件夹里的main.js

- 修改步骤：

    - 在项目根目录（也就是跟package.json同级）的地方，新建一个文件 `webpack.config.js` （webpack的配置文件）

    

### 入口

[传送门](https://www.webpackjs.com/concepts/#%E5%85%A5%E5%8F%A3-entry-)

- 在文件里写以下代码

```js
  module.exports = {
  
      //打包入口,以src里面的xx.js为入口
      entry:"./src/xx.js"
}
```

- 打包时要带上这个配置文件

```npm
npx webpack --config webpack.config.js
```

- 这个意思是打包，并且用webpack.config.js的配置来打包
- 默认它其实就会去找 webpack.config.js 这个文件来作为配置
- 在webpack老版本的时候，必须自己制定这个配置文件
- 也可以不叫 `webpack.config.js` 叫别的名字，叫别的名字必须制定配置文件的名字



### 出口

[传送门](https://www.webpackjs.com/concepts/#%E5%87%BA%E5%8F%A3-output-)

- webpack.config.js

```js
output:{
    //路径
    path:'',
    //文件名
    filename:''
}
```



- 最终配置代码

```js
const path = require('path')

module.exports = {

    //打包入口
    entry:"./src/index.js",

    //打包出口
    output:{

        // 打包后的路径，默认是./dist
        // 打包后的路径必须写绝对路径
        path: path.resolve(__dirname,'./dist'),
        //打包后的文件名，默认叫main.js
        filename:'index.js'
    }
}
```



## scripts作用

- npm run 后面要接 scripts 里面的名字
- npm run build 它就相当于找到 package.json 里面的 scripts 里面的 build ，再把 build 对应的代码执行起来
- 总结作用：它的作用可以把一串复杂的命令打包起来，然后要运行，只要 npm run xxx就行了

```js
package.json

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "buildcustom": "webpack --config webpack.custom.config.js", //指定打包配置文件
    "build": "webpack",
    "watch": "webpack --watch",
    "dev2": "webpack-dev-server --compress --hot --port 5000 --open --contentBase src",
    "server": "node server.js"
  },
      
--compress  //gzip压缩
--hot 		//热更新,保存自动更新页面
--port 5000 //端口
--open 		//npm run dev 后自动打开页面
--contentBase src", //指定默认打开路径
```



## --save 和 --save-dev 区别

- --save 会把你下载的第三方包信息保存到 `dependencies`
- --save-dev 会把你下载的第三方包保存到 `devDependencies`
- npm i 插件名 默认相当于  npm i --save 插件名



## devDependencies和 dependencies区别

- devDependencies ：开发时需要，正式上线不需要

    - 所以对于这类插件，记得下载时一定要用 --save-dev 的命令

- dependencies： 里面的插件代表开发打包后也会要用

    - 直接npm i 就行了，因为npm i 默认就是 --save
    - 如果是cnpm i 那么必须自己加 --save

    

# 打包插件

## 打包html

[传送门](https://www.webpackjs.com/guides/output-management/#%E8%AE%BE%E5%AE%9A-htmlwebpackplugin)

- webpack默认只能打包js

- 如果要打包html，还得下载一个html的插件

- 并且要修改配置文件，不能只是独立的html，还得给一个js的入口文件

- 步骤：

    - ```bash
        npm install --save-dev html-webpack-plugin
        ```

    - 修改webpack.config.js

    - 先导入

    - ```diff
        const HtmlWebpackPlugin = require('html-webpack-plugin');
        ```

    ```js
    plugins: [
          new HtmlWebpackPlugin({
                //title设置打包后的html标题
                title: '测试'
              template:'./src/index.html' //导入自己的html;
            })
        ],
    ```

    - 会自动把入口文件的js  打包后的js文件 导入到打包后的html里面来
    - 如果只是写title，它会帮你创建新的空的html,并导入js依赖
    - 如果写template跟路径，就代表找到template对应的路径的html文件，把它打包起来，并添加依赖



## 打包css

- webpack默认只认识.js文件，如果想打包解析别的文件格式，就需要对应的loader

- 下载loader

    - style-loader  css-loader

    - ```bash
        npm install --save-dev style-loader css-loader
        ```

    - webpack.config.js

    - ```js
            module: {
                rules: [
                    {
                        test: /\.css$/,
                        use: [
                            'style-loader',
                            'css-loader'
                        ]
                    }
                ]
            }
        ```

        



## 打包图片

- 默认不支持打包图片

- 所以要下载对应loader

- ```js
    npm install --save-dev file-loader
    ```

- ```diff
    webpack.config.js
    
    
    const path = require('path');
    
    module.exports = {
      entry: './src/index.js',
      output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
      },
      module: {
        rules: [
          {
            test: /\.css$/,
            use: [
              'style-loader',
              'css-loader'
            ]
          },
    +       {
    +         test: /\.(png|svg|jpg|gif)$/,
    +         use: [
    +           'file-loader'
    +         ]
    +       }
          ]
        }
      };
    ```



## webpack打包vue

- 本质是跟打包css是一样的，都是要先下载一个loader
- 然后改配置文件

# 每次打包清空dist文件夹

[中文传送门](https://www.webpackjs.com/guides/output-management/#%E6%B8%85%E7%90%86-dist-%E6%96%87%E4%BB%B6%E5%A4%B9)

[英文官网](https://webpack.js.org/guides/output-management/#cleaning-up-the-dist-folder)

- 下载清空的插件

    - ```bash
        npm install clean-webpack-plugin --save-dev
        ```

- webpack.config.js

    ```js
    const { CleanWebpackPlugin } = require('clean-webpack-plugin');
    ```

    ```diff
     plugins: [
       //清空 dist 文件夹
       new CleanWebpackPlugin()
    ]
    ```



# 用webpack模拟出vue-cli

- 创建一个项目文件夹，进来输入 npm init -y
- 创建src文件夹，里面放main.js
- 创建public文件夹，里面放index.html
- 下载webpack和webpack-cli
- 写 webpack.config.js
    - 配置入口 （./src/main.js）
    - 配置出口
    - 配置使用自己的html
        - 下载html插件
        - 改配置，配置的template里面写./public/index.html
- 下载css-loader
- 下载vue-loader
- main.js里写以前那些vue的初始化代码

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin');
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
  //入口
  entry: "./src/main.js",
  //出口
  output: {
    path: path.resolve(__dirname, './dist/'),
    filename: 'index.js' //出口文件名
  },

  devServer: {
    // 设置这个微型服务器的根目录
    contentBase: './dist'
  },

  module: {
    rules: [
      {
        test: /\.vue$/, //vue模块
        loader: 'vue-loader'
      },
      {
        test: /\.css$/, //css模块
        use: [
          'style-loader',
          'css-loader'
        ]
      }
    ]
  },

  plugins: [ //插件管理
    new HtmlWebpackPlugin({
      //title设置打包后的html标题
      template: "./public/index.html"
    }),
    new VueLoaderPlugin()
  ],
  // production，会打包的慢一点，它里面会压缩代码
  // development，打包相对快一点，它里面的代码不压缩
  mode:"production"
}
```



## webpack -dev-server

[传送门](https://www.webpackjs.com/guides/development/#%E4%BD%BF%E7%94%A8-webpack-dev-server)

为你提供了一个简单的 web server，并且具有 live reloading(实时重新加载) 功能

- 安装

    - ```js
        npm install --save-dev webpack-dev-server
        
        https://blog.csdn.net/hdchangchang/article/details/80112593
        ```

- 配置webpack.config.js

    - ```diff
        devServer: {
           contentBase: './dist'
         },
        ```

- 运行起来

    - ```bash
        npx webpack-dev-server --open
        ```

- 每次这么运行非常麻烦，所以这个命令写在package.json的`scripts`里面

- 我们就用 npm run xxx 运行

### 参数解读:

```js
webpack-dev-server有三种配置方式，有配置文件方式、package.json方式和纯node的API实现方式，
```

```js
devServer: {
    contentBase: path.join(__dirname, "public")"./",//本地服务器所加载的页面所在的目录
    historyApiFallback: true,//不跳转; 应对返回404页面时定向到特定页面用的
    historyApiFallback:{
       rewrites:[
          {from:/./,to:'/404.html'}
       ]
  	},
    host:'0.0.0.0', //服务器的主机号，默认是localhost，
    port:7000,//端口号
    inline: true,//实时刷新
    hot:true,//热替换
    compress:true,//gzip压缩
    overlay: true, //浏览器输出编译错误的，默认是关闭的，需要手动打开：
    stats: "errors-only" ,//编译的时候shell上的输出内容
    open:true, //dev server将直接打开浏览器
    proxy: {
        "/api": {
            target: "http://localhost:3000",
            changeOrigin: true,
            pathRewrite: {"^/api" : ""}如果不希望”api”在传递中被传递过去，可以使用rewrite的方式实现：
        }
    }，//重定向
    
    publicPath:'/assets/'//编译后文件的路径 http://localhost:8080/assets/bundle.js
 }
————————————————
原文链接：https://blog.csdn.net/franktaoge/article/details/80083317
```



## webpack跨域

```js
webpack的devServer.proxy就是使用了非常强大的 http-proxy-middleware 包


 // 开发配置
    dev: {
        assetsRoot: path.resolve(__dirname, "../dist"),
        // 静态资源文件夹
        assetsSubDirectory: "static",
        // 发布路径
        assetsPublicPath: "/",
        // Various Dev Server settings
        host: "localhost",
        // dev-server监听的端口
        port: 8080,
        autoOpenBrowser: true,
        proxyTable: {
            //综合收件
            '/api': {
                target: "http://www.baidu.com", //开发环境
                changeOrigin: true,
                pathRewrite: {
                    '^/api': 'api'
                }
            },
        }
        //是否使用 cssSourceMap
        cssSourceMap: false
    }

作者：htyin
链接：https://juejin.im/post/5cb3d6ecf265da03b57b4b21
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

# webpack文件

## package.json

```json
{
  "name": "webpack-basic",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "buildcustom": "webpack --config webpack.custom.config.js",
    "build": "webpack",
    "watch": "webpack --watch",
    "dev2": "webpack-dev-server --compress --hot --port 5000 --open --contentBase src",
    "dev": "webpack-dev-server",
    "server": "node server.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {	//开发使用
    "webpack-dev-server": "^3.3.1"
  },
  "dependencies": {		//上线使用
    "@babel/polyfill": "^7.4.4",
  }
}
```

## webpack.config.js

```json
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const CleanWebpackPlugin = require('clean-webpack-plugin')
const CopyWebpackPlugin = require('copy-webpack-plugin')
const webpack = require('webpack')

// webpack的配置文件遵循着CommonJS规范
module.exports = {
  entry: './src/main.js',  //入口
  output: {					//出口
    // path.resolve() : 解析当前相对路径的绝对路径
    // path: path.resolve('./dist/'),
    // path: path.resolve(__dirname, './dist/'),
    path: path.join(__dirname, './dist/'),
    filename: 'bundle.js',
    publicPath: '/'
  },
  mode: 'production',
  // 开启监视模式, 此时执行webpack指令进行打包会监视文件变化自动打包
  // watch: true
  devServer: {
    open: true,
    hot: true,
    compress: true,
    port: 3000,
    // contentBase: './src'
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'index.html',
      template: './src/index.html'
    }),
    new CleanWebpackPlugin(),
    new CopyWebpackPlugin([
      {
        from: path.join(__dirname, 'assets'),
        to: 'assets'
      }
    ]),
    new webpack.BannerPlugin('黑马程序员真牛biubiu!')
  ],
  module: {
    rules: [
      {
        test: /\.css$/,
        // webpack读取loader时 是从右到左的读取, 会将css文件先交给最右侧的loader来处理
        // loader的执行顺序是从右到左以管道的方式链式调用
        // css-loader: 解析css文件
        // style-loader: 将解析出来的结果 放到html中, 使其生效
        use: ['style-loader', 'css-loader']
      },
      { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] },
      { test: /\.s(a|c)ss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
      {
        test: /\.(jpg|jpeg|png|bmp|gif)$/,
        use: {
          loader: 'url-loader',
          options: {
            limit: 5 * 1024,
            outputPath: 'images',
            name: '[name]-[hash:4].[ext]'
          }
        }
      },
      exclude: /node_modules/,
      }
    ]
  },
  // devtool: 'cheap-module-eval-source-map'
}
```

