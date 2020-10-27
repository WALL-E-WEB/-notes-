## JQuery

```js
官网传送门:<https://jquery.com/
中文:http://jquery.cuishifeng.cn/
```

JQ设计思想

```js
方法统一;
隐式迭代;
```

jq入口函数

```js
(2种语法)
$(function(){});
$(document).ready(function(){});

jq入口函数与原生入口函数的区别
​	a.数量不同:原生入口函数只能一个,jq可以多个;
​	b.加载时期不同:
​			jq入口函数:DOM树加载完毕就执行
​			原生入口函数:DOM树+所有外部资源路径
```

JQ对象

```js
使用jq语法获取的对象;
使用DOM语法获取的对象;
	DOM对象：使用js原生的api获取的元素对象;
	jQuery对象：使用jquery的方法

​JQ对象与DOM对象的区别:
	两者互不兼容:
		原生对象无法使用JQ语法;
		JQ对象不能使用原生语法;
    JQ对象的本质:一个伪数组.

​Dom 对象和 jq对象互转:
 	var box2 = $('#box')[0];
 	var box = $('#box').get(0);

	$(this)--把DOM对象 this 转成 jq对象;


​$是一个函数对象
	$函数对象三种功能:
		1.$("选择器"):获取元素;
		2.$(function(){}):入口函数;
		3.$(DOM对象):DOM->JQ;

```

### 获取

```js
与css一致
基本选择器:
	$('#id');
	$('.class');
	$('div');
	$('div,p'); 并集
    $('li.one');交集 
```

```js
层次选择器:
	$('ul>li');子代
    $('ul li');后代
    $('ul+li');
	$('ul~li');
```

```js
过滤选择器: $('选择器:过滤条件')//下标0开始
	$('li:odd');奇数
    $('li:even');偶数
    $('li:eq(1)');指定下标
    $('li').eq(index);可以放入变量;
```

### 属性操作

```js
特点:
	获取一切样式,(底层:windom.getComputedStyle);
	获取字符串,带单位;
	可以修改;

多个元素,获取操作操作只会返回第一个;
		设置操作(赋值)支持隐式迭代(遍历);
```



```js
CSS属性
	$('#id').css('属性名')
	$('#id').css('属性名',属性值)
	$('#id').css(
        {width:'100px'},
        {height:'200px'}
    );
	
```

```js
html属性
获取内容:
	$().text(); 获取
	$().text('内容');设置
    
	$().html();
标准属性,自定义
	$().attr();获取
    $().attr('属性名','属性值');设置
    
	$().removeAttr();
```

```js
input属性
	$().val() //value
	$().prop() //disabled checked selected 
```



### JQ节点操作

```js
获取子元素
	$().children();
	$().parent();
	$().prev();	//上一兄弟 prev
	$().next(); //下一兄弟
	
	JQ特有:
	$().siblings(); 
		除了自身之外所有同辈元素;
	$().find('选择器');
		获取所有子元素;//本质递归实现

$('ul').children('li'),子代的li;
$('ul').find('li'),所有后代的li

jq对象返回JQ对象,所以可链式语法;
	一个对象可以连续调用方法;
	原理:在方法中返回自身;
	
```

| 名称               | 用法                        | 描述                             |
| ------------------ | --------------------------- | :------------------------------- |
| children(selector) | $('ul').children('li')      | 相当于$('ul>li')，子类选择器     |
| find(selector)     | $('ul').find('li');         | 相当于$('ul li'),后代选择器      |
| siblings(selector) | $('#first').siblings('li'); | 查找兄弟节点，不包括自己本身。   |
| parent()           | $('#first').parent();       | 查找父亲                         |
| eq(index)          | $('li').eq(2);              | 相当于$('li:eq(2)'),index从0开始 |
| next()             | $('li').next()              | 找下一个兄弟                     |
| prev()             | $('li').prev()              | 找上一个兄弟                     |

```js
显示:$().show()    底层是设置display为block

隐藏： $().hide()    底层是设置display为none

$(this).children('ul').hide();

排他:
$(this).children().eq(index).show().sibilings().hide();
```

```js
onmouseente不支持事件冒泡;
onmouseover

onmouseleave 不支持事件冒泡
onmouseout
```

### index()

```js
$(this).index()   获取下标;
```

### 创建元素

```js
$().html('');	//innerHTML


$('')			//document.createElement();

var $str = $('<p>我我我哦我我</p>');
$('#div').append($str);

```

### 添加

```js
父元素.append(子元素);
子元素.appendTo(父元素); 添加到最后面;

父元素.prepend(子元素)	添加到最前面;
兄弟A.before(兄弟B)		B元素插入到A元素前面;
兄弟A.after(兄弟B)		B元素插入到A元素后面;
```

### 移除

```js
全部清空:
	$().html('');
	$().empty();	全部

单个移除
	$().remove(); 自杀; (底层:this.parentNode.removeChild(this);
```

### 类名操作

```js
$().addClass(''); //添加	不会覆盖原有类名
$().removeClass(''); //移除 
$().hasClass('');	//判断是否有类名  //返回 true or false
$().toggleClass(''); //如果有则移除,没有则添加
```



## 动画

show()

```js
显示动画 // 由display:none -->到地display:block的过程;
参数1:动画事件 时间 //可选 //fast:200  noraml:400 slow:600
参数2:动画完成回调函数 //可选
	$().show(1000,function(){
    
	})
$().show() 显示
$().show('') == $().show('noraml')

hide()

toggle();
有display:block 则隐藏
有display:none  则显示
```

滑入 滑出

```js
slideDown('时间',function(){});  //不填入默认noraml

slideUp()

slideToggle()
```

淡入 淡出

```js
第一个值://"slow","normal", or "fast"
第二个值://swing , linear
fadeIn() 淡入

fadeOut() 淡出

fadeToggle() 

fadeTo('时间','指定透明度',function(){
})
```

自定义动画

```js

属性对象
动画时间
动画速度  默认 缓动swing   匀速 linear
$().animate(
	{
		left:300,
		top:200,
	},2000,'swing',function(){
	
	}
)

stop(true,false);清除之前动画
$().stop(true,false).animate()
```

动画队列

```js
开始动画:多个动画排列依次执行
结束动画队列:以本次为准;

clearQueue:如果设置成true，则清空队列。可以立即结束动画。
jumpToEnd:如果设置成true，则完成队列。可以立即完成动画。

stop(stopAll,goToEnd)

stop(true,true) 结束动画  本次执行(瞬间到达);
stop(true,false)	结束动画,返回
stop(false,true) 	
stop(false,false) 默认
```



## 三大家族

```js
特性:
	特点与原生一样;
	不同的是可以更改,修改width/height;
outerWidth() / outerHeigth() //content + padding +border
	$().
width() / height() :

innerWidth() / innerHeight() : //width+padding

outerWidth(true) / outerHeigth(true) //content + padding +border+margin


position()
	特点:获取的是一个对象;不能修改;
	

offset();
	自生到整个页面左上角
    不定位也可获取;//jq会自动给元素加相对定位

	特点:可获取,可修改;
	$().offset({
        left:200,
        top:200
    })

获取页面可视区域大小;
	$(window).width();
	$(window).height();

$(window).resize(function(){

})



$(window).scrollLeft()
$(window).scrollTop()
	$(window).scroll(function(){
        $(window).scrollLeft();
        $(window).scrollTop();
    })
```

## 事件

```js
注册:
	$().click();
	$().bind();	//已取消	解决1
	$().delegate() //已取消 事件委托 ,原理事件冒泡 解决1.2
	$().on('click',function(){});

$().click():
	特点:
		1.不能一行注册两个事件;
		2.不能动态添加事件;

document.body.onclick=function(e){
    if(e.target.nodeName == 'DIV'){
        shijian
    }
}

$().on('click',function(){});
	1.同时注册;
	2.动态注册;
		给元素注册:不支持动态注册;
		给body注册:支持;
	$().on(click mouseenter ,'div',function(){
        
    })
```

### 移除事件

```js
$().off('click');
$().off() //不传参 移除所有事件
```

### 事件触发

```js
事件主动触发:
原生:ele.onclick();触发事件;

 $().trigger('click'); 触发事件;
---------------------------------------------
js原生:
	let btn_1 = document.getElementById('btn-1');
    let btn_2 = document.getElementById('btn-2');
    	btn_1.onclick = function () {
        	var myEvent = new Event('click');
        	btn_2.dispatchEvent(myEvent);
    	}
    btn_2.onclick = function () {
        alert('OK');
    // do something
    }
--------------------- 
```

### 事件对象

```js
JQ事件对象和原生一样;JQ解决兼容问题;

$().on('click',function(e){
    e.pageX;
    e.target;
})

$().on('keydown', function(){
    e.keyCode  //
})
```

### 自定义事件

```js
var CLICK_EVENT_KEY = 'click-bounced';
var BOUNCING_DURATION = 1000;
$.event.special[CLICK_EVENT_KEY] = {
  bindType: 'click',
  handle(event){
  	if ($(this).data('clicking')){
    	return
  	}else{
    	$(this).data('clicking', true);
    	event.handleObj.handler.apply(this, arguments);
    	var _this = this;
    setTimeout(function(){
      $(_this).data('clicking', false);
    }, BOUNCING_DURATION)
  }
  }
}

$('button.bounced').on(CLICK_EVENT_KEY, function(){
  let num = Number(document.querySelector('.alert').innerHTML);
  document.querySelector('.alert').innerHTML = ++ num;
});
```



## 链式语法注意点

```jq
设置类的方法,返回jq对象;
获取类的方法,返回的属性值;不能链式,如:text(),

end()返回上一级DOM div
```



显示迭代

```js
$('li').each(function(index,ele){
	console.log(index);//下标
	console.log(elem); DOM元素
})
```

查看jq版本号

```js
console.log($.fn.jquery)
console.log(JQuery.fn.jquery)
console.log($.prototype.jquery)
```

如实现多库共存

```js
释放$控制器

var $3 = $.noConFlict(); 
console.log($3.fn.jquery)//使用库3 用$3
console.log($.fn.jquery)

任然想使用$ 用$3
(function($){
    里面$是$3;
})($3)
外面是 $ 是$
```
