# html-css

## html有哪些常用标签:

```html
header
nav

section
article
aside

footer
```

## 简述一下html语义化理解:

- ```js
    让页面的内容结构化,结构更清晰,便于阅读、维护和理解
    ```

## html5新特性,移除了哪些元素

- ```js
    
    ```

## 什么是盒子模型:画出盒子模型

- ```
    margin
      border
      padding
      content
    ```

## 行内元素有哪些,块级元素有哪些,空元素有哪些

- ```js
    行内元素:span, i, em,
      块级元素:div,h,ul,li,ol
    ```

## display有哪些值,说明他们的作用

- ```js
  块转行内：display:inline;
    行内转块：display:block;
    块、行内元素转换为行内块： display: inline-block;
    隐藏:display:none;
    flex布局:display:flex;
  ```

## css选择器有哪些

- ```
    
    ```

    

## 解释css sprites 精灵图 雪碧图

- ```js
    
    ```

    

## 清除浮动的方式:

- ```
    
    ```

    

## Flex布局有哪些常见属性:

```

```

## 水平居中有哪些方法:

```

```

## 移动端怎么做适配:

```
1.媒体查询。

2.js 动态设置 html 的 font-size（rem 为单位）。

3.淘宝提供的解决方案 flexible.js（rem 为单位）。

rem 淘宝适配方案+postcss-pxtorem
```

2-js 动态设置

```js
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0" />

(function(doc, win) {
    var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function() {
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;
        // 设置设计稿的宽度clientWidth为750
            if (clientWidth >= 750) {
                docEl.style.fontSize = '75px';
            } else {
                // 设置设计稿的宽度clientWidth为750
                docEl.style.fontSize = 75 * (clientWidth / 750) + 'px';
            };
        };
    if (!doc.addEventListener) return;
    win.addEventListener(resizeEvt, recalc, false);
    doc.addEventListener('DOMContentLoaded', recalc, false);
})(document, window);
```

3-淘宝提供的解决方案 flexible.js（rem 为单位）。

```js
// 首先是一个立即执行函数，执行时传入的参数是window和document
(function flexible (window, document) {
  var docEl = document.documentElement // 返回文档的root元素
  var dpr = window.devicePixelRatio || 1 
  // 获取设备的dpr，即当前设置下物理像素与虚拟像素的比值

  // 调整body标签的fontSize，fontSize = (12 * dpr) + 'px'
  // 设置默认字体大小，默认的字体大小继承自body
  function setBodyFontSize () {
    if (document.body) {
      document.body.style.fontSize = (12 * dpr) + 'px'
    } else {
      document.addEventListener('DOMContentLoaded', setBodyFontSize)
    }
  }
  setBodyFontSize();

  // set 1rem = viewWidth / 10
  // 设置root元素的fontSize = 其clientWidth / 10 + ‘px’
  function setRemUnit () {
    var rem = docEl.clientWidth / 10
    docEl.style.fontSize = rem + 'px'
  }

  setRemUnit()


    // 当我们页面尺寸大小发生变化的时候，要重新设置下rem 的大小
    window.addEventListener('resize', setRemUnit)
        // pageshow 是我们重新加载页面触发的事件
    window.addEventListener('pageshow', function(e) {
        // e.persisted 返回的是true 就是说如果这个页面是从缓存取过来的页面，也需要从新计算一下rem 的大小
        if (e.persisted) {
            setRemUnit()
        }
    })

  // 检测0.5px的支持，支持则root元素的class中有hairlines
  if (dpr >= 2) {
    var fakeBody = document.createElement('body')
    var testElement = document.createElement('div')
    testElement.style.border = '.5px solid transparent'
    fakeBody.appendChild(testElement)
    docEl.appendChild(fakeBody)
    if (testElement.offsetHeight === 1) {
      docEl.classList.add('hairlines')
    }
    docEl.removeChild(fakeBody)
  }
}(window, document))
```



## 简述px,em,rem

- ```
    PX
    px像素（Pixel）

    em
    相对父级文fontsize; 1em = 父fontsize;
    
    rem
    	相对html的fontsize大小; 1rem = html fontsize
    ```
    
    

# js

## 原型链

![1559057933326](../image/1559057933326-1574858855016.png)

## 原型继承方式

### 1原型链继承

- ```js
  function SuperType() {
    this.property = true;
  }
  SuperType.prototype.getSuperValue = function() {
    return this.property;
  }
  function SubType() {
    this.Subproperty = false;
  }
  SubType.prototype = new SuperType(); // 继承了SuperType
  SubType.prototype.getSubValue = function() {
    return this.Subproperty ;
  }
  var instance = new SubType();
  alert(instance.getSuperValue()) // true
  ```

  **优缺点:**

  ```js
  继承原理：通过让子类的原型等于父类的实例，来实现继承。
  优点：继承了超类型的构造函数的所有属性和方法。
  缺点：1、在创建子类实例时，无法向超类型的构造函数传参，继承单一。
  　　　2、所有新实例都会共享父类实例的属性。
  ```

  

### 2构造函数继承

- ```js
  function SuperType() {
    this.colors = ['red', 'blue', 'green'];
  }
  function SubType() {
    SuperType.call(this); //  继承了SuperType
  }
  var instance1 = new SubType();
  instance1.colors.push('black');
  console.log(instance1.colors); // ['red', 'blue', 'green', 'black']
  ```

  **优缺点:**

  ```js
  继承原理：改变子类的this,通过call指向父类;
  优点：可以在子类构造函数中，向超类型构造函数传递参数。
  缺点：只继承了父类构造函数的属性，没有继承父类原型的属性。所有的方法都在构造函数中定义，无法实现复用，影响性能。
  ```

  

### 3组合继承

- ```js
  function SuperType(name) {
    this.name = name;
    this.colors = ['red','blue','green'];
  }
  SuperType.prototype.sayNAme = function() {
    alert(this.name);
  }
  function SubType(name,age) {
    SuperType.call(this, name); // 继承属性
    this.age = age;
  }
  SubType.prototype = new SuperType(); // 继承方法
  SubType.prototype.constructor = SubType;
  SubType.prototype.sayAge = function() {
    alert(this.age);
  }
  
  var instance1 = new SubType('xxx', 15);
  instance1.colors.push('black');
  console.log(instance1.colors); // ['red','blue','green','black']
  instance1.sayNAme(); // xxx
  instance1.sayAge(); // 15
  ```

  **优缺点:**

  ```js
  使用原型链实现对原型属性和方法的继承，通过构造函数来实现对实例属性的继承。这样既通过在原型上定义方法实现了函数的复用，又能够保证每个实例都有它自己的属性。
  缺点：调用两次父类构造函数。
  ```

  

### 4寄生组合继承

- ```js
  function create(prototype) {
  function Super() {}
  Super.prototype = prototype
  return new Super()
  }
  
  function Programmer(age, name) {
  Person.call(this, age)
  this.name = name
  }
  
  Programmer.prototype = create(Person.prototype)
  Programmer.prototype.constructor = Programmer // 修复构造函数指向
  
  let jon = new Programmer(18, 'jon')
  jon.name // jon
  ```

  **优缺点:**

  ```js
  子类构造函数复制父类的自身属性和方法，子类原型只接受父类的原型属性和方法
  ```

  

进描述一下cookies,sessionStorage和localStorage

- ```
    
    ```

    

浏览器的同源策略

- ```
    
    ```

    

正则表达式,匹配以字母开头,后面可以是数字6-30?

- ```
    
    ```

    

统计字符串出现最多的字母aaacccdddddffff

- ```
    
    ```

    

AJAX的原理

- ```js
    
    ```

    

js原生对象有哪些

- ```
    
    ```

    

对象声明三种方式:

- ```
    
    ```

    

前端优化有哪些:

- ```js
    
    ```

# ES6

es6有哪些新特性:

```

```

数组有哪些常见的api:

```


```

# vue

vue的v-model的原理是?

双向绑定是分两个数据传递方向:

```

```

vue的生命周期:

```

```

vue组件传递如何传递:

父>子:

```

```

子>父:

```

```

兄弟互传:

```js

```

# xss 和 csrf

## xss

```js
https://www.cnblogs.com/tugenhua0707/p/10909284.html

http://www.ruanyifeng.com/blog/2016/09/csp.html
```



```js
Cross Site Scripting
跨站脚本攻击
恶意攻击者在web页面中会插入一些恶意的script代码。

```

1. **xss防御html编码**

   ```
   编码规则：将 & < > " ' / 转义为实体字符
   ```

   

2. **XSS 防御HTML Attribute编码**

   ```
   编码规则：除了字母、数字、字符以外，使用 &#x;16进制格式来转义ASCII值小于256所有的字符。
   
   
   ```

   

3. **XSS防御之javascript编码**

   ```js
   编码规则:JavaScript编码将字符编码成\x+16进制的形式，对款字节编码成Unicode
   function encodeForJavascript(str) {
         let encoded = '';
         for(let i = 0; i < str.length; i++) {
           let cc = hex = str[i];
           if (!/[A-Za-z0-9]/.test(str[i]) && str.charCodeAt(i) < 256) {
             hex = '\\x' + cc.charCodeAt().toString(16);
           }
           encoded += hex;
         }
         return encoded;
       };
   
    XSS 防御HTML Attribute编码中我们是可以防御XSS攻击，但是它只能防御的是HTML通用属性，并不是全部属性，在html中还存在很多支持协议解析的html属性，比如 onclick, onerror, href, src 等这些，
   ```

   

4. **XSS 防御之 URL 编码**

   ```js
   将不可信数据作为url参数值时需要经行url编码
   
   使用encodeURIComponent（url）
   ```

5. **XSS 防御之 CSS 编码**

   ```css
   编码规则：除了字母数字字符以外，使用\XXXXXX格式来转义ASCII值小于256的所有字符。 
   background-img：url（）
   
   function encodeForCSS (attr, str){
     let encoded = '';
     for (let i = 0; i < str.length; i++) {
       let ch = str.charAt(i);
       if (!ch.match(/[a-zA-Z0-9]/) {
         let hex = str.charCodeAt(i).toString(16);
         let pad = '000000'.substr((hex.length));
         encoded += '\\' + pad + hex;
       } else {
         encoded += ch;
       }
     }
     return encoded;
   };
   ```

   

### 解决方案:

**开启CSP网页安全政策防止XSS攻击**

```html
<meta http-equiv="Content-Security-Policy" content="">
  
<meta http-equiv="Content-Security-Policy" content="
default-src http: https:  *.xxx.com 'self' 'unsafe-inline' ;
style-src 'self' 'unsafe-inline' *.yyy.com;
script-src 'self' 'unsafe-inline' 'unsafe-eval' ;
">
```

## CSRF

CSRF跨站点请求伪造(Cross—Site Request Forgery)

```js


验证 HTTP Referer 字段；
	HTTP 请求头Referer 记录请求的来源地址 后台验证；
    
在请求地址中添加 token 并验证；
	防止请求伪造
```

# HTTP

## 常见状态码

```

```

