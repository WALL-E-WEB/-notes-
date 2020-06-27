# Dart

## 变量

```js
var name = 1  //可重复赋值

final name = new Date.now() //不可重复赋值,可为表达式

const name = 1 //不可重复赋值,常量
final a = const [] //创建常量值端构造函数

String name = '1' //指定类型
```

## 数据类型

```dart
Number 
    int doulbe	 // 类型 num
String	
Boolean
List (也被称为 Array)
Map //对象
Set	//无序数组 唯一值
Rune (用于在字符串中表示 Unicode 字符)
Symbol
```

- int

  ```
  移位<< >>  按位与^ 按位或|
  assert((3 << 1) == 6); // 0011 << 1 == 0110
  assert((3 >> 1) == 1); // 0011 >> 1 == 0001
  assert((3 | 4) == 7); // 0011 | 0100 == 0111
  ```

- String

  ```dart
  $表达式
  var name = 'walle'
  print('abc$name'); // abcwalle
  
  + 拼接
  ''' ''', """ """ 保持换行空格样式;
  
  ```

- Boolean

  ```dart
  // 检查空字符串。
  var fullName = '';
  assert(fullName.isEmpty);
  
  // 检查 0 值。
  var hitPoints = 0;
  assert(hitPoints <= 0);
  
  // 检查 null 值。
  var unicorn;
  assert(unicorn == null);
  
  // 检查 NaN 。
  var iMeantToDoThis = 0 / 0;
  assert(iMeantToDoThis.isNaN);
  ```

- Set

  ```dart
  var names = <String>{};
  // Set<String> names = {}; // 这样也是可以的。
  // var names = {}; // 这样会创建一个 Map ，而不是 Set 。
  ```

- Map

  ```dart
  var gifts = Map();
  var gifts =new Map(); //new 可选
  gifts['first'] = 'partridge';
  常量声明
  final constantMap = const {
    2: 'helium',
    10: 'neon',
    18: 'argon',
  };
  ```

  

## 数据转换

```dart
String --> int
var one = int.parse('1')

String --> double
var one = double.parse('1')

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

## 函数

```dart
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}

isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}

bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

- 参数

  ```dart
  可选参数
  String say(String from, String msg, [String device]) {
    var result = '$from says $msg';
    if (device != null) {
      result = '$result with a $device';
    }
    return result;
  }
  ```

  ```dart
  默认参数
  void enableFlags({bool bold = false, bool hidden = false}) {...}
  ```

  ```dart
  list map 默认参数
  void doStuff(
      {List<int> list = const [1, 2, 3],
      Map<String, String> gifts = const {
        'first': 'paper',
        'second': 'cotton',
        'third': 'leather'
      }}) {
    print('list:  $list');
    print('gifts: $gifts');
  }
  ```

  

## 类

封装 继承 多态

```dart
class Person {
  // 变量
  String name = 'walle';
  int age = 13;
  // new 时传入参数
  Person(this.name, this.age); //与初始化二存一
  // 命名构造函数 且传入参数
  Person.now(a, b) {
    this.age = a;
    this.name = b;
  }
  // 初始化
  // Person()
  //     : age = 18,
  //       name = "walle" {
  //   print(age);
  // }
  // 私有属性,方法 为文件时有效
  int _flag;
  void _run() {
    print(this._flag);
  }
  // 静态
  static int age2 = 200; //调用 静态不用 this ;age2外部可访问
  static void func(){} //无法访问非静态方法和属性
  // get 类似计算属性
  String get reutnName {
    return this.name;
  }

  // set
  set setAge(num b) {
    this.age = b;
  }

  void fun(a) {
    print("${age}:${this.name}+$a");
  }
}

main() {
  var p1 = new Person('w', 10);
  var age2 = Person.age2; //访问静态
  var func = Person.func(); //访问静态方法
  var p2 = new Person.now(1, 's');
  p1.fun(22);
  print(p1.name);
}

```

```dart
? 	条件运算符 //判断类属性,方法是否为空 安全操作
as	类型转换  //(p as className).name
is	类型判断  //
..	级联操作
	Person p1 new Person()
	p1..name="walle"
	  ..age=30;
```

### 继承

```dart
class Web extends Person{
   String sex;
  // 给Person 传参数
  //Web(String name, int age) : super(name, age);
Web(String name, int age, String sex) : super(name, age){
    this.sex = sex;
  }
  //重写父类属性
  @override
  void fun(a){
    super.age; //调用父类属性 方法
  }
}
```

### 多态 - 抽象类 方法

```dart
多态:
	每个子类有不同的表现;

//子类必须定义抽象方法;
abstract class Doer { //抽象类 不能实例化,只有子类可以实例化
  // 定义实例变量和方法 ...

  void doSomething(); // 定义一个抽象方法。
  void func(){
      //抽象类的方法
  }
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // 提供方法实现，所以这里的方法就不是抽象方法了...
  }
}
```

接口

```dart
class Impostor implements Person {
  get _name => '';
	
  String greet(String who) => 'Hi $who. Do you know who I am?';
}
```

------



# flutter

hello world

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Welcome to Flutter',
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Welcome to Flutter'),
        ),
        body: new Center(
          child: new Text('Hello World'),
        ),
      ),
    );
  }
}
```

命令

```
flutter packages get
flutter run
```

## 生命周期

```
上图就是 State 的生命周期图。

StatefulWidget.createState()

Framework 调用会通过调用 StatefulWidget.createState() 来创建一个 State。

initState()

新创建的 State 会和一个 BuildContext 产生关联，此时认为 State 已经被安装好了，initState() 函数将会被调用。

通常，我们可以重写这个函数，进行初始化操作。

didChangeDependencies()

在 initState() 调用结束后，这个函数会被调用。

事实上，当 State 对象的依赖关系发生变化时，这个函数总会被 Framework 调用。

build()

经过以上步骤，系统认为一个 State 已经准备好了，就会调用 build() 来构建视图。

我们需要在这个函数中，返回一个 Widget。

deactivate()

当 State 被暂时从视图树中移除时，会调用这个函数。

页面切换时，也会调用它，因为此时 State 在视图树中的位置发生了变化，需要先暂时移除后添加。

⚠️注意，重写的时候必须要调用 super.deactivate()。

dispose()

当 State 被永久的从视图树中移除，Framework 会调用该函数。

在销毁前触发，我们可以在这里进行最终的资源释放。

在调用这个函数之前，总会先调用 deactivate()。

⚠️注意，重写的时候必须要调用 super.dispose()。

didUpdateWidget(covariant T oldWidget)

当 widget 的配置发生变化时，会调用这个函数。

比如，Hot-reload 的时候就会调用这个函数。

这个函数调用后，会调用 build()。

setState()

当我需要更新 State 的视图时，需要手动调用这个函数，它会触发 build() 。
```

```
当sestate 执行时会触发 build;

initstate

build

dispose


```

## 事件event

```dart

gesturedetector

点击:
	onTapDown: 		用户手指按下
    onTapUp: 		手指抬起
	onTap: 			点击完成
    onTapCancel: 	按下过程取消

双击:
	onDoubleTap: 	双击

长按:
	onLongPress:	在屏幕上保持一段时间

纵向拖拽:
	onVerticalDragStart: 	接触并开始纵向移动
    onVerticalDragUpdate:	移动
	onVerticalDragEnd:		结束


横向拖拽:
	onHorizontlDragStart: 	接触并开始纵向移动
    onHorizontlDragUpdate:	移动
	onHorizontlDragEnd:		结束
        
globalPosition  获取相对屏幕位置
localPosition	相对于Widget位置信息
```

```dart
body:Listener(
		onPointerDown:(event){
			event.position		// 屏幕中位置
			event.localPosition // 在组件中的位置
		}
	)
指针事件:
	onPointerDownEvent
    onPointerMoveEvent
    onPoiinterUpEvent 
    onPointerCancelEvent

```

事件传递

```dart
event_bus
```



## StatelessWidget

## StatefullWidget

```dart
StatelessWidget //无状态
StatefullWidget //可变状态
```

## MaterialApp

https://api.flutter.dev/flutter/material/MaterialApp-class.html

```dart
MaterialApp({
  Key key,
  this.title = '', // 设备用于为用户识别应用程序的单行描述
  this.home, // 应用程序默认路由的小部件,用来定义当前应用打开的时候，所显示的界面
  this.color, // 在操作系统界面中应用程序使用的主色。
  this.theme, // 应用程序小部件使用的颜色。
  this.routes = const <String, WidgetBuilder>{}, // 应用程序的顶级路由表
  this.navigatorKey, // 在构建导航器时使用的键。
  this.initialRoute, // 如果构建了导航器，则显示的第一个路由的名称
  this.onGenerateRoute, // 应用程序导航到指定路由时使用的路由生成器回调
  this.onUnknownRoute, // 当 onGenerateRoute 无法生成路由(initialRoute除外)时调用
  this.navigatorObservers = const <NavigatorObserver>[], // 为该应用程序创建的导航器的观察者列表
  this.builder, // 用于在导航器上面插入小部件，但在由WidgetsApp小部件创建的其他小部件下面插入小部件，或用于完全替换导航器
  this.onGenerateTitle, // 如果非空，则调用此回调函数来生成应用程序的标题字符串，否则使用标题。
  this.locale, // 此应用程序本地化小部件的初始区域设置基于此值。
  this.localizationsDelegates, // 这个应用程序本地化小部件的委托。
  this.localeListResolutionCallback, // 这个回调负责在应用程序启动时以及用户更改设备的区域设置时选择应用程序的区域设置。
  this.localeResolutionCallback, // 
  this.supportedLocales = const <Locale>[Locale('en', 'US')], // 此应用程序已本地化的地区列表 
  this.debugShowMaterialGrid = false, // 打开绘制基线网格材质应用程序的网格纸覆盖
  this.showPerformanceOverlay = false, // 打开性能叠加
  this.checkerboardRasterCacheImages = false, // 打开栅格缓存图像的棋盘格
  this.checkerboardOffscreenLayers = false, // 打开渲染到屏幕外位图的图层的棋盘格
  this.showSemanticsDebugger = false, // 打开显示框架报告的可访问性信息的覆盖
  this.debugShowCheckedModeBanner = true, // 在选中模式下打开一个小的“DEBUG”横幅，表示应用程序处于选中模式
}) 
```

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Welcome to Flutter',
      theme:new ThemeData(
      	primaryColor: Colors.
      ),
    );
  }
}
```

## 底部导航栏

```dart

import 'package:flutter/material.dart';

class BottomBar extends StatefulWidget {
  @override
  BottomBarState createState() => BottomBarState();
}

class BottomBarState extends State<BottomBar> {
  @override
  Widget build(BuildContext context) {
    return BottomNavigationBar(
      items: [
        BottomNavigationBarItem(
            icon: Icon(
              Icons.home,
              color: Colors.blue,
            ),
            title: Text('HOME', style: TextStyle(color: Colors.blue))),
        BottomNavigationBarItem(
            icon: Icon(
              Icons.home,
              color: Colors.blue,
            ),
            title: Text('HOME', style: TextStyle(color: Colors.blue)))
      ],
    );
  }
}

mixin StateBottomBar {}

```

```
import 'package:flutter/material.dart';

import './pages/main_BottomBar/main_BottomBar.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Welcome to Flutter',
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Welcome to Flutster'),
        ),
        body: new Center(
          // child: new Text(
          //   'Hello Worlds',
          //   textDirection: TextDirection.ltr,
          //   style: TextStyle(
          //       fontSize: 14.0, color: Color.fromRGBO(255, 122, 122, .5)),
          // ),
          heightFactor: 1,
          widthFactor: 1,
          // child: new HomeContent(),
          // child: new ImageCom(),
          child: ListView(
            children: <Widget>[
              ListTile(
                title: Text('title'),
                subtitle: Text('data'),
                trailing: Text('trailing'),
                isThreeLine: true,
                dense: true,
                onLongPress: () {
                  print('222');
                },
              ),

              TextField(
                  decoration: InputDecoration(
                      hintText: 'dddd',
                      border: OutlineInputBorder(),
                      labelText: '用户')),
              SizedBox(height: 20),
              TextField(
                  obscureText: true,
                  decoration: InputDecoration(
                      hintText: 'dddd',
                      border: OutlineInputBorder(),
                      labelText: '用户')),

              // MyInput()
            ],
          ),
          // child: new PaddingTestRoute(),
        ),
       bottomNavigationBar:BottomBar(),
      ),
    );
  }
}
```



## 布局

### container

```dart
class HomeContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Text('ss'),
      height: 200.0,
      width: 300.0,
      padding:EdgeInsets.all(20.0),
      alignment:Alignment.centerRight,
      decoration: BoxDecoration(
          color: Colors.yellow,
          border: Border.all(
            width: 1.0,
            color: Colors.blue,
          )),
    );
  }
}
```

### Align

```dart
const Align({
    Key key,
    this.alignment = Alignment.center,
    this.widthFactor,
    this.heightFactor,
    Widget child,
})
```

### Row

```dart
Row({
    Key key,
    // 主轴 水平方向
    MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
    MainAxisSize mainAxisSize = MainAxisSize.max,
    // 主轴 垂直方向
    CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
    TextDirection textDirection,
    VerticalDirection verticalDirection = VerticalDirection.down,
    TextBaseline textBaseline,
    List<Widget> children = const <Widget>[],
  })
```

### Column

```dart
 Column({
    Key key,
     // 主轴 垂直方向
    MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
     // 盒子 max=block min=aline
    MainAxisSize mainAxisSize = MainAxisSize.max,
     // 副轴	水平方向
    CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
    TextDirection textDirection,
     // item 排序方式 
    VerticalDirection verticalDirection = VerticalDirection.down,
    TextBaseline textBaseline,
    List<Widget> children = const <Widget>[],
  })
```

### Expanded

```dart
body:Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: <Widget>[
    Center(child:Text('I am JSPang')),
      // 当前元素 最大占据
    Expanded(child:Center(child:Text('my website is jspang.com'))),
    Center(child:Text('I love coding'))
  ],
)
```

### CircleAvatar

```dart
  const CircleAvatar({
    Key key,
    this.child,
    this.backgroundColor,
    this.backgroundImage,
    this.onBackgroundImageError,
    this.foregroundColor,
    this.radius,
    this.minRadius,
    this.maxRadius,
  })
```

### Stack

```dart
 Stack({
    Key key,
    this.alignment = AlignmentDirectional.topStart,
    this.textDirection,
    this.fit = StackFit.loose,
    this.overflow = Overflow.clip,
    List<Widget> children = const <Widget>[],
  })
     
     
var stack = new Stack(

        children: <Widget>[
          new CircleAvatar(
            backgroundImage: new NetworkImage('http://jspang.com/static//myimg/blogtouxiang.jpg'),
            radius: 100.0,
          ),
          new Positioned(
            top:10.0,
            left:10.0,
            child: new Text('JSPang.com'),
          ),
          new Positioned( // 定位
            bottom:10.0,
            right:10.0,
            child: new Text('技术胖'),
          )
        ],
      );
```

sliverList

sliverAppBar

pageview.builder 有懒加载

## 辅助样式

color

```dart
Color _bottombarcolor = Color(0xFFF63515);
```



### padding

```dart
	用法:
Padding(
	padding: const EdgeInsets.all(10.0),
	child: Text("title")
)

    属性:
padding:
	EdgeInsets.all(10.0); //全部 padding:
	EdgeInsets.only(	//padding-top:
    	left:20.0,
        top:20.0,
        right:20.0,
        bottom:20.0,
    );
	EdgeInsets.symmetric(
    	vertical:100.0, //垂直方向 padding-top/bottom 100
        horizontal:100.0  //水平方向
    );
	EdgeInsets.fromLTRB(
    	left:10.0,
        top:10.0,
        right:10.0,
        bottom:10.0,
    )
```

### Alignment

```dart
const Align({
    Key key,
    this.alignment = Alignment.center,
    this.widthFactor,
    this.heightFactor,
    Widget child
  })
    


alignment: 
	Alignment.center,
	Alignment.topLeft,
	Alignment.topCenter,
	Alignment.topRight,
	Alignment.centerLeft,
	Alignment(x,y), //中心为(0,0) (1,1)为右下角
```

### textDirection

```dart
// 文字排列方式
textDirection:
	TextDirection.ltr;
	TextDirection.rtl;
```

### BoxFit

```dart
fit:
	BoxFit.fit 			//全图显示 充满父容器
	BoxFit.contain		//全图显示 显示原比例 可能会有空隙
	BoxFit.cover		//显示可能拉伸，可能裁切，充满
	BoxFit.fitWidth		//宽度充满 会拉伸
	BoxFit.fitHeight	//高度充满
	BoxFit.scaleDown	//不允许显示超过源图片大小，可小不可大
```



## image

- Image.asset 本地

  ```dart
   Image.asset(
      String name, {
      Key key,
      AssetBundle bundle,
      this.frameBuilder,
      this.errorBuilder,
      this.semanticLabel,
      this.excludeFromSemantics = false,
      double scale,
      this.width,
      this.height,
      this.color,
      this.colorBlendMode,
      this.fit,
          |-BoxFit.cover //不变形
      this.alignment = Alignment.center,
      this.repeat = ImageRepeat.noRepeat,
      this.centerSlice,
      this.matchTextDirection = false,
      this.gaplessPlayback = false,
      String package,
      this.filterQuality = FilterQuality.low,
      int cacheWidth,
      int cacheHeight,
    })
  ```

  ```dart
  lib同级目录下 创建images文件
  
  |-images
  	|-2.0x
  	|-3.0x
  	|-a.png
  	
  new Image.asset('images/logo.png')
      
  
  ```

  ```
   pubspec.yaml 
   
  flutter:
  
    # The following line ensures that the Material Icons font is
    # included with your application, so that you can use the icons in
    # the material Icons class.
    uses-material-design: true
    assets:
      - images/logo.png
      - images/2.0x/logo.png
      - images/3.0x/logo.png
  ```

  

- Image.network 网路

  ```dart
  new Image.network ('https://test.jpg'))
  ```

- Image.file

  ```dart
  加载本地图片
  new Image.file(new File('/storage/xxx/xxx/test.jpg'))
  ```

  

## form

```dart

class MyStatefulWidget extends StatefulWidget {
  MyStatefulWidget({Key key}) : super(key: key);
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  final _formKey = GlobalKey<FormState>();
  var userName = new TextEditingController(); // 声明

  @override
  void initState() {
    super.initState();
    userName.text = '22220';
  }
    var flag = true;
  @override
  Widget build(BuildContext context) {
    
    return Form(
      key: _formKey,
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: <Widget>[
          TextFormField(
            
            decoration: const InputDecoration(
              hintText: 'Enter your email',
            ),
            validator: (value) {
              if (value.isEmpty) {
                return 'Please enter some text';
              }
              return null;
            },
            controller: userName, //绑定
            onChanged: (value){
              print('$value');
              print(userName.text); // 双向绑定
            },
          ),
          Padding(
            padding: const EdgeInsets.symmetric(vertical: 16.0),
            child: RaisedButton(
              onPressed: () {
                // Validate will return true if the form is valid, or false if
                // the form is invalid.
                if (_formKey.currentState.validate()) {
                  // Process data.
                  print('sss');
                }
              },
              child: Text('Submit'),
            ),
          ),
             Checkbox(value:this.flag, onChanged: (value){
            setState(() {
              this.flag = value;
              print(!value);
            });
          })
        ],
      ),
    );
  }
}

```



checkbox

```
RadioListTile(
              value: 1,
              onChanged: (v) {
                setState(() {
                  this.sex = v;
                });
              },
              groupValue: this.sex,
            ),
```

```
  RadioListTile(
            groupValue: this.sex,
            onChanged: (value) {
              print(value);
              setState(() {
                this.sex = value;
              });
            },
            value: 1,
            title: Text('sss'),
          ),
```

## routes

```dart
navigattor.of(context).push(MaterialPageRoute(
	builder:(ctx){
		return aboutPage()
	}
))
    
Navigator.push(MaterialPageRoute(
	builder:(ctx){
		return aboutPage()
	}
))
    
    
Navigator.of().pushNamed('/home') //命名路由
```

钩子

```
onGenerateRoute(settings)

onUnkonwnRoute  //不存在路由
```

例

```
routes:{
	'/home':(context)=>About()
},
initialRoute:'/', //默认路径
onGenerateRoute:(settings){
	if(settings.name == '/home'){
		return MaterialPageRoute(
			builder:(context)=>HOme(settings.arguments)
		);
	}
},
onUnkonwnRoute(){
	return MaterialPageRoute(
			builder:(context)=>Eer(settings.arguments)
		);
}

```

