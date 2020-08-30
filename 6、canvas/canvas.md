## Canvas

```js
canvas Echarts 可视化
https://echarts.baidu.com/index.html  

svg D3
https://d3js.org/


canvas 文档:
https://www.runoob.com/tags/ref-canvas.html
```



## 创建

```js
 <canvas id="myCanvas" width="200" height="100"></canvas>
```



```js
var ctx = myCanvas.getContext('2d');

	ctx.beginPath();//开启新路径;
	ctx.moveTo(100,200.5);//起始坐标
	ctx.lineTo(200,100.5);//结束坐标
	ctx.strokeStyle='blue';//颜色
	ctx.lineWidth=10;	//线宽度
	ctx.stroke();//描边
	ctx.fill();//填充	非零环绕规则
	ctx.closePath();//自动闭合 尾部和头部相连闭合

	ctx.lineCap 线末端类型:butt round square
    ctx.lineJoin 相较的拐点样式 miter,round ,bevel平的
	ctx.setLineDash([5,10])  //虚线-- 参数[实,虚,实````]
	ctx.lineDashOffset=-20;  //需爱先偏移(负值往右)
	ctx.getLineDash() //获取虚线集合


	ctx.rect(x0,y0,w,h);//矩形,不独立,可被覆盖
	ctx.strokeRect(x0,y0,w,h);//独立路径
	ctx.fillRect(x0,y0,w,h);//填充矩形

	ctx.clearRect(x0,y0,w,h);//清除

	
    
```

## 绘制文字

```js
	文字的起点是在文字的左下角;
	ctx.font=''字体
	strokeText(text,x,y)//描边文字
	fillText(text,x,y)//填充

fillText(text,x,y,maxWidth)
	- text 要绘制的文本
	- x,y 文本绘制的坐标（文本左下角）
	- maxWidth 设置文本最大宽度，可选参数
    
ctx.textAlign文本水平对齐方式，相对绘制坐标来说的//相对起始点
	- left
	- center
	- right
	- start 默认
	- end

direction属性css(rtl ltr) start和end于此相关
	- 如果是ltr,start和left表现一致
	- 如果是rtl,start和right表现一致

ctx.textBaseline 设置基线（垂直对齐方式  ）
	- top 文本的基线处于文本的正上方，并且有一段距离
	- middle 文本的基线处于文本的正中间
	- bottom 文本的基线处于文本的证下方，并且有一段距离
	- hanging 文本的基线处于文本的正上方，并且和文本粘合
	- alphabetic 默认值，基线处于文本的下方，并且穿过文字
	- ideographic 和bottom相似，但是不一样
measureText() 获取文本宽度obj.width
```

## 渐变

```js
for(var i=0;i<255;i++){
	ctx.beginPath();
	ctx.moveTo(100+i-1,100);
	ctx.lineTo(100+i,100);
	ctx.strokeStyle='rgb('+i+',0,0)';
	ctx.stroke();
}
createLinearGradient(x,y,endx,endy);
createRadialGradient(x,y,r,x)

创建渐变方案
var linearGradient = ctx.createLinearGradient(x0,y0,x1,y1);//起点,结束点
linearGradient.addColorStop(0,'pink'); //渐变值0-1
linearGradient.addColorStop(0.5,'greed');

ctx.fillstyle=linearGradient;
```

## 绘制圆弧

```js
	坐标 x,y;半径r;起始弧度;结束弧度;direction顺时针(false)
	ctx.arc(100,100,150,0,Math.PI/2,false);

饼图
	var w = ctx.canvas.width;
	var h = ctx.canvas.height;
	ctx.moveTo(w/2,h/2);//设置起始点;
	ctx.arc(w/2,h/2,150,0,-Math.PI/2,true);
	ctx.closePath();//闭合
	
```

## 绘制图片

```js
var image = new Image();
image.src='image/01.png';
image.onload = function(){
    ctx.drawImage(image,x0,y0,w,h);//w,h是缩放 image可换成this
}


drawImage(image,px,py,vw,vh,x0,y0,w,h);
vw,图片可视区;
p,定位位置;
```

## 坐标变换

```css
- 平移 移动画布的原点
    - translate(x,y) 参数表示移动目标点的坐标
- 缩放
    - scale(x,y) 参数表示宽高的缩放比例
- 旋转
    - rotate(angle) 参数表示旋转角度
```



## 坐标案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        canvas {
            display: block;
            margin: 200px auto;
            border: 1px solid #ccc;
        }
    </style>
</head>

<body>
    <canvas width="600" height="400"></canvas>
    <script>
        var LineChart = function (ctx) {
            this.ctx = ctx || document.querySelector('canvas').getContext('2d');

            this.canvasWidth = this.ctx.canvas.width;
            this.canvasHeight = this.ctx.canvas.height;
            //网格大小
            this.gridSize = 10;
            //边距
            this.space = 20;
            //原点
            this.x0 = this.space;
            this.y0 = this.canvasHeight - this.space;
            this.strokeStyle='skyblue';
            this.fillStyle='red';
            //箭头大小
            this.arrowSize = 10;
            //绘制点大小
            this.dottedSize = 6;
        }
        //初始化
        LineChart.prototype.init = function (data) {
            this.drawGrid();
            this.drawAxis();
            this.drawDotted(data)
        }
        //绘制网格
        LineChart.prototype.drawGrid = function () {
            var yGrid = Math.floor(this.canvasHeight / this.gridSize);
            this.ctx.strokeStyle = '#ccc';
            for (var i = 0; i <= yGrid; i++) {
                this.ctx.beginPath();
                this.ctx.moveTo(0, i * this.gridSize - 0.5);
                this.ctx.lineTo(this.canvasWidth, i * this.gridSize - 0.5)
                this.ctx.stroke();
            }
            var xGrid = Math.floor(this.canvasWidth / this.gridSize);
            for (var i = 0; i <= xGrid; i++) {
                this.ctx.beginPath();
                this.ctx.moveTo(i * this.gridSize - 0, 5, 0);
                this.ctx.lineTo(i * this.gridSize - 0.5, this.canvasHeight);
                this.ctx.stroke();
            }

        }
        //绘制坐标
        LineChart.prototype.drawAxis = function () {
            this.ctx.strokeStyle = this.strokeStyle;
            this.ctx.beginPath();
            this.ctx.moveTo(this.x0, this.y0);
            this.ctx.lineTo(this.canvasWidth - (this.space), this.y0);
            this.ctx.lineTo(this.canvasWidth - (this.space) - this.arrowSize, this.y0 + this.arrowSize / 2);
            this.ctx.lineTo(this.canvasWidth - (this.space) - this.arrowSize, this.y0 - this.arrowSize / 2);
            this.ctx.lineTo(this.canvasWidth - (this.space), this.y0);
            this.ctx.stroke();
            this.ctx.fillStyle = this.fillStyle;
            this.ctx.fill();

            this.ctx.beginPath();
            this.ctx.moveTo(this.x0, this.y0);
            this.ctx.lineTo(this.x0, this.space);
            this.ctx.lineTo(this.x0 + this.arrowSize / 2, this.space + this.arrowSize);
            this.ctx.lineTo(this.x0 - this.arrowSize / 2, this.space + this.arrowSize);
            this.ctx.lineTo(this.x0, this.space);
            this.ctx.stroke();
            this.ctx.fill();
        }
        // 绘制点,并连接
        LineChart.prototype.drawDotted = function (data) {
            var _this = this;
            var prevx = 0;
            var prevy = 0;
            console.log('aaaa');
            for (var i = 0; i < data.length; i++) {
                var ctxx = this.x0 + data[i].x; //转为该坐标的点坐标
                var ctxy = this.y0 - data[i].y;
                this.ctx.beginPath();
                this.ctx.moveTo(ctxx-this.dottedSize/2,ctxy-this.dottedSize/2);
                this.ctx.lineTo(ctxx+this.dottedSize/2,ctxy-this.dottedSize/2);
                this.ctx.lineTo(ctxx+this.dottedSize/2,ctxy+this.dottedSize/2);
                this.ctx.lineTo(ctxx-this.dottedSize/2,ctxy+this.dottedSize/2);
                this.ctx.fill();
                if (i==0) {
                    this.ctx.beginPath();
                    this.ctx.moveTo(this.x0,this.y0);
                    this.ctx.lineTo(ctxx,ctxy);
                    this.ctx.stroke();
                    prevx=ctxx;
                    prevy=ctxy;
                }else{
                    this.ctx.beginPath();
                    this.ctx.moveTo(prevx,prevy);
                    this.ctx.lineTo(ctxx,ctxy);
                    this.ctx.stroke();
                    prevx=ctxx;
                    prevy=ctxy;
                }
            }
        }
        var data = [{
                x: 100,
                y: 120
            },
            {
                x: 200,
                y: 160
            },
            {
                x: 300,
                y: 240
            },
            {
                x: 400,
                y: 120
            },
            {
                x: 500,
                y: 80
            }
        ];
        var lineChart = new LineChart();
        lineChart.strokeStyle='#000';
        lineChart.init(data);

        // console.log(document.querySelector('canvas'));
    </script>
</body>

</html>
```

# 获取图片主题色

```js
  let image = document.getElementById('img')
        img.crossOrigin = '';
        console.log(image);

        image.onload = function () {
            let width = image.width;
            let height = image.height;
            let blockSize = 4
            let rgb = { r: 0, g: 0, b: 0 }
            let i = -4;
            let count = 0
            console.log('---', width, height);

            let canvas = document.createElement('canvas');
            canvas.width = width;
            canvas.height = height;

            let ctx = canvas.getContext("2d");
            ctx.drawImage(image, 0, 0);
            let data = ctx.getImageData(0, 0, width, height).data;
            let length = data.length
            while ((i += blockSize * 4) < length) {
                ++count;
                rgb.r += data[i];
                rgb.g += data[i + 1];
                rgb.b += data[i + 2];
            }
            rgb.r = ~~(rgb.r / count); // 取平均值
            rgb.g = ~~(rgb.g / count);
            rgb.b = ~~(rgb.b / count);
            let bg = document.getElementById('bg');
            // r: 65, g: 85, b: 21
            console.log(rgb);
            bg.style.backgroundColor = `rgb(${rgb.r},${rgb.g},${rgb.b})`
        }
```

跨域问题:

```js
 <img id="img" src="./static/img/d.jpg" crossorigin="anonymous" alt="">
     
加:crossorigin="anonymous" 好像不起作用;
本地调试:可用http-server
```

