# NodeJS

是一种不需要在浏览器执行的技术;

​	1.内置了谷歌的V8引擎-高效率的执行 js代码;

​	2.内置模块 就是写好的 Js代码,类似于jquery.js;

数据库,微服务(Docker);

ipconfig 查看ip地址

cls 清屏

## require-加载规则

```js
require('模块标识')
	1.缓存优先,
    2. 模块
    	1.第三方模块:
		2.核心模块:已转为二进制,本质是文件
		3.引用:'./xxx';
```

## npm

```js
cnpm-淘宝
npm.taobao.org
npm install --global cnpm   //使用淘宝镜像 后面使用cnpm

npm install 包名 --registry=https://registry.npm.taobao.org

加载改为:
npm config set registry https://registry.npm.taobao.org

npm init
	npm init -y //跳过导向一步到位,直到创建依赖项创建

npm install --save 包名 下载并保存依赖项
	npm i -S 包名
	
npm uninstall --save 包名  删除
	npm un -S 包名

npm 命令 --help

查看是否成功
npm config list
```



## 文件系统

#### 文件删除

```js
const fs = require('fs');

fs.unlink("./tex.txt",err)=>{
    if(err !=null){
        console.log(err.message);
    }else{
        console.log("成功");
    }
}
```

#### 文件读取

```js
const fs = require('fs'); //异步
	第一个参数:读取文件路径;
	第二个参数是:一个回调函数
    	成功:
			data 数据
            err	错误对象  err.message;
fs.readFile('url',{encoding:'utf-8'},(err,data)=>{
	if(err == null){
		console.log(data);
	}else {
		cosole.log(err.message);
	}
});



url是相对于小黑框的执行路径而言;
url = nodejs执行所在的位置+url;

	问题:相对路径不准确,绝对不可移动;
	解决:
	__dirname	执行js文件 所在 的绝对路径//两个下划线
    __filename	执行js文件 本身的绝对路径//两个下划线
let filePath = _dirname+'./aa.txt';
```

#### writeFile()

```js
第一个参数:文件路径;
第二个参数:文件内容;
第三个参数:回调函数;
fs.writeFile('url','写入内容',(err)=>{
    if(err){
       //失败
      }else{
        //成功
    }
})
```



## path模块-路径

```js
const path = require('path');
let filePath = path.join(__dirname,'url');
拼接路径

导入本地包
const path = require('path'); //

const dbpath = path.join(__dirname, 'utils', 'db.js'); //通过path方法 导入其他包
const db = require(dbpath);//导入包

```

## http

```js
const http = require("http");
let serverobj =http.createServer((request,reponse)=>	{
    
	})
    	request:请求报文,包含浏览器发来的数据
        reponse:响应报文对象,包含了和准备了要发送到浏览器的数据
serverobj.listen(8080,(err)=>{
    
})
locallhost:3747;浏览器请求

request对象,请求报文,
request.url:文件路径
request.method:get,post
request.headers:
request.headers.host:请求记录;
```

```js
什么是服务器软件?
	用来和浏览器软件做通信的软件,接受 分析 业务处理,,,
ip 和端口的作用?
	ip:互联网中唯一标识;
	port:在电脑中 唯一标识
使用http模块,
	1.导包;const http = require("http");
	2.创建;服务器对象
	3.启动;服务器软件监听;serverlisten(3747,(err)=>{});
		启动服务器时执行
```

## 创建本地服务器

```js
var fs = require("fs");
var path = require("path");
var http = require("http");

var serverobj = createServer((request,response)=>{
    var filepath = path.join(__dirname,request.url);
    fs.readFile(filepath,{'utf-8'},(err,data)=>{
        
    })
});
serverobj.listen(3747,(err)=>{
    
})

1.加载核心模块
	var http = require("http");
2.创建
	var server = http.cearteServer((request,reponse)=>{
        
    });
3.服务要干嘛
	server.on('request',function(request,response){
    console.log('收到客户请求'+request.url);
    response.write('holllll')
    response.write('nodejs')
    response.end();
    
})
4.绑定端口号,启动服务
	server.listen(3000,function(){
        
    })


resquest.setHearder('Content-Type','text/html;charset-utf-8')
```

## request-请求报文

```js
request.url 请求的路径
request.method 请求的方式 get/post
request.query.key   获取get发送的url?后的key=value
request.post
request.setHeader('content-type', 'text/html'); 设置
reuqest.getHeader('content-type');// text/html; 获取
reuqest.removeHeader('content-type');//移除

request.headers  打印全部请求头信息--对象形式
request.rawHeaders  全部头信息--数组形式
request.httpVersion  请求的协议方式
```

## response-响应报文

```
response.header
response.setHeader(属性名,属性值);
response.wriete();
response.end()
```

## get/post

```js
 method = 'GET/POST'
 
 GET:把数据放到url；
 POGT：把数据放到 请求报文体 中； 
 
 应用场景：
 	GET：为了获取服务器数据；（获取）
 	POST:为了修改改正服务器数据；（提交）
```

## Express

```js
www.express.com.cn

//1.下载
//2.导包
const express = require('express');
const body-parser = require('body-parser');//用户post
//2.1设置 web 文件夹 为 静态资源文件夹，浏览器可以直接访问
app.use(express.static('web'));
//2.2 注册 body-parser 中间件：自动 帮我们把 浏览器 发送来的 post 数据 封装到 request.body 中
app.use(bodyParser.urlencoded({ extended: false })) // parse application/x-www-form-urlencoded
app.use(bodyParser.json()) // parse application/json

//3. 创建服务器
	const app = express();
	

// 4.注册路由
  // 4.1向浏览器发送 响应数据
    app.get('/htmll',(req,res)=>{
            //1.字符串
            res.send('sdfsdfsdsdfdfdfsdf');//写在报文体
            //2.JSON
            // let obj = {name:'kk',age:'dddd'};
            // res.send(obj); //JSON.parse(obj)里面执行
    });
	//4.2获取 浏览器发送来的 get 参数，并打印
	app.get('/url',(req,res)=>{
        console.log(req.query)
    })
	//4.3post
    app.post('/reg',function (req,res) {
      console.log(req.body);
      console.log(req.body.txtName);
      console.log(req.body.txtPwd);
    })

// 5.



// 6.启动,设置端口
    app.listen(3747,(err)=>{
        if (err==null) {
            console.log('success');
        }else{
            console.log('启动 失败');
        }
    })

```

## multer

```js
https://github.com/expressjs/multer/blob/master/doc/README-zh-cn.md

//1.导包
//1.1 导入 express 包
const express = require('express')
//1.2 创建 express服务器程序对象
const app = express()
//1.3 创建 multer 对象，并设置 上传文件夹
var multer = require('multer')

var upload = multer({ dest: 'uploads/' })-----------创建文件夹

//2.1设置 web 文件夹 为 静态资源文件夹，浏览器可以直接访问
app.use(express.static('web'));

//3.注册路由 (url -> 处理函数 的关系)

// 3.3 获取 浏览器 发送来的 post 参数，并打印
app.post('/upload', upload.single('file01'), function (req, res) {-----注册路由
  // req.file 是 `file01` 文件的信息
  console.log(req.file);
  // req.body 将具有文本域数据，如果存在的话
  console.log(req.body);
  res.send('上传成功啦~~~' + req.file.filename);
})


```

```js
req.files 是 `photos` 文件数组的信息
{ fieldname: 'icon',
  originalname: '6385682971224b4c33e8e3507fd7a279.png',
  encoding: '7bit',
  mimetype: 'image/png',
  destination: 'uploads',
  filename: '8c9c56da992fc02ab691a7dca0d0c63e',
  path: 'uploads\\8c9c56da992fc02ab691a7dca0d0c63e',
  size: 25978 }
```

```js
req.body 将具有文本域数据，如果存在的话
[Object: null prototype] { name: 'walle', sikll: 'kuku' }
```

# express

## 中间件

- 特点:
    1. 使用app.use 注册中间件 函数—-本质是一个函数;
    2. 中间件函数有三个固定的参数(request,response,next());
    3. 中间件中 必须调用 next()函数,!!一般放在所有业务执行之后;
    4. 【面向切面编程】中间件,不论哪个路由被请求都会 先执行 中间件;

```js
中间件
	
app.use(function(request,response,next){
	
})

app.use(express.static('web/'));//暴露文件

app.use(bodyParser.urlencoded({extende:false}));
app.use(bodyParser.json());
```

Router()

```js
const express = require('express')

let myRouter = express.Router()

myRouter.use(function(req,res,next){
	next()
})
myRouter.get('/htmss',function(req,res){

})
module.exports = myRouter

--------------------------
导入:
const myrouter = require('./01myrouter.js')

app.use(myrouter) //自定义路由模块 注册
```

## hash

```js
hash.js   npm搜索
```

# cookie

```js
const cookieParser = require('cookie-parser')

注册cookie中间件
app.use(cookieParser())

res.cookie()

backurl:'/index' 返回链接
```

# cookie-session

```
session模块包含cookie-parser所有方法

app.use(cookiesession({
	name:'sessionId',
	keys:['234','kjlk']
}))
```

## 图片验证

```
svg-captcha
```

## connect-multipary

```js
bodyparser 不支持formdata
```



# 跨域

```js
浏览器会针对 异步对象 的 异步请求 做 跨域请求.

--1.请求添加如下:响应报文加如下
response.setHeader('Access-Control-Allow-Origin','*')
添加到响应报文,允许跨域访问

--2.下载包解决,原理如1;
npm i cors
const cors = require('cors')
注册cors跨域中间件
app.use(cors());


--3.解决:利用创建script的src请求;避开对http对异步跨域检测
$.ajax({
    url:'',
    method:'get',
    dataType:'jsonp',//ajax不再使用异步请求,而是使用script标签去请求
    cache:false, //不使用缓存,原理:是url产生随机数
    success:function(backdata){
        eval(backData);
    }
})
以上操作原理如下:
let strhtml = '<script src="跨域地址"></script>'
$('body').append(strhtml)

--4.通过src写入参数传入服务器,
let strhtml = '<script src="跨域地址?fn=fnname"></script>'
$('body').append(strhtml)
服务端:
let jsmethodname = req.query.fn
res.send(jsmethodname +'(参数)')
```

# JSONP

```

```

# promise

三个状态

```js
pending:进行中
fulfilled:成功
rejected:失败

```



```js
const fs = require('fs');

function getPromise(fileName) {
    return new Promise((resolve, reject) => {
      //读文件
      fs.readFile(`./etc/${fileName}.txt`, (err, data) => {
        if (err == null) {
          //读文件没有出错(异步成功)
          resolve(data);
        } else {
          //失败
          reject(err);
        }
      });
    });
}

//需求: 要先读a, 读完a后读b, 读完b后读c.
getPromise('a').then((data)=>{
    console.log(data.toString());

    //继续读b
    return getPromise('b');

}).then((data)=>{
    console.log(data.toString());

    //继续读c
    return getPromise('c');
}).then((data)=>{
    console.log(data.toString());
}).catch((err)=>{ //catch方法用来捕获错误信息的
      
});


promise 是一个构造函数
//必须传入一个回调函数,两个参数resolve,reject
//把需要异步的代码放到这个构造函数里
//没有错执行resolve
//错执行reject
//一旦创建即执行
let pm = new Promise((resolve,reject)=>{
    fs.readFile('url',(error,data)=>{
        if(error){
        	reject(error)
        }else{
            resolve(data)
        }
    })
})  

// 
pm.then((data)=>{
						//里面调用数据传入resolve(data)
}).then((data)=>{
    
})
```

catch

```js
用于捕获错误信息
```



## all方法

```js
/读a/b/c文件的promise
let pa = getPromise('a');
let pb = getPromise('b');
let pc = getPromise('c');

// 把这三个promise对象,搞成一个promise对象.
let pAll = Promise.all([pa,pb,pc]);
// 三个promise都异步成功后,才去执行pAll.then的第一个参数函数.
// 只要有一个失败了,就去执行catch里面的函数.
pAll.then((data)=>{
    console.log(data.toString());
}).catch((err)=>{
    console.log(err);
});
```

## race方法

```js
与all类似
只需一个成功就执行


// 三个promise只需要有一个异步请求成功了,就会去执行p.then的第一个参数函数.
// 都失败了,就去执行catch里面的函数.
const p = Promise.race([pa, pb, pc]);
p.then((data)=>{
    console.log(data.toString());
}).catch((err)=>{
    console.log(err);
});

```



# 数据库

```js
-- 1.查询
select * from heroinfo


-- 2.新增
insert into heroinfo(name,skill,icon) values('孙悟空','金箍棒','3.jpg' )


--3.删除
delete from heroinfo where id=3
delete from heroinfo where id>1 and id<=4


--4.修改
update heroinfo set skill = '七十二变' where id=5
update heroinfo set skill = '77变' ,icon= '7.jpg' where id = 5
```

## mysql

```js
var mysql = require('mysql')
var connection = mysql.createConnection({//创建连接
	host:'127.0.0.1',
    port:3306,//默认3306,可不写
	user:'root',
	password:'root',
	database://数据库名
})
    
connection.connect()//连接


connection.query('数据库操作语句',function(err,res,fields){
    
})

connection.end()//关闭连接



```

```js
返回
select的返回:
[ RowDataPacket { Id: 3, name: 'pppp', skill: 'sss', icon: 'sss' },
  RowDataPacket { Id: 4, name: 'pppp', skill: 'kk', icon: 'kk' },
  RowDataPacket { Id: 5, name: 'pppp', skill: 'kuku', icon: 'kk' },
  RowDataPacket { Id: 6, name: 'pppp', skill: 'kk', icon: 'kk' } ]
  
insert:的返回
	OkPacket{
      fieldCount:0
      affectedRows: 0,//受影响行数,新增,修改,删除
      insertId: 0,	//新增操作会 返回新增行id
      serverStatus: 2,//服务器状态
      warningCount: 0,
      message: '',
      protocol41: true,
      changedRows: 0
    }
```

# 获取异步值方法

```js
/*
 * @Description: In User Settings Edit
 * @Author: your name
 * @Date: 2019-08-28 19:35:16
 * @LastEditTime: 2019-08-28 19:35:25
 * @LastEditors: Please set LastEditors
 */
//1.调函数
function getSomething(cb) {
    var r = 0;
    setTimeout(function () {
        r = 2;
        cb(r);
    }, 10);
}

function compute(x) {
    alert(x * 2);
}
getSomething(compute);


//2.promise
//专门解决由于回调函数引起的问题
function getSomething() {
    var r = 0;
    return new Promise(function (resolve) {
        setTimeout(function () {
            r = 2;
            resolve(r);
        }, 10);
    });
}

function compute(x) {
    alert(x * 2);
}
getSomething().then(compute);

//3.generator
//有中断函数执行的能力
function getSomething() {
    var r = 0;
    setTimeout(function () {
        r = 2;
        it.next(r);
    }, 10);
}

function* compute(it) {
    var x = yield getSomething();
    alert(x * 2);
}
var it = compute();
it.next();

//4.promise + generator
//promise加generator，才是异步的完美方式
function getSomething() {
    var r = 0;
    return new Promise(function (resolve) {
        setTimeout(function () {
            r = 2;
            resolve(r);
        }, 10);
    });
}

function* compute() {
    var x = yield getSomething();
    alert(x * 2);
}
var it = compute();
it.next().value.then(function (value) {
    it.next(value);
});


//5.async
//终极方案:async。
function getSomething() {
    var r = 0;
    return new Promise(function (resolve) {
        setTimeout(function () {
            r = 2;
            resolve(r);
        }, 10);
    });
}

async function compute() {
    var x = await getSomething();
    alert(x * 2);
}
compute();

```



# 案例

### 1.http-简单文件服务器

```js
const http = require('http');
const mime = require('mime');
const path = require('path')
const fs = require('fs');

const serverobj = http.createServer((request, response) => {
    let urlstr = request.url; //获取请求/后的链接
    
    //根据链接 获取mime值 ,
    let mimeval = mime.getType(urlstr);
    
    //设置response headers中的 Content-Type
    response.setHeader('Content-Type', mimeval);
    let filepath = path.join(__dirname, urlstr); //获取地址
    fs.readFile(filepath, (err, data) => {
        if (err == null) {
           console.log(data);
            response.end(data);
        }else{
            console.log('请求失败');
        }
    })
})

serverobj.listen(3747,(err)=>{
    if(err==null){
        console.log('success')
    }
})
```

### 2.重定向

```js
const http = require('http');
const url = require('url');
const mime = require('mime');

const server = http.createServer((request,response)=>{
    // 如果 浏览器请求的 是页面 9，就发送 302 给 浏览器，告诉他 跳转到 2.html
    if (request.url.indexOf('9.html')>-1) {
        
    // 向 响应报文 头 中 添加 location ，告诉浏览器 要跳转的目标
        response.setHeader('location','2.html');
        
    // 向响应报文头中 设置 状态码为 302
        response.writeHead(302,'move');
        
    }else if(request.url.indexOf('10.html')>-1){
        let mimeval = mime.getType(request.url);//根据获取的url尾部,获取Content-type
        response.setHeader('Content-type',mimeval+";charset=utf-8")
        response.write('<script>alert("要跳转了"); window.location = "2.html";</script>');
       
    }
    response.end();
})

server.listen(3747,(err)=>{
    if (err==null) {
        console.log('启动成功');
    }else {
        console.log('启动失败');
    }
})
```

### 3.获取get数据

```js
<html>

<head>
  <title></title>
  <meta charset='UTF-8' />
</head>

<body>
  <!-- 表单 Get 方式提交数据  -->
  <form action="http://192.168.14.134:3747/2.html" method="GET">
    <input type="text" name="txtName">
    <input type="password" name="txtPwd">
    <br>
    <input type="submit" value="提交">
  </form>
</body>

</html>

const http = require('http');
const url = require('url');

const serverobj = http.createServer((request,response)=>{
    //a. 获取 浏览器 用 get 方式 传来的 数据
    let urlstr = request.url;
    console.log(urlstr)
     //b. 使用 url.parse 方法，将 请求的 路径中的 get 参数 转成 对象，存入 url对象.query属性中
    let urlobj = url.parse(urlstr,true);
    console.log(urlobj);
})

serverobj.listen(3747,(err)=>{
    if (err==null) {
        console.log('success');
        
    }else{
        console.log(' failures');
    }
})
```

### 4.path模块生成路径

```js
const path = require('path');
const fs = require('fs');

//文件夹路径+文件路径 拼接
let filePath = path.join(__dirname,'文件路径');

fs.readFile(filePath,'utf-8',(err,data)=>{
    if(err == null){
        console.log(data);
    }else{
        cosole.log(err.messge)
    }
})
```

### 5.数据库操作封装

```js
const mysql = require('mysql')
const connInfo={
    host:'127.0.0.1',
    database:'新数据库2',
    user:'root',
    password:'root'
}

module.exports = {
    getHero:function(fn){
        let connection = mysql.createConnection(connInfo)
        connection.connect()
        connection.query('select * from hero',fn)
        connection.end()
    },
    addHero:function({name,skill,icon},fn){
        let connection = mysql.createConnection(connInfo)
        connection.connect()
        connection.query(`insert into hero(name,skill,icon) value('${name}','${skill}','${icon}')`,fn)
        connection.end()
    },
    deleteHero:function(id,fn){
        let connection = mysql.createConnection(connInfo)
        connection.connect()
        connection.query(`delete from hero where id=${id}`,fn)
        connection.end()
    },
    updateHero:function({name,skill,icon,id},fn){
        let connection = mysql.createConnection(connInfo)
        connection.connect()
        connection.query(`update hero set name = '${name}' ,skill = '${skill}',icon = '${icon}' where id = ${id}`,fn)
        connection.end()
    }
}
```



# ES6

## let 与 const

```js
let
	无法变量提升
	无法重复声明
	可以重新赋值
	有块级作用域
	
const
	1.无法变量提升
 \* 2.无法重复声明
 \* 3.无法重新赋值
 \* 4.有块级作用域
 \* 5.必须声明时就要赋值
```

## 解构

```js
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。
这种写法属于“模式匹配”
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

1.解构不成功返回 undefined
2.不完全解构
	let [x, y] = [1, 2, 3];
		x // 1
		y // 2
	let [a, [b], d] = [1, [2, 3], 4];
		a // 1
		b // 2
		d // 4
3.如果等号的右边不是数组/对象(不可遍历的结构 /Iterator 接口),会报错;


```

### 对象解构赋值

```js
而对象的属性没有次序，变量必须与属性同名，
let { bar, foo } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"

// 例一
let { log, sin, cos } = Math;
上面代码的例一将Math对象的对数、正弦、余弦三个方法，赋值到对应的变量上
// 例二
const { log } = console;
log('hello') // hello
例二将console.log赋值到log变量

let obj = {};
let arr = [];
({ foo: obj.prop, bar: arr[0] } = { foo: 123, bar: true });
obj // {prop:123}
arr // [true]

------------默认赋值---做边有值则不覆盖,无则赋值
var {x = 3} = {};
x // 3

var {x, y = 5} = {x: 1};
x // 1
y // 5

var {x: y = 3} = {};
y // 3

var {x: y = 3} = {x: 5};
y // 5

var {x = 3} = {x: undefined};
x // 3

var {x = 3} = {x: null};
x // null

注意点:
// 正确的写法  //声明语句不能用()
let x;
({x} = {x: 1});

// 错误的写法
let x;
{x} = {x: 1};
// SyntaxError: syntax error
```

### 字符串解构

```js
字符串被转换成了一个类似数组的对象。
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"

类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。
let {length : len} = 'hello';
len // 5
```

### 函数参数解构赋值

```js
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]

function move({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}
move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, undefined]
move({}); // [undefined, undefined]
move(); // [0, 0]
```

### 解构用途

```js
http://es6.ruanyifeng.com/?search=%E3%80%8AGenerator+%E5%87%BD%E6%95%B0%E3%80%8B&x=6&y=3#docs/destructuring

1.变量交换值:
	[x, y] = [y, x];
2.函数返回多个值:
	function example() {
  		return {
    		foo: 1,
    		bar: 2
  		};
	}
	let { foo, bar } = example();
3.函数参数的定义:
	function f({x, y, z}) { ... }
	f({z: 3, y: 2, x: 1});
4.提取JSON数据:
	let jsonData = {
    	id: 42,
    	status: "OK",
    	data: [867, 5309]
  	};
	let { id, status, data: number } = jsonData;
```



## 箭头函数

```js
var f = v => v;

// 等同于
var f = function (v) {
  return v;
};


var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};

var sum = (num1, num2) => { return num1 + num2; }
```

### 展开运算符

```js
let chinaPerson = {
  skin: 'yellow',
  hair: 'black',
  sayHi: '吃了没'
}

let zhubo = {
  skill: '唱，跳，rap',
  habbit: '打篮球'
}
let newObj ={
  ...chinaPerson, // 将 chinaPerson 的成员 都添加到此
  ...zhubo // 将 zhubo 的成员 都添加到此
};
```

### 模板字符串

```js
可以挖坑 ${表达式}
```







# ES6 简要

## 01.  ES6简介

### 1.1 什么是ES6

​	ES6其实就是在ES5的基础之上新增了一些语法和提供多了一些api, 使用ES6新增的语法和api, 我们可以快速实现一些功能，而不必使用ES5中写很多代码的方式来实现。比如我要判断1个字符串是否以指定的字符串开始，在ES6中，直接为字符串对象新增了1个方法`startsWtih`就可以轻松的实现这个功能。

```javascript
var str = "heima good"; 
var res = str.startsWith("hei"); //判断字符串str是否以hei开头
//res就是1个bool值，代表str是否以"hei"开头
```

​	ES6就是这么高效，为JavaScripter提供了快速高效的编码方式.

### 1.2 ES6的兼容性

​	ES6标准于2015年6月正式发布, 经过四年的发展，PC桌面端的主流浏览器最新版本都对ES6实现了最大化的兼容，移动端浏览器基本上实现了对ES6的兼容，NodeJS对ES6绝大部分语法进行了实现。

​	ES6兼容情况一览表：  [传送门](<http://kangax.github.io/compat-table/es6/>)

​	对于少部分语法不兼容的情况(主要是PC桌面端浏览器), 我们可以使用编译器(如Babel)将我们写的ES6代码转换为ES5的代码，以便让低版本的浏览器可以兼容。具体如何使用Babel，我们将在后续的章节为大家介绍。

## 02. let与const

### 2.1 他们是什么？

​	`let`与`const`是ES6新增的两个关键字，他们的作用和`var`的作用一样，是用来声明变量的

```javascript
var a = 1;
let b = 2;
const c = "i love heima";
```

### 2.2 let与const的区别

​	使用`let`声明的变量，后续可以重新为其赋值；使用`const`声明的变量，要求在声明的同时就进行初始化，但是后续无法再为这个变量进行重新赋值。

```javascript
let a = 10;
a = 20;
let b;
b = "jack";
const c = 10;
c = 20; //错误，c是const声明的，变量不能再重新赋值
const d; //错误，使用const声明的变量，必须在声明的同时就初始化.
```

**特别注意**，`const`变量指向1个对象的时候，这个变量的值不能变，但是这个变量指向的对象可以修改.

```javascript
const person = {
    name: "jack",
    age: 19,
    gender: "male"
};
person.name = "rose"; //可以，并没有修改person变量的值，修改的是person指向的对象的属性的值.
person = {
    name: "rose",
    age: 18,
    gender: "female"
}; //错误，person变量是被const修饰的，不能再为其赋值.

```

### 2.3 与var的区别

使用`let`和`const`声明的变量不存在变量提升，有自己的作用域 - 其所在的大括弧中。

```javascript
let a = 1;
{
    let b = 2;
    console.log(c);//报错，提示变量c未定义
    const c = 3;
    //变量b、c只能在声明b、c变量中的大括弧中访问。 
    //并且也不存在变量提升
    console.log(a); //可以访问
    console.log(b);//可以访问
    console.log(c); //可以访问
}
console.log(a); //可以访问
console.log(b);//不可以访问
console.log(c); //不可以访问`
```

### 2.4 使用建议

- 能使用const就不要使用let
- 能使用let就不要使用var

​       其实大多数情况下，我们声明的变量后续都不会再重新赋值，所以这种情况，建议使用`const`；如果变量的值后续需要更改，可以使用`let`； `var`关键字请彻底废弃。

## 03. 箭头函数

​	箭头函数是我们之前学习的函数的一种简写方式。

### 3.1 箭头函数的书写规则

​	将普通函数的`function`关键字删掉， 在小括弧与大括弧中间加上1个箭头`=>`，用法与普通函数一样。

```javascript
const add = function (a, b){
    const result = a + b;
    return result;
}

const sayHi = (a, b) => {
    const result = a + b;
    return result;
}
```

![](../../../%E5%89%8D%E7%AB%AF41%E6%9C%9F/07.node-JS/node.js%E9%A2%84%E4%B9%A0%E8%B5%84%E6%96%99/day01/02-%E5%85%B6%E4%BB%96%E8%B5%84%E6%96%99/es6/media/01-arrow.gif)  

箭头函数的作用：  让我们声明函数的时候，使用更少的代码，看起来更简洁。



### 3.2 更简洁的写法

- a. 如果参数只有1个，那么包围参数的小括弧可以省略

```javascript
const isEven = num => {
    if(num % 2 == 0){
        return true;
    }else{
        return false
    }
}
```

   

- b. 如果函数体只有一句代码，那么包围函数体的大括弧可以省略,并且这句代码的结果会自动作为返回值返回

```javascript
const isEven = num => num % 2 == 0;
const res = isEven(10);
```



### 3.3 箭头函数的使用场景

- 箭头函数本身是1个匿名函数，所以如果你要二次使用，必须得有个变量保存起来.
- 箭头函数在回调函数中被经常使用到，代码会显得更简洁。

```javascript
setTimeout(()=>console.log(1),1000);

```

### 3.4 箭头函数使用注意

- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。
- 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

## 04. 字符串

### 4.1 模板字符串

​	声明字符串我们可以使用单引号和双引号来表示，在ES6中新增了一种声明方式，使用1对撇号来表示。

```javascript
let msg = `大家好，
我是小明
\n哈哈，你好啊
这是1个模板字符串哦
`;

```

- 模板字符串，支持换行，等操作，撇号中的内容会被原样识别。
- 模板字符串还支持变量替换

```javascript
let name1 = "杜子腾";
let name2 = "秦寿生";
let msg = `孔子东游，见两小儿辩斗，问其故。
${name1}曰：“我以日始出时去人近，而日中时远也。”
${name2}以日初出远，而日中时近也。
${name1}曰：“日初出大如车盖，及日中则如盘盂，此不为远者小而近者大乎？”
${name2}曰：“日初出沧沧凉凉，及其日中如探汤，此不为近者热而远者凉乎？”
孔子不能决也。
${name1+"和"+name2}笑曰：“孰为汝多知乎？”
`;

```



### 4.2 字符串新增方法

- `includes()`方法              是否包含子串
- `startsWith()`方法          以指定的串开始
- `endsWith()`方法             以指定的串结尾
- `repeat()`方法                将字符串重复
- `padStart()`方法            头部补全
- `padEnd()`方法                尾部补全

## 05. 数值Number

> ES6为Number新增了一些方法，方便我们更加方便操作Number数据.

- `Number.isFinite()` 用来检查一个数值是否为有限的（finite），即不是`Infinity`
- `Number.isNaN()`  用来检查一个值是否为`NaN`
- es6将全局方法`parseInt()`和`parseFloat()`，移植到`Number`对象上面，行为完全保持不变
- `Number.isInteger()` 用来判断一个数值是否为整数。



## 06. Math类

ES6对Math对象新增了很多数学方法.  [传送门](http://es6.ruanyifeng.com/#docs/number#Math-%E5%AF%B9%E8%B1%A1%E7%9A%84%E6%89%A9%E5%B1%95)

并且新增了1个算术运算符 - 指数运算符 （ ** ）

```javascript
const a = 2;
const b = 3;
const c = 2 ** 3;  //2的3次方.

```



## 07. 函数

### 7.1 参数默认值

​	在声明函数的时候，允许对函数的参数赋一个默认值， 当调用函数时，如果不为指定默认值的参数传值，那么在函数执行的时候，参数的值就是默认值

```javascript
const add = (a, b = 20) => {
    const res = a + b;
    console.log(res);
}
add(10);//在调用函数的时候，只为第1个参数传值，而没有为第2个参数传值。那么第2个参数的值就是其默认值20
add(10, 5);//如果两个参数都传了值，那么参数的值就是传入的值。

```

​	需要注意的是， 如果函数的参数带了默认值，那么带了默认值的参数必须写在参数列表的最后

```javascript
const add = (a = 10, b) => { //报错，带默认值的参数必须放在参数列表的最后.
    
}

```

​	这样，别人在调用我们写的函数的时候，一眼就能看出哪些参数是必传参数，哪些参数是可选参数。

### 7.2 参数是1个对象的时候

​	当1个函数的参数是1个对象的时候，按照我们之前的写法，调用者很难知道这个对象的属性有哪些。比如，jQuery的ajax方法，这个方法我们都知道要传入1个对象，但是这个对象要准备哪些属性呢？ 除了看文档，真的没有别的方法。在ES6中，为我们提供了一种写法，让调用者看到我们函数的形参就知道要传入哪些属性，代码演示如下

```javascript
//参数直接使用1个大括弧围起来，把属性写在其中. 这就表示参数是1个对象，这个对象中有这么些属性
const ajax = ({url, method, data}) =>{ 
    console.log(url, method, data)      
}

ajax({
    url: "aa",
    method: "get",
    data: {
        name: "jack",
        age: 18
    }
});


```

### 7.3 rest参数(可变参数)

​	当我们需要某1个函数可以接收任意多个参数的时候，我们之前的做法要么是使用arguments，要么是使用1个数组，在ES6中，借鉴了其它语言中非常流行的一种做法，那就是rest参数.

​	当形参前面加上`...` 三个点， 就表示这是1个rest参数，这是1个数组，它可以接收多余的实参到这个数组中。

```javascript
const add = (a, b, ...args) => { //args就是1个rest参数，它是1个数组，用来存储传入的额外参数.
    let sum = a + b;
    for(let index in args){
        sum += args[index];
    }
    console.log(sum);
}
add(1, 2, 3, 4, 5, 6, 7, 8);  //1和2分别传给了参数a和b, 后面的所有参数都传给了args数组.

```

​	**需要注意的是，rest参数只能放在参数列表的最后，并且1个函数最多只能有1个rest参数**



### 7.4 函数参数的尾逗号

​	在ES6中，允许在参数列表的最后也加上1个逗号，用来让我们的代码变的可读性更高。

```javascript
const add = (a, b, c,) => {
    return a + b + c;
}

add(10,20,30,);

```

## 08. 数组

### 8.1 扩展运算符

​	其实叫做`展开运算符`更容易理解一些，它可以将1个数组中的元素展开, 一般用在函数的传参中。

```javascript
const add = (a, b, c) => {
    return a + b + c;
}
const arr = [10, 20, 30];
add(...arr); //将数组arr展开成单独的10,20,30，传给add函数

```





### 8.2 常用扩展方法

- `includes()`， 判断数组中是否包含指定的元素

- `flat()`, 当数组中包含1个数组时，可以将里面的数组拉平，变成1个一维数组。参数代表拉平的层数。`Infinity`

    

    其它方法扩展。 [传送门](<http://es6.ruanyifeng.com/#docs/array>)



## 09. 对象

### 9.1 属性简洁表示法

​	声明对象的时候，如果属性名和属性值都是一样的变量，可以使用简写的形式，代码演示如下。

```javascript
ES5写法:
var name = "jack";
var age = 19;
var gender = "男";

var person = {
    name: name,
    age: age,
    gender: gender,
    sayHi: function(){
        console.log("你好，hi...");
    }
}

ES6简写形式
const name = "jack";
const age = 19;
const gender = "男";

const person = {
    name,
    age,
    gender, //如果属性名，和属性的值使用的是同1个变量，可以这样简写
    sayHi(){
        console.log("你好，hi...");
    }//对象方法也可以简写.
}


```

### 9.2 属性名表达式

在ES5中，要为对象新增1个属性，可以使用这样的代码

```javascript
const p1 = {
    name: "jack",
    age: 18
}
p1.gender = "男";
p1["weight"] = 140;

```

在ES6中，为对象新增属性，属性可以使用表达式，像下面这样

```javascript
const p1 = {
    name: "jack",
    age: 18
}
p1["gen"+"der"] = "男";
p1["wei"+"ght"] = 140;
p1["say"+"hi"] = () => { console.log("hi....") }

```

最终对象是这样的，属性名可以使用拼接。

![](../../../%E5%89%8D%E7%AB%AF41%E6%9C%9F/07.node-JS/node.js%E9%A2%84%E4%B9%A0%E8%B5%84%E6%96%99/day01/02-%E5%85%B6%E4%BB%96%E8%B5%84%E6%96%99/es6/media/01.png) 



### 9.3 属性的可枚举

#### 引入

​	`for in`可以遍历对象的属性包括方法

```javascript
const p1 = {
    name: "jack",
    age: 19,
    sayHi(){console.log("hi...")}
}
for(let key in p1){
    console.log(p1[key]);
}

```

结果如下

![](../../../%E5%89%8D%E7%AB%AF41%E6%9C%9F/07.node-JS/node.js%E9%A2%84%E4%B9%A0%E8%B5%84%E6%96%99/day01/02-%E5%85%B6%E4%BB%96%E8%B5%84%E6%96%99/es6/media/02.png) 

但是，你有没有想过一个问题，p1对象中只有这些成员吗？还有从父类继承过来的`toString`方法没有被遍历出来，是继承的属性不能被遍历吗？ 用代码证实一下

```javascript
function Animal (name) {
  this.name = name || 'Animal';
  this.sleep = function(){
    console.log(this.name + '正在睡觉！');
  }
}
Animal.prototype.eat = function(food) {
  console.log(this.name + '正在吃：' + food);
};
Animal.prototype.type = "哺乳动物";

function Cat(){

}
Cat.prototype = new Animal();
Cat.prototype.name = "cat"

var c1 = new Cat();
for(let key in c1){
    console.log(c1[key]);
}//证实父类的属性可以被遍历.

```

证实父类的属性可以被遍历

![](../../../%E5%89%8D%E7%AB%AF41%E6%9C%9F/07.node-JS/node.js%E9%A2%84%E4%B9%A0%E8%B5%84%E6%96%99/day01/02-%E5%85%B6%E4%BB%96%E8%B5%84%E6%96%99/es6/media/03.png) 

那究竟什么样的属性才可以被遍历呢？

#### 属性描述对象

> 对象的每一个属性，其实都有1个描述对象，这个描述对象来保存这个属性的描述信息(是否能被遍历，是否可读，默认值...)。 使用 *Object.getOwnPropertyDescriptor()*方法可以获取对象的属性的描述方法. 

```javascript
const p1 = {
    name: "jack",
    age: 19,
    sayHi(){ console.log("hi..."); }
}
const desc = Object.getOwnPropertyDescriptor(p1, "name"); //获取p1对象的name属性的描述对象

```

属性描述对象描述这个属性的信息如下。

![](../../../%E5%89%8D%E7%AB%AF41%E6%9C%9F/07.node-JS/node.js%E9%A2%84%E4%B9%A0%E8%B5%84%E6%96%99/day01/02-%E5%85%B6%E4%BB%96%E8%B5%84%E6%96%99/es6/media/04.png) 

​	只有当属性的描述对象的`enumerable`值为`true`的时候，这个属性才会被允许遍历。

​	那属性的描述对象的`enumerable`值什么时候才有可能为`false`呢?

​	当我们使用`Object.getOwnPropertyDescriptor()` 为对象定义属性的时候，可以指定描述对象的`enumerable`的值

```javascript
const p1 = {
    name: "jack",
    age: 19,
    sayHi(){ console.log("hi..."); }
}
//参数1  要设定属性的对象
//参数2  要设定的属性的名
//参数3  描述对象
Object.defineProperty(p1, "gender", {
    enumerable: false,
    value: "男"
});

```

​	此时，新增的属性就不能被`for in`遍历了.



#### 属性遍历

##### `for in` 遍历对象

​	循环遍历对象自身的和继承的可枚举属性

##### `Object.keys(obj)` 

​	返回一个数组，包括对象自身的（不含继承的）所有可枚举属性的键名。

##### `Object.getOwnPropertyNames(obj)` 

​	返回一个数组，包含对象自身的所有属性（包括不可枚举属性）的键名。



## 10. set

> Set是1个类似于数组的数据结构，与数组不同的是，Set中的数据不允许重复，当向Set中添加1个已经存在的数据时，不会成功。

```javascript
const set = new Set();
set.add(1);
set.add(2);
set.add(3);
set.add(2);//不会添加成功，但是不会报错

```

常用方法

- `size`属性返回set中数据的个数
- `add()`
- `delete()`
- `has()`
- `clear()`

遍历操作

- `keys()`
- `values()`
- `entries()`
- `forEach()`

### WeakSet

> WeakSet和Set一样，都是存储不可重复的数据，与Set的区别有两点
>
> 1. WeakSet中只能存储对象.
> 2. WeakSet中存储的对象都是弱引用，当外部没有变量指向对象的时候，即使被WeakSet所引用，对象也会被回收。



## 11. Map

> 键值对存储数据，和js中的对象类似，不同的是，js对象中的键只能是字符串，而map中的键可以是任意类型.

```javascript
const map = new Map();
const p1 = { name: "jack" }
const p2 = { name: "rose" }
map.set(p1, p2); //以p1为键，将p2存储到Map对象中.

```

### 常用方法

- `size`属性 获取Map中键值对的个数
- `set(key, value)` 添加键值对， `key`和`value`可以是任意的类型. 该方法返回当前Map对象.
- `get()`根据键获取键对应的值、
- `has(key)`
- `delete(key)` 
- `clear()` 
- `keys()`
- `values()`
- `entries()`
- `foreach()`



### WeakMap

> 与Map类似，WeakMap也是用来存储键值对的集合，与Map的区别有两点
>
> 1. WeakMap只接受对象作为键名(null除外)
> 2. 其次，`WeakMap`的键名所指向的对象，不计入垃圾回收机制。





## 12. 迭代器

在ES6中新增了一种遍历方式叫做`for...of`，可以使用它来遍历数组、Map、Set等.

```javascript
const arr = [10,20,30,40,50,60,70,80,90,100];
for(let item of arr){
    console.log(item);
}

const set = new Set(arr);
for(let item of set){
    console.log(item);
}

const map = new Map();
map.set("name", "jack");
map.set("age", 19);
map.set("gender", "男");

for(let item of map){
    console.log(item);
}

```

能否使用`for...of`循环遍历我们自己写的对象吗？

```javascript
const p1 = {
    name: "jack",
    age: 19,
    gender: "男"
}

for(let item of p1){
    console.log(item);
} //报错 无法使用for of遍历p1对象.

```

![](../../../%E5%89%8D%E7%AB%AF41%E6%9C%9F/07.node-JS/node.js%E9%A2%84%E4%B9%A0%E8%B5%84%E6%96%99/day01/02-%E5%85%B6%E4%BB%96%E8%B5%84%E6%96%99/es6/media/06.png) 

### 12.1 for...of的原理

​	在使用`for..of`遍历1个对象的时候，先调用这个对象的`Symbol.iterator`方法，这个方法返回1个`迭代器`。每遍历一次，就会调用`迭代器`对象的`next`方法，这个方法会返回1个对象，这个对象包含两个属性，一个是`value`,指定本次遍历得到的结果，还有一个属性是`done`，bool值，代表遍历是否结束，每调用一次`next`方法， 就返回下1个被遍历的值，直到最后一个元素。

```javascript
const arr = [10,20,30,40,50,60,70,80,90,100];
const set = new Set(arr);
//1.调用set对象的遍历器方法，返回1个迭代器对象.  
const iterator = set[Symbol.iterator]();
//iterator就是这个迭代器对象.
while(true){
    let item = iterator.next();
    if(item.done){
		break;
    }
    console.log(item.value);
}

```





### 12.2 实现自己的迭代器

知道了`for...of`的原理后， 如果我们希望我们自己的对象也能被`for...of`遍历，那么就可以这么做

- 为对象添加1个`[Symbol.iterator]`方法。
- 这个方法返回1个对象
- 这个对象需要有1个next方法
- 这个next方法返回1个对象，对象包含`vulue`属性，表示本次遍历的值，包含1个`done`属性，表示本次遍历结束后是否还有数据。 然后保证下次调用next方法的时候 返回的是下1个数据.

```javascript
const hmSet = {
    data: [10,20,30,40,50,60,70,80,90,100],
    [Symbol.iterator](){
        const that = this;
        let index = 0;
        return {
            next: function(){
                return {
                    value: that.data[index++],
                    done: index == that.data.lenght + 1
                }
            }
        }
    }
}

for(let item of hmSet){
    console.log(item);
}

```



### 12.3 原生实现了迭代器的对象

- Array
- Map
- Set
- String
- TypedArray
- 函数的 arguments 对象
- NodeList 对象

也就是说，这些对象是可以直接用`for...of`来遍历的。





