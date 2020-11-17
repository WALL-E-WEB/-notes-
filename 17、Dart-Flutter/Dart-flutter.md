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
  https://www.cnblogs.com/lxlx1798/p/11280106.html
  
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

  ## Map
  
  创建
  
  ```dart
  创建Map: var map1 = {"first":"Dart",1:true,true:"2"};
  创建不可变Map: var map2 = const{"first":"Dart",1:true,true:"2"};
  
  构造创建：var map3 = new Map();
  ```
  
  
  
  ```dart
  	常用属性：
          keys            获取所有的key值
          values          获取所有的value值
          isEmpty         是否为空
          isNotEmpty      是否不为空
      常用方法:
          remove(key)     删除指定key的数据
          addAll({...})   合并映射  给映射内增加属性
          containsValue   查看映射内的值  返回true/false
          forEach   
          map
          where
          any
          every
       常用操作   
          [],length,keys,values,
          containsKey,
          containsValue,
          remove,forEach 
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

  

## String

```
https://www.cnblogs.com/lxlx1798/p/11280106.html
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



## 定时器

```dart
import 'dart:async';

 Timer timeoutId;


const timeout = const Duration(seconds: 5);
print('currentTime='+DateTime.now().toString()); // 当前时间
timeoutId = Timer(timeout, () { //callback function
  print('afterTimer='+DateTime.now().toString()); // 5s之后
});

const timeout = const Duration(seconds: 1);
timeoutId = Timer.periodic(timeout, (timer) { //callback function
  //1s 回调一次
  print('afterTimer='+DateTime.now().toString());
  
  timer.cancel();  // 取消定时器
}
               
               
```

清除定时器

```
 
 @override
 void dispose() {
  super.dispose();
  timeoutId.cancel();
 }
```



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
flutter ctrate 项目名称  // 创建项目


flutter packages get // 类似 npm i
flutter run			// 运行
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

```dart
Inkwell 和 GestureDetector区别

  new InkWell(
    child: new Text("Click me!"),
    onTap: () {
      // 单击
    },
    onDoubleTap: () {
      // 双击
    },
    onLongPress: () {
      // 长按
    }
  );
  
  
  GestureDetector: 
  		是无状态组件 
  		无水波纹

  Inkwell:
  		水波纹
  		widget
            
可自定义水波纹:
	Ink(
        highlightColor: Colors.purple[800], //颜色在最上层 会覆盖
    	splashColor:Color.red
    )
```

事件传递

```dart
event_bus //第三方库
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

| key   | type      | detail                       |
| ----- | --------- | ---------------------------- |
| title | String    | 为用户识别应用程序的单行描述 |
| theme | ThemeData |                              |
|       |           |                              |

ThemeData

```dart
factory ThemeData({
  Brightness brightness, // 应用整体主题的亮度。用于按钮之类的小部件，以确定在不使用主色或强调色时选择什么颜色。
  MaterialColor primarySwatch,// 定义一个单一的颜色以及十个色度的色块。
  Color primaryColor, // 应用程序主要部分的背景颜色(toolbars、tab bars 等)
  Brightness primaryColorBrightness, // primaryColor的亮度。用于确定文本的颜色和放置在主颜色之上的图标(例如工具栏文本)。
  Color primaryColorLight, // primaryColor的浅色版
  Color primaryColorDark, // primaryColor的深色版
  Color accentColor, // 小部件的前景色(旋钮、文本、覆盖边缘效果等)。
  Brightness accentColorBrightness, // accentColor的亮度。
  Color canvasColor, //  MaterialType.canvas 的默认颜色
  Color scaffoldBackgroundColor, // Scaffold的默认颜色。典型Material应用程序或应用程序内页面的背景颜色。
  Color bottomAppBarColor, // BottomAppBar的默认颜色
  Color cardColor, // Card的颜色
  Color dividerColor, // Divider和PopupMenuDivider的颜色，也用于ListTile之间、DataTable的行之间等。
  Color highlightColor, // 选中在泼墨动画期间使用的突出显示颜色，或用于指示菜单中的项。
  Color splashColor,  // 墨水飞溅的颜色。InkWell
  InteractiveInkFeatureFactory splashFactory, // 定义由InkWell和InkResponse反应产生的墨溅的外观。
  Color selectedRowColor, // 用于突出显示选定行的颜色。
  Color unselectedWidgetColor, // 用于处于非活动(但已启用)状态的小部件的颜色。例如，未选中的复选框。通常与accentColor形成对比。也看到disabledColor。
  Color disabledColor, // 禁用状态下部件的颜色，无论其当前状态如何。例如，一个禁用的复选框(可以选中或未选中)。
  Color buttonColor, // RaisedButton按钮中使用的Material 的默认填充颜色。
  ButtonThemeData buttonTheme, // 定义按钮部件的默认配置，如RaisedButton和FlatButton。
  Color secondaryHeaderColor, // 选定行时PaginatedDataTable标题的颜色。
  Color textSelectionColor, // 文本框中文本选择的颜色，如TextField
  Color cursorColor, // 文本框中光标的颜色，如TextField
  Color textSelectionHandleColor,  // 用于调整当前选定的文本部分的句柄的颜色。
  Color backgroundColor, // 与主色形成对比的颜色，例如用作进度条的剩余部分。
  Color dialogBackgroundColor, // Dialog 元素的背景颜色
  Color indicatorColor, // 选项卡中选定的选项卡指示器的颜色。
  Color hintColor, // 用于提示文本或占位符文本的颜色，例如在TextField中。
  Color errorColor, // 用于输入验证错误的颜色，例如在TextField中
  Color toggleableActiveColor, // 用于突出显示Switch、Radio和Checkbox等可切换小部件的活动状态的颜色。
  String fontFamily, // 文本字体
  TextTheme textTheme, // 文本的颜色与卡片和画布的颜色形成对比。
  TextTheme primaryTextTheme, // 与primaryColor形成对比的文本主题
  TextTheme accentTextTheme, // 与accentColor形成对比的文本主题。
  InputDecorationTheme inputDecorationTheme, // 基于这个主题的 InputDecorator、TextField和TextFormField的默认InputDecoration值。
  IconThemeData iconTheme, // 与卡片和画布颜色形成对比的图标主题
  IconThemeData primaryIconTheme, // 与primaryColor形成对比的图标主题
  IconThemeData accentIconTheme, // 与accentColor形成对比的图标主题。
  SliderThemeData sliderTheme,  // 用于呈现Slider的颜色和形状
  TabBarTheme tabBarTheme, // 用于自定义选项卡栏指示器的大小、形状和颜色的主题。
  CardTheme cardTheme, // Card的颜色和样式
  ChipThemeData chipTheme, // Chip的颜色和样式
  TargetPlatform platform, 
  MaterialTapTargetSize materialTapTargetSize, // 配置某些Material部件的命中测试大小
  PageTransitionsTheme pageTransitionsTheme, 
  AppBarTheme appBarTheme, // 用于自定义Appbar的颜色、高度、亮度、iconTheme和textTheme的主题。
  BottomAppBarTheme bottomAppBarTheme, // 自定义BottomAppBar的形状、高度和颜色的主题。
  ColorScheme colorScheme, // 拥有13种颜色，可用于配置大多数组件的颜色。
  DialogTheme dialogTheme, // 自定义Dialog的主题形状
  Typography typography, // 用于配置TextTheme、primaryTextTheme和accentTextTheme的颜色和几何TextTheme值。
  CupertinoThemeData cupertinoOverrideTheme 
})
```

AppBarTheme

```dart
  const AppBarTheme({
    this.brightness,
    this.color, 	// 背景颜色
    this.elevation, // 阴影辐射范围 default 4.0
    this.shadowColor,
    this.iconTheme,
    this.actionsIconTheme,
    this.textTheme,
    this.centerTitle,
  });
```



## Scaffold

![image-20200704124550478](Dart-flutter.assets/image-20200704124550478.png)

## appbar

```dart
AppBar({
    Key key,
    this.leading, //widget类型，即可任意设计样式，表示左侧leading区域，通常为icon，如返回icon
    this.automaticallyImplyLeading = true, // 如果leading!=null，该属性不生效；如果leading==null且为true，左侧leading区域留白；如果leading==null且为false，左侧leading区域扩展给title区域使用
    this.title,//widget类型，即可任意设计样式，表示中间title区域，通常为标题栏
    this.actions,// List<Widget>类型，即可任意设计样式，表示右侧actions区域，可放置多个widget，通常为icon，如搜索icon、菜单icon
    this.flexibleSpace,
    this.bottom, //PreferredSizeWidget类型，appbar底部区域，通常为Tab控件
    this.elevation, //阴影高度，默认为4
    this.shape,//ShapeBorder 类型，表示描边形状
    this.backgroundColor, //Color类型，背景色 
    this.brightness,//Brightness类型，表示当前appbar主题是亮或暗色调，有dark和light两个值，可影响系统状态栏的图标颜色
    this.iconTheme, //IconThemeData类型，可影响包括leading、title、actions中icon的颜色、透明度，及leading中的icon大小。
    this.actionsIconTheme,
    this.textTheme,// TextTheme类型，文本主题样式，可设置appbar中文本的许多样式，如字体大小、颜色、前景色、背景色等...
    this.primary = true,//true时，appBar会以系统状态栏高度为间距显示在下方；false时，会和状态栏重叠，相当于全屏显示。
    this.centerTitle, // boolean 类型，表示标题是否居中显示
    this.titleSpacing = NavigationToolbar.kMiddleSpacing,//title区域水平方向与leading和actions的间距(padding)
    this.toolbarOpacity = 1.0,//toolbar区域透明度
    this.bottomOpacity = 1.0,//bottom区域透明度
  }
```



## 显示隐藏状态

```dart
import 'package:flutter/services.dart';

   //显示底部栏(隐藏顶部状态栏)
//    SystemChrome.setEnabledSystemUIOverlays([SystemUiOverlay.bottom]);
    //显示顶部栏(隐藏底部栏)
//    SystemChrome.setEnabledSystemUIOverlays([SystemUiOverlay.top]);
    //隐藏底部栏和顶部状态栏
    SystemChrome.setEnabledSystemUIOverlays([]);
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

## SliverAppBar

```dart
 const SliverAppBar({
    Key key,
    this.leading,//左侧的图标或文字，多为返回箭头
    this.automaticallyImplyLeading = true,//没有leading为true的时候，默认返回箭头，没有leading且为false，则显示title
    this.title,//标题
    this.actions,//标题右侧的操作
    this.flexibleSpace,//可以理解为SliverAppBar的背景内容区
    this.bottom,//SliverAppBar的底部区
    this.elevation,//阴影
    this.forceElevated = false,//是否显示阴影
    this.backgroundColor,//背景颜色
    this.brightness,//状态栏主题，默认Brightness.dark，可选参数light
    this.iconTheme,//SliverAppBar图标主题
    this.actionsIconTheme,//action图标主题
    this.textTheme,//文字主题
    this.primary = true,//是否显示在状态栏的下面,false就会占领状态栏的高度
    this.centerTitle,//标题是否居中显示
    this.titleSpacing = NavigationToolbar.kMiddleSpacing,//标题横向间距
    this.expandedHeight,//合并的高度，默认是状态栏的高度加AppBar的高度
    this.floating = false,//滑动时是否悬浮
    this.pinned = false,//标题栏是否固定
    this.snap = false,//配合floating使用
  })
```

滚动到指定位置

```dart
 onTap: () {
      _pageScroll.animateTo(
          _pageScroll.position.minScrollExtent, //滚动到顶部部
          duration: const Duration(milliseconds: 300),
                      curve: Curves.easeOut,
                    );
  },
```

## Dialog

```dart
https://juejin.im/post/6844903822028963847
Future<T> showDialog<T>({
  @required BuildContext context,
  // 点击 dialog 外部是否可消失
  bool barrierDismissible = true,
  // 构建 Dialog 视图
  WidgetBuilder builder,
})

    
    如果要更新 dialog中的视图
    科技加一层StatefulBuilder建立自身的 setstate；
```

```dart
showDialog<Future>(
      context: context,
      barrierDismissible: false,
      useRootNavigator: true,
      useSafeArea: true,
      builder: (BuildContext context) {
      	 BuildContext iscontext = context; // 父级的
         bool isShowPhone = true;
        return StatefulBuilder(builder: (context, state // 自己的setstate) {
        	return Widget
        }
      }

```



## Widget

### Text

```dart
 Text(
        "Text组件的使用",
        style: TextStyle(
            // 文字颜色
            color: Color(0xfff0000),
            // none 不显示装饰线条，underline 字体下方，overline 字体上方，lineThrough穿过文字
            decoration: TextDecoration.none,
            // solid 直线，double 双下划线，dotted 虚线，dashed 点下划线，wavy 波浪线
            decorationStyle: TextDecorationStyle.solid,
            // 装饰线的颜色
            decorationColor: Colors.red,
            // 文字大小
            fontSize: 15.0,
            // normal 正常，italic 斜体
            fontStyle: FontStyle.normal,
            // 字体的粗细
            fontWeight: FontWeight.bold,
            // 文字间的宽度
            letterSpacing: 1.0,
            // 文本行与行的高度，作为字体大小的倍数（取值1~2，如1.2）
            height: 1,
            //对齐文本的水平线:
            //TextBaseline.alphabetic：文本基线是标准的字母基线
            //TextBaseline.ideographic：文字基线是表意字基线；
            //如果字符本身超出了alphabetic 基线，那么ideograhpic基线位置在字符本身的底部。
            textBaseline: TextBaseline.alphabetic),
        // 段落的间距样式
        strutStyle: StrutStyle(
          fontFamily: 'serif',
          fontFamilyFallback: ['monospace', 'serif'],
          fontSize: 20,
          height: 2,
          leading: 2.0,
          fontWeight: FontWeight.w300,
          fontStyle: FontStyle.normal,
          forceStrutHeight: true,
          debugLabel: 'text demo',
        ),
        // 文字对齐方式
        textAlign: TextAlign.center,
        // 文字排列方向 ltr 左到右，rtl右到左
        textDirection: TextDirection.ltr,
        // 用于选择区域特定字形的语言环境
        locale: Locale('zh_CN'),
        // 软包裹 ，文字是否应该在软断行出断行
        softWrap: false,
        // 如何处理视觉溢出:clip 剪切溢出的文本以修复其容器。ellipsis 使用省略号表示文本已溢出。fade 将溢出的文本淡化为透明。
        overflow: TextOverflow.clip,
        // 文字的缩放比例
        textScaleFactor: 1.0,
        // 文本要跨越的可选最大行数,
        maxLines: 2,
        // 图像的语义描述，用于向Andoid上的TalkBack和iOS上的VoiceOver提供图像描述
        semanticsLabel: 'text demo',
        textWidthBasis: TextWidthBasis.longestLine,
      )
```

## Offstage

```
 控制child是否显示
 const Offstage({ Key key, this.offstage = true, Widget child })
```

## PreferredSize

```
   Scaffold( 
        appBar: PreferredSize(
        child: AppBar(
        ),
        preferredSize: Size.fromHeight(screenSize.height * 0.07))
);
```

## tabber

```dart
 Key key,
    @required this.tabs,
    this.controller,
    this.isScrollable = false, 				//是否可滚动
    this.indicatorColor,					//指示器颜色
    this.indicatorWeight = 2.0,				//指示器厚度
    this.indicatorPadding = EdgeInsets.zero,//底部指示器的Padding

    this.indicator,						//指示器decoration，例如边框等
    this.indicatorSize, //指示器大小计算方式
    this.labelColor,
    this.labelStyle,
    this.labelPadding,
    this.unselectedLabelColor,
    this.unselectedLabelStyle,
    this.dragStartBehavior = DragStartBehavior.start,
    this.mouseCursor,
    this.onTap,
    this.physics,
```

## SliverAppBar

```dart
 const SliverAppBar({
    Key key,
    this.leading,//左侧的图标或文字，多为返回箭头
    this.automaticallyImplyLeading = true,//没有leading为true的时候，默认返回箭头，没有leading且为false，则显示title
    this.title,//标题
    this.actions,//标题右侧的操作
    this.flexibleSpace,//可以理解为SliverAppBar的背景内容区
    this.bottom,//SliverAppBar的底部区
    this.elevation,//阴影
    this.forceElevated = false,//是否显示阴影
    this.backgroundColor,//背景颜色
    this.brightness,//状态栏主题，默认Brightness.dark，可选参数light
    this.iconTheme,//SliverAppBar图标主题
    this.actionsIconTheme,//action图标主题
    this.textTheme,//文字主题
    this.primary = true,//是否显示在状态栏的下面,false就会占领状态栏的高度
    this.centerTitle,//标题是否居中显示
    this.titleSpacing = NavigationToolbar.kMiddleSpacing,//标题横向间距
    this.expandedHeight,//合并的高度，默认是状态栏的高度加AppBar的高度
    this.floating = false,//滑动时是否悬浮
    this.pinned = false,//标题栏是否固定
    this.snap = false,//配合floating使用
  })
```

```dart
      body: new CustomScrollView(
        slivers: <Widget>[
          new SliverAppBar(
            leading: GestureDetector(
              child: Icon(Icons.arrow_back),
              onTap: () => Navigator.pop(context),
            ), //左侧按钮
            /**
             * 如果没有leading，automaticallyImplyLeading为true，就会默认返回箭头
             * 如果 没有leading 且为false，空间留给title
             * 如果有leading，这个参数就无效了
             */
            automaticallyImplyLeading: true,
            // title: Text('大标题'), //标题
            centerTitle: true, //标题是否居中
            actions: [Icon(Icons.archive)], //右侧的内容和点击事件啥的
            elevation: 4, //阴影的高度
            forceElevated: false, //是否显示阴影
            backgroundColor: Colors.green, //背景颜色
            brightness: Brightness.dark, //黑底白字，lignt 白底黑字
            iconTheme: IconThemeData(
                color: Colors.red,
                size: 30,
                opacity: 1), //所有的icon的样式,不仅仅是左侧的，右侧的也会改变
            textTheme: TextTheme(), //字体样式
            primary: true, // appbar是否显示在屏幕的最上面，为false是显示在最上面，为true就显示在状态栏的下面
            titleSpacing: 16, //标题两边的空白区域
            expandedHeight: 200.0, //默认高度是状态栏和导航栏的高度，如果有滚动视差的话，要大于前两者的高度
            floating: false, //滑动到最上面，再滑动是否隐藏导航栏的文字和标题等的具体内容，为true是隐藏，为false是不隐藏
            pinned: true, //是否固定导航栏，为true是固定，为false是不固定，往上滑，导航栏可以隐藏
            snap:
                false, //只跟floating相对应，如果为true，floating必须为true，也就是向下滑动一点儿，整个大背景就会动画显示全部，网上滑动整个导航栏的内容就会消失
            flexibleSpace: new FlexibleSpaceBar(
              title: new Text("随内容一起滑动的头部"),
              centerTitle: true,
              collapseMode: CollapseMode.pin,
            ),
          ),
          new SliverFixedExtentList(
            itemExtent: 150.0,
            delegate:
                new SliverChildBuilderDelegate((context, index) => new ListTile(
                      title: new Text("List item $index"),
                    )),
          )
        ],
      ),
```



```dart
滚动 浮动
http://www.ptbird.cn/flutter-customscrollview-floating-appbar.html
```

示例

```dart
TabController _controller;

@override
  void initState() {
    super.initState();
    _controller = TabController(
      length: _tabValues.length,
      vsync: ScrollableState(),
    );
  }

Container(
            child: TabBar(
              tabs: _tabValues.map((f) {
                return Text(f);
              }).toList(),
              controller: _controller,
              indicatorColor: Colors.red,
              indicatorSize: TabBarIndicatorSize.tab,
              isScrollable: true,
              labelColor: Colors.red,
              unselectedLabelColor: Colors.black,
              indicatorWeight: 5.0,
              labelStyle: TextStyle(height: 2),
            ),
          ),

 Container(
            // width: 750,
            height: 600.0, // 非body时 需要指定高度
            child: TabBarView(
              controller: _controller,
              children: _tabValues.map((f) {
                return Center(
                  child: Text(f),
                );
              }).toList(),
            ),
          ),
```

## 主题ThemeData

```dart
factory ThemeData({
  Brightness brightness, // 应用整体主题的亮度。用于按钮之类的小部件，以确定在不使用主色或强调色时选择什么颜色。
  MaterialColor primarySwatch,// 定义一个单一的颜色以及十个色度的色块。
  Color primaryColor, // 应用程序主要部分的背景颜色(toolbars、tab bars 等)
  Brightness primaryColorBrightness, // primaryColor的亮度。用于确定文本的颜色和放置在主颜色之上的图标(例如工具栏文本)。
  Color primaryColorLight, // primaryColor的浅色版
  Color primaryColorDark, // primaryColor的深色版
  Color accentColor, // 小部件的前景色(旋钮、文本、覆盖边缘效果等)。
  Brightness accentColorBrightness, // accentColor的亮度。
  Color canvasColor, //  MaterialType.canvas 的默认颜色
  Color scaffoldBackgroundColor, // Scaffold的默认颜色。典型Material应用程序或应用程序内页面的背景颜色。
  Color bottomAppBarColor, // BottomAppBar的默认颜色
  Color cardColor, // Card的颜色
  Color dividerColor, // Divider和PopupMenuDivider的颜色，也用于ListTile之间、DataTable的行之间等。
  Color highlightColor, // 选中在泼墨动画期间使用的突出显示颜色，或用于指示菜单中的项。
  Color splashColor,  // 墨水飞溅的颜色。InkWell
  InteractiveInkFeatureFactory splashFactory, // 定义由InkWell和InkResponse反应产生的墨溅的外观。
  Color selectedRowColor, // 用于突出显示选定行的颜色。
  Color unselectedWidgetColor, // 用于处于非活动(但已启用)状态的小部件的颜色。例如，未选中的复选框。通常与accentColor形成对比。也看到disabledColor。
  Color disabledColor, // 禁用状态下部件的颜色，无论其当前状态如何。例如，一个禁用的复选框(可以选中或未选中)。
  Color buttonColor, // RaisedButton按钮中使用的Material 的默认填充颜色。
  ButtonThemeData buttonTheme, // 定义按钮部件的默认配置，如RaisedButton和FlatButton。
  Color secondaryHeaderColor, // 选定行时PaginatedDataTable标题的颜色。
  Color textSelectionColor, // 文本框中文本选择的颜色，如TextField
  Color cursorColor, // 文本框中光标的颜色，如TextField
  Color textSelectionHandleColor,  // 用于调整当前选定的文本部分的句柄的颜色。
  Color backgroundColor, // 与主色形成对比的颜色，例如用作进度条的剩余部分。
  Color dialogBackgroundColor, // Dialog 元素的背景颜色
  Color indicatorColor, // 选项卡中选定的选项卡指示器的颜色。
  Color hintColor, // 用于提示文本或占位符文本的颜色，例如在TextField中。
  Color errorColor, // 用于输入验证错误的颜色，例如在TextField中
  Color toggleableActiveColor, // 用于突出显示Switch、Radio和Checkbox等可切换小部件的活动状态的颜色。
  String fontFamily, // 文本字体
  TextTheme textTheme, // 文本的颜色与卡片和画布的颜色形成对比。
  TextTheme primaryTextTheme, // 与primaryColor形成对比的文本主题
  TextTheme accentTextTheme, // 与accentColor形成对比的文本主题。
  InputDecorationTheme inputDecorationTheme, // 基于这个主题的 InputDecorator、TextField和TextFormField的默认InputDecoration值。
  IconThemeData iconTheme, // 与卡片和画布颜色形成对比的图标主题
  IconThemeData primaryIconTheme, // 与primaryColor形成对比的图标主题
  IconThemeData accentIconTheme, // 与accentColor形成对比的图标主题。
  SliderThemeData sliderTheme,  // 用于呈现Slider的颜色和形状
  TabBarTheme tabBarTheme, // 用于自定义选项卡栏指示器的大小、形状和颜色的主题。
  CardTheme cardTheme, // Card的颜色和样式
  ChipThemeData chipTheme, // Chip的颜色和样式
  TargetPlatform platform, 
  MaterialTapTargetSize materialTapTargetSize, // 配置某些Material部件的命中测试大小
  PageTransitionsTheme pageTransitionsTheme, 
  AppBarTheme appBarTheme, // 用于自定义Appbar的颜色、高度、亮度、iconTheme和textTheme的主题。
  BottomAppBarTheme bottomAppBarTheme, // 自定义BottomAppBar的形状、高度和颜色的主题。
  ColorScheme colorScheme, // 拥有13种颜色，可用于配置大多数组件的颜色。
  DialogTheme dialogTheme, // 自定义Dialog的主题形状
  Typography typography, // 用于配置TextTheme、primaryTextTheme和accentTextTheme的颜色和几何TextTheme值。
  CupertinoThemeData cupertinoOverrideTheme 
})
```

## safearea

```
屏幕适配
```



## webview

```
插件
https://pub.dev/packages/webview_flutter
```

```dart
拦截返回
import 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart';

class Case extends StatefulWidget {
  Case({Key key, this.title}) : super(key: key);
  final String title;
  @override
  _CaseState createState() => _CaseState();
}

class _CaseState extends State<Case> {
  String url = 'https://m.jia.top/sz/design/index?hideLeftArrow=1';
  WebViewController _webViewController;
  Future<bool> _requestPop() {
    // Navigator.of(context).pop(100);

    ///弹出页面并传回int值100，用于上一个界面的回调
    // return new Future.value(false);
    Future canGoBack = _webViewController.canGoBack();
    canGoBack.then((str) {
      if (str) {
        _webViewController.goBack();
      } else {
        Navigator.of(context).pop();
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return WillPopScope(
      child: WebView(
        initialUrl: url,
        javascriptMode: JavascriptMode.unrestricted,
        onWebViewCreated: (WebViewController webViewController) {
          // 在WebView创建完成后会产生一个 webViewController
          _webViewController = webViewController;
        },
      ),
      onWillPop: _requestPop,
    );
  }
}

```



## 布局

### container

绘制顺序

1. transform
2. decoration
3. child
4. foregroundDecoration

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

|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |



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



## Wrap

|                    |      |      |
| ------------------ | ---- | ---- |
| direction          | axis |      |
| alignment          |      |      |
| runSpacing         |      |      |
| runAlignment       |      |      |
| crossAxisAlignment |      |      |
| VerticalDirection  |      |      |
| textDirection      |      |      |
| children           |      |      |

```dart
 Wrap({
    Key key,
    this.direction = Axis.horizontal,   //排列方向，默认水平方向排列
    this.alignment = WrapAlignment.start,  //子控件在主轴上的对齐方式
    this.spacing = 0.0,  //主轴上子控件中间的间距
    this.runAlignment = WrapAlignment.start,  //子控件在交叉轴上的对齐方式
    this.runSpacing = 0.0,  //交叉轴上子控件之间的间距
    this.crossAxisAlignment = WrapCrossAlignment.start,   //交叉轴上子控件的对齐方式
    this.textDirection,   //textDirection水平方向上子控件的起始位置
    this.verticalDirection = VerticalDirection.down,  //垂直方向上子控件的其实位置
    List<Widget> children = const <Widget>[],   //要显示的子控件集合
  })
```



### 辅助布局

#### center

```

```

|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |

#### SizeBox



#### AspectRatio



#### FractionallySizedBox

#### card

## Transform

```dart
Transform(
     origin: Offset(57.w / 2, 34.h / 2),
     transform: Matrix4.rotationZ(pi / 2),
     child: Image.asset(
            'images/next.png',
             width: 57.w,
             height: 34.h,
           ),
  ),
```



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

### Icon

```dart
Icon(
   Icons.search,
   color: Color(0xffcccccc),
   size:18.0,
),
```

BoxDecoration

```
gradient:LinearGradient() //.渐变
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

### input

```dart
const TextField({
    Key key,
    this.controller,    //编辑框的控制器，跟文本框的交互一般都通过该属性完成，如果不创建的话默认会自动创建
    this.focusNode,  //用于管理焦点
    this.decoration = const InputDecoration(),   //输入框的装饰器，用来修改外观
    TextInputType keyboardType,   //设置输入类型，不同的输入类型键盘不一样
    this.textInputAction,   //用于控制键盘动作（一般位于右下角，默认是完成）
    this.textCapitalization = TextCapitalization.none,
    this.style,    //输入的文本样式
    this.textAlign = TextAlign.start,   //输入的文本位置
    this.textDirection,    //输入的文字排列方向，一般不会修改这个属性
    this.autofocus = false,   //是否自动获取焦点
    this.obscureText = false,   //是否隐藏输入的文字，一般用在密码输入框中
    this.autocorrect = true,   //是否自动校验
    this.maxLines = 1,   //最大行
    this.maxLength,   //能输入的最大字符个数
    this.maxLengthEnforced = true,  //配合maxLength一起使用，在达到最大长度时是否阻止输入
    this.onChanged,  //输入文本发生变化时的回调
    this.onEditingComplete,   //点击键盘完成按钮时触发的回调，该回调没有参数，(){}
    this.onSubmitted,  //同样是点击键盘完成按钮时触发的回调，该回调有参数，参数即为当前输入框中的值。(String){}
    this.inputFormatters,   //对输入文本的校验
    this.enabled,    //输入框是否可用
    this.cursorWidth = 2.0,  //光标的宽度
    this.cursorRadius,  //光标的圆角
    this.cursorColor,  //光标的颜色
    this.keyboardAppearance,
    this.scrollPadding = const EdgeInsets.all(20.0),
    this.dragStartBehavior = DragStartBehavior.down,
    this.enableInteractiveSelection,
    this.onTap,    //点击输入框时的回调(){}
    this.buildCounter,
  })

```

### 表单验证

```
https://www.jianshu.com/p/3fb613ffac22
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

### TextField

```
https://www.cnblogs.com/joe235/p/11711653.html
```

复制粘贴设置成中文

```
-pubspec.yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
```

```dart
return MaterialApp(
  localizationsDelegates: [
    GlobalMaterialLocalizations.delegate,
    GlobalWidgetsLocalizations.delegate,
  ],
  supportedLocales: [
    const Locale('zh', 'CN'),
    const Locale('en', 'US'),
  ]
}

```



```dart
 Key key,
    this.controller,                    // 控制正在编辑文本
    this.focusNode,                     // 获取键盘焦点
    this.decoration = const InputDecoration(),              // 边框装饰
    TextInputType keyboardType,         // 键盘类型
    this.textInputAction,               // 键盘的操作按钮类型
    this.textCapitalization = TextCapitalization.none,      // 配置大小写键盘
    this.style,                         // 输入文本样式
    this.textAlign = TextAlign.start,   // 对齐方式
    this.textDirection,                 // 文本方向
    this.autofocus = false,             // 是否自动对焦
    this.obscureText = false,           // 是否隐藏内容，例如密码格式
    this.autocorrect = true,            // 是否自动校正
    this.maxLines = 1,                  // 最大行数
    this.maxLength,                     // 允许输入的最大长度
    this.maxLengthEnforced = true,      // 是否允许超过输入最大长度
    this.onChanged,                     // 文本内容变更时回调
    this.onEditingComplete,             // 提交内容时回调
    this.onSubmitted,                   // 用户提示完成时回调
    this.inputFormatters,               // 验证及格式
    this.enabled,                       // 是否不可点击
    this.cursorWidth = 2.0,             // 光标宽度
    this.cursorRadius,                  // 光标圆角弧度
    this.cursorColor,                   // 光标颜色
    this.keyboardAppearance,            // 键盘亮度
    this.scrollPadding = const EdgeInsets.all(20.0),        // 滚动到视图中时，填充边距
    this.enableInteractiveSelection,    // 长按是否展示【剪切/复制/粘贴菜单LengthLimitingTextInputFormatter】
    this.onTap,  
```



```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

///整理
//TextField 输入文本 decoration 配置边框样式以及提示文本分析篇
class TextFeildHomePage5 extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return TextFeildHomePageState();
  }
}

class TextFeildHomePageState extends State {

  ///用来控制  TextField 焦点的获取与关闭
  FocusNode focusNode = new FocusNode();
  ///文本输入框是否可编辑
  bool isEnable = true;

  @override
  void initState() {
    super.initState();

    ///添加获取焦点与失去焦点的兼听
    focusNode.addListener((){
      ///当前兼听的 TextFeild 是否获取了输入焦点
      bool hasFocus = focusNode.hasFocus;
      ///当前 focusNode 是否添加了兼听
      bool hasListeners = focusNode.hasListeners;

      print("focusNode 兼听 hasFocus:$hasFocus  hasListeners:$hasListeners");
    });

    /// WidgetsBinding 它能监听到第一帧绘制完成，第一帧绘制完成标志着已经Build完成
    WidgetsBinding.instance.addPostFrameCallback((_) {
      ///获取输入框焦点
      FocusScope.of(context).requestFocus(focusNode);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        actions: <Widget>[
          FlatButton(child: Text("获取焦点"),onPressed: (){
            FocusScope.of(context).requestFocus(focusNode);
          },),
          FlatButton(child: Text("失去焦点"),onPressed: (){
            focusNode.unfocus();
          },),
          FlatButton(child: Text("编辑"),onPressed: (){
            setState(() {
              isEnable = true;
            });
          },),
          FlatButton(child: Text("不可编辑"),onPressed: (){
            setState(() {
              isEnable = false;
            });
          },),
        ],
      ),
      body: Container(
        ///SizedBox 用来限制一个固定 width height 的空间
        child: SizedBox(
          width: 400,
          height: 130,
          child: Container(
            color: Colors.white24,
            ///距离顶部
            margin: EdgeInsets.only(top: 30),
            padding: EdgeInsets.all(10),
            ///Alignment 用来对齐 Widget
            alignment: Alignment(0, 0),
            ///文本输入框
            child: TextField(

              ///是否可编辑
              enabled: isEnable,
              ///焦点获取
              focusNode: focusNode,
              ///用来配置 TextField 的样式风格
              decoration: InputDecoration(
                ///设置输入文本框的提示文字
                ///输入框获取焦点时 并且没有输入文字时
                hintText: "请输入用户名",
                ///设置输入文本框的提示文字的样式
                hintStyle: TextStyle(color: Colors.grey,textBaseline: TextBaseline.ideographic,),
                ///输入框内的提示 输入框没有获取焦点时显示
                labelText: "用户名",
                labelStyle: TextStyle(color: Colors.blue),
                ///显示在输入框下面的文字
                helperText: "这里是帮助提示语",
                helperStyle: TextStyle(color: Colors.green),

                ///显示在输入框下面的文字
                ///会覆盖了 helperText 内容
                errorText: "这里是错误文本提示",
                errorStyle: TextStyle(color: Colors.red),

                ///输入框获取焦点时才会显示出来 输入文本的前面
                prefixText: "prefix",
                prefixStyle: TextStyle(color: Colors.deepPurple),
                ///输入框获取焦点时才会显示出来 输入文本的后面
                suffixText: "suf ",
                suffixStyle: TextStyle(color: Colors.black),

                ///文本输入框右下角显示的文本
                ///文字计数器默认使用
                counterText: "count",
                counterStyle:TextStyle(color: Colors.deepPurple[800]),

                ///输入文字前的小图标
                prefixIcon: Icon(Icons.phone),
                ///输入文字后面的小图标
                suffixIcon: Icon(Icons.close),

                ///与 prefixText 不能同时设置
//                prefix: Text("A") ,
                /// 与 suffixText 不能同时设置
//                suffix:  Text("B") ,
                ///设置边框
                ///   InputBorder.none 无下划线
                ///   OutlineInputBorder 上下左右 都有边框
                ///   UnderlineInputBorder 只有下边框  默认使用的就是下边框
                border: OutlineInputBorder(
                  ///设置边框四个角的弧度
                  borderRadius: BorderRadius.all(Radius.circular(10)),
                  ///用来配置边框的样式
                  borderSide: BorderSide(
                    ///设置边框的颜色
                    color: Colors.red,
                    ///设置边框的粗细
                    width: 2.0,
                  ),
                ),
                ///设置输入框可编辑时的边框样式
                enabledBorder: OutlineInputBorder(
                  ///设置边框四个角的弧度
                  borderRadius: BorderRadius.all(Radius.circular(10)),
                  ///用来配置边框的样式
                  borderSide: BorderSide(
                    ///设置边框的颜色
                    color: Colors.blue,
                    ///设置边框的粗细
                    width: 2.0,
                  ),
                ),
                disabledBorder: OutlineInputBorder(
                  ///设置边框四个角的弧度
                  borderRadius: BorderRadius.all(Radius.circular(10)),
                  ///用来配置边框的样式
                  borderSide: BorderSide(
                    ///设置边框的颜色
                    color: Colors.red,
                    ///设置边框的粗细
                    width: 2.0,
                  ),
                ),
                ///用来配置输入框获取焦点时的颜色
                focusedBorder: OutlineInputBorder(
                  ///设置边框四个角的弧度
                  borderRadius: BorderRadius.all(Radius.circular(20)),
                  ///用来配置边框的样式
                  borderSide: BorderSide(
                    ///设置边框的颜色
                    color: Colors.green,
                    ///设置边框的粗细
                    width: 2.0,
                  ),
                ),
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

### 失去焦点

```dart
 GestureDetector(
       behavior: HitTestBehavior.translucent,
       onTap: () {
          FocusScope.of(context).requestFocus(FocusNode());
  },
 ）
```



## 点击事件

```dart
InkWell,GestureDetector,RaisedButton。
```

GestureDetector

```dart
GestureDetector

behavior:
	HitTestBehavior.opaque  // 事件可穿透
    HitTestBehavior.deferToChild // child处理事件
	HitTestBehavior.translucent // 自己和child都可以响应事件
```



# routes

MaterialPageRoute

`MaterialPageRoute`继承自`PageRoute`类，`PageRoute`类是一个抽象类，表示占有整个屏幕空间的一个模态路由页面，它还定义了路由构建及切换时过渡动画的相关接口及属性。`MaterialPageRoute` 是Material组件库提供的组件，它可以针对不同平台，实现与平台页面切换动画风格一致的路由切换动画：

```
  MaterialPageRoute({
    WidgetBuilder builder,
    RouteSettings settings,
    bool maintainState = true,
    bool fullscreenDialog = false, //返回按键变X
  });
 
```

- `builder` 是一个WidgetBuilder类型的回调函数，它的作用是构建路由页面的具体内容，返回值是一个widget。我们通常要实现此回调，返回新路由的实例。
- `settings` 包含路由的配置信息，如路由名称、是否初始路由（首页）。
- `maintainState`：默认情况下，当入栈一个新路由时，原来的路由仍然会被保存在内存中，如果想在路由没用的时候释放其所占用的所有资源，可以设置`maintainState`为false。
- `fullscreenDialog`表示新的路由页面是否是一个全屏的模态对话框，在iOS中，如果`fullscreenDialog`为`true`，新页面将会从屏幕底部滑入（而不是水平方向）。

普通路由:

```dart
import '../home/HomeTest.dart';

//进入
navigattor.of(context).push(MaterialPageRoute(
	builder:(context){
		return HomeTest()
	}
))
//进入    
 Navigator.push(
          context,
          MaterialPageRoute(builder: (context) {
            return HomeTest();
          }),
        );
//返回
 Navigator.of(context).pop();

Navigator.of().pushNamed('/home') //命名路由
```

普通路由传值:

```dart
 Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) {
              return HomeTest(title:'wo');
            },
          ),
        ); // 传值

class HomeTest extends StatefulWidget {
  HomeTest({Key key, this.title}) : super(key: key);
  final String title; //接收
  @override
  _HomeTestState createState() => _HomeTestState();
}

class _HomeTestState extends State<HomeTest> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title:Text(widget.title), // 赋值
      ),
      body: Text('data'),
    );
  }
}
```

命名路由:

```dart
申明:
main.dart
import 'package:flutter/material.dart';
import './routers/router.dart';
import './home/HomeTest.dart';
    void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      routes:{
        '/home':(context)=>HomeTest(), //申明 全局引用
      },
      initialRoute: "/",
      onGenerateRoute: onGenerateRoute,
    );
  }
};

页面调用:
  Navigator.pushNamed(context, '/home',);
```

动态图命名路由传值:

```
 Navigator.pushNamed(context, '/HomeTest',arguments: {'title':'4444'}); 传参数;
 
```

```
import 'package:flutter/material.dart';
import '../Tabs/Tabs.dart'; //配置路由
import '../home/HomeTest.dart';
动态路由配置:
final routes = {
  '/': (context) => Tabs(),
  '/HomeTest': (context, {arguments}) => HomeTest(arguments: arguments),
};


// ignore: top_level_function_literal_block
var onGenerateRoute = (RouteSettings settings) {
  // 统一处理
  final String name = settings.name;
  final Function pageContentBuilder = routes[name];

  if (pageContentBuilder != null) {
    if (settings.arguments != null) {
      print(name);
      final Route route = MaterialPageRoute(
          builder: (context) =>
              pageContentBuilder(context, arguments: settings.arguments));
      return route;
    } else {
      final Route route =
          MaterialPageRoute(builder: (context) => pageContentBuilder(context));
      return route;
    }
  }
};

```

```dart
import 'package:flutter/material.dart';

class HomeTest extends StatefulWidget {
  final arguments; // 接收
  HomeTest({Key key, this.arguments}) : super(key: key);

  @override
  _HomeTestState createState() => _HomeTestState();
}

class _HomeTestState extends State<HomeTest> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.arguments['title']), //使用
      ),
      body: FloatingActionButton(
        child: Text('2'),
        onPressed: () {
          Navigator.of(context).pop();
        },
      ),
    );
  }
}

```

页面返回返回参数:

```dart
 Navigator.of(context).pop('返回'); // 传参

写法一:
Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) {
              return HomeTest(arguments:{'title':'mytitle'});
            },
            // fullscreenDialog: true,
          ),
        ).then((value){
          print('222222');
          print(value);
        });
写法二:
Future future = Navigator.pushNamed(
          context,
          '/HomeTest',
          arguments: {'title': '上个页面的title'},
        );
        future.then((value) {
          print('value--------');
          print(value);
        });
写法三:    
 Navigator.of(context).pushNamed(
          '/HomeTest',
          arguments: {'title': '上个页面的title'},
        ).then((value) {
          print(value);
          print('999');
        });

注:点击顶部返回,手机手势返回;不能捕获参数;

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

```dart
import 'package:flutter/material.dart';
import '../Tabs/Tabs.dart'; //配置路由

final routes = {
  '/': (context) => Tabs(),
}; //固定写法

var onGenerateRoute = (RouteSettings settings) {
  // 统一处理
  final String name = settings.name;
  final Function pageContentBuilder = routes[name];
  if (pageContentBuilder != null) {
    if (settings.arguments != null) {
      final Route route = MaterialPageRoute(
          builder: (context) =>
              pageContentBuilder(context, arguments: settings.arguments));
      return route;
    } else {
      final Route route =
          MaterialPageRoute(builder: (context) => pageContentBuilder(context));
      return route;
    }
  }
};



```



# bottomNavigationBar

```dart
import 'package:flutter/material.dart';
import './Category.dart';
import './Home.dart';
import './My.dart';
import './User.dart';

class Tabs extends StatefulWidget {
  Tabs({Key key, this.title}) : super(key: key);
  final String title;
  @override
  _TabsState createState() => _TabsState();
}

class _TabsState extends State<Tabs> {
  int _currentIndex = 0;

  List _TabsPages = [Home(), Category(), My(), User()];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: _TabsPages[this._currentIndex],
      bottomNavigationBar: BottomNavigationBar(
          currentIndex: this._currentIndex,
          onTap: (index) {
            setState(() {
              this._currentIndex = index;
            });
          },
          type: BottomNavigationBarType.fixed, // 多个底部导航栏需要配置
          items: [
            BottomNavigationBarItem(
              title: Text("首页"),
              icon: Icon(Icons.home),
            ),
            BottomNavigationBarItem(
              title: Text("分类"),
              icon: Icon(Icons.category),
            ),
            BottomNavigationBarItem(
              title: Text("购物车"),
              icon: Icon(Icons.shopping_cart),
            ),
            BottomNavigationBarItem(
              title: Text("我的"),
              icon: Icon(Icons.people),
            ),
          ]),
    );
  }
}

```

```dart
main.dart

import 'package:flutter/material.dart';
import "./Tabs/Tabs.dart";
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.red,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: Tabs(title: 'walle JD'),
    );
  }
}


```

# 获取定位

1. 申请高德key；

2. 创建应用；

3. 获取sha1，获取包名；

4. ```
   keytool -list -v -keystore F:/androiddebugkey.jks
   ```

   

5. 声明权限；

```
参考：https://blog.csdn.net/qq_42772570/article/details/101671009
https://blog.csdn.net/Gemini_Kanon/article/details/104628500?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduend~default-4-104628500.nonecase&utm_term=flutter%20%E8%8E%B7%E5%8F%96%E4%BD%8D%E7%BD%AE%E4%BF%A1%E6%81%AF&spm=1000.2123.3001.4430
https://lbs.amap.com/faq/android/map-sdk/create-project/43112
```

参考：https://blog.csdn.net/qq_44749053/article/details/101102785

```
依赖：
  amap_location: ^0.2.0
  permission_handler: ^3.2.0 // 权限判断

引入：
import 'package:amap_location/amap_location.dart';
import 'package:permission_handler/permission_handler.dart'; //权限
```

```dart
检查权限：
 //检测权限状态
  void checkPersmission() async {
    // 申请权限
    Map<PermissionGroup, PermissionStatus> permissions =
        await PermissionHandler()
            .requestPermissions([PermissionGroup.location]);
    // 申请结果
    PermissionStatus permission = await PermissionHandler()
        .checkPermissionStatus(PermissionGroup.location);
    if (permission == PermissionStatus.granted) {
      _getLocation();
    } else {
      print('定位权限申请被拒绝');
      bool isOpened = await PermissionHandler().openAppSettings(); //打开应用设置
    }
  }
```

```dart
监听：
void _getLocation() async {
    //先启动一下
    await AMapLocationClient.startup(new AMapLocationOption(
        desiredAccuracy: CLLocationAccuracy.kCLLocationAccuracyHundredMeters));

    //直接获取定位
    var result = await AMapLocationClient.getLocation(true);
    print('result--$result');
    print("""
    经度：${result.longitude}
    纬度：${result.latitude}
    """);
    var lat = result.latitude;
    var lng = result.longitude;
    if (lat.toString().isNotEmpty && lng.toString().isNotEmpty) {
    } else {
      print('获取位置失败，请检测GPS是否开启！');
    }
    // 关闭
    // AMapLocationClient.stopLocation();
    //停止定位

    //监听定位
    // AMapLocationClient.onLocationUpate.listen((AMapLocation loc) {
    //   if (!mounted) return;
    //   setState(() {
    //     print("""
    // 经度：${result.longitude}
    // 纬度：${result.latitude}
    // """);
    //   });
    // });
    // 开始监听
    // AMapLocationClient.startLocation();
  }
```

android下的 build.gradle

```dart
defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.myjd"
        minSdkVersion 16
        targetSdkVersion 28
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
        +manifestPlaceholders = [
                AMAP_KEY : "d7aba329530bff4dce38b06aed63db8d", /// 高德地图key
        ]
    }


dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    +implementation 'com.amap.api:location:latest.integration' // 高德地图依赖
    +implementation 'androidx.appcompat:appcompat:1.0.0'
}
```

android下的>src>AndroidManifest.xml

```dart
 <application>
 ...
     +<meta-data android:name="com.amap.api.v2.apikey" android:value="d7aba329530bff4dce38b06aed--高德的key" />
	+<service android:name="com.amap.api.location.APSService"></service>
 </application>
```

android下的>src>main>profile>AndroidManifest.xml

```dart
 <!--用于访问GPS定位-->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"></uses-permission>
    <!--用于获取运营商信息，用于支持提供运营商信息相关的接口-->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
    <!--用于访问wifi网络信息，wifi信息会用于进行网络定位-->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"></uses-permission>
```



# 问题

'getAppBarWidget' can't be assigned to the parameter type 'PreferredSizeWidget'.

```dart
import 'package:flutter/material.dart';

class HomeAppBar extends StatelessWidget implements PreferredSizeWidget { //加入 接口PreferredSizeWidget
  @override
  Widget build(BuildContext context) {
    return PreferredSize(
      child: AppBar(
        title: Image.asset('images/jd.png'),
        backgroundColor: Colors.red,
        actions: <Widget>[
          Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Icon(Icons.crop_free),
              Text('扫一扫', style: TextStyle(fontSize: 6.0))
            ],
          ),
          Padding(padding: EdgeInsetsDirectional.fromSTEB(0, 0, 10, 0)),
          Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Icon(Icons.sms),
              Text('消息', style: TextStyle(fontSize: 6.0))
            ],
          ),
          Padding(padding: EdgeInsetsDirectional.fromSTEB(0, 0, 20, 0))
        ],
      ),
      preferredSize: Size.fromHeight(44),
    );

    
  }
  // final String name;
  // HomeAppBar({Key key, @required this.name}) :super(key: key);
  @override
  // TODO: implement preferredSize
    Size get preferredSize => getSize();
    
      getSize() {
         return new Size(100.0, 44.0);
      }
}

```

## 去除顶部半透明

![360截图20200427015824935.png](Dart-flutter.assets/4158227332-5ea654ce483c9_articlex.png)

```kotlin
package com.example.helloflutter

import io.flutter.embedding.android.FlutterActivity
//---增加部分
import android.os.Build;
import android.os.Bundle;
//----end
class MainActivity: FlutterActivity() {
   //-----增加部分
    //设置状态栏沉浸式透明（修改flutter状态栏黑色半透明为全透明）
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState);
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
        window.statusBarColor = 0
    }
}
//---- end
}
```

## flutter_swiper 裁剪border radius

```dart
外层加入:
PhysicalModel(
            color: Colors.transparent,
            borderRadius: BorderRadius.circular(12),
            clipBehavior: Clip.antiAlias,
)
```

## BottomNavigation切换保持

```dart
class _TabsState extends State<Tabs> {
  int _currentIndex = 0;
  List _TabsPages = [Home(), Category(), My(), User()];
  var _pageController = PageController(); // 一

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("flutter ZJ"),
      ),
      body: PageView.builder(  // 二
          physics: NeverScrollableScrollPhysics(),
          //禁止页面左右滑动切换
          controller: _pageController,
          onPageChanged: (int index) {
            if (index != _currentIndex) {
              setState(() {
                _currentIndex = index;
              });
            }
          },
          //回调函数
          itemCount: _TabsPages.length,
          itemBuilder: (context, index) => _TabsPages[index]),// 三

      bottomNavigationBar: BottomNavigationBar(
          currentIndex: this._currentIndex,
          onTap: (index) {
            setState(() {
              _pageController.jumpToPage(index);
            });
          },
          type: BottomNavigationBarType.fixed,
          items: [
            BottomNavigationBarItem(
              title: Text("首页"),
              icon: Icon(Icons.home),
            ),
           	//....
          ]),
    );
  }
}

```

```dart
子页面
class _HomeState extends State<Home> 
with AutomaticKeepAliveClientMixin { // AutomaticKeepAliveClientMixin

 @override
  bool get wantKeepAlive => true; // 
}
```

```
https://blog.csdn.net/qq_32687703/article/details/95645331?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~first_rank_v2~rank_v28-6-95645331.nonecase&utm_term=flutter%20%E5%BD%93%E5%89%8D%E9%A1%B5%E9%9D%A2%E6%98%AF%E5%90%A6%E5%8F%AF%E8%A7%81&spm=1000.2123.3001.4430
```

```
https://blog.csdn.net/c6e5uli1n/article/details/104666263
```



# flutter 插件

### 国外论坛

```
https://dev.to/
```



### 工具集

```
https://dev.to/parabeac/5-tools-to-supercharge-your-flutter-development-1m0l
```



### flutter_swiper

地址:https://pub.dev/packages/flutter_swiper

```dart
import 'package:flutter/material.dart';
import 'package:flutter_swiper/flutter_swiper.dart';


class Home extends StatefulWidget {
  Home({Key key, this.title}) : super(key: key);
  final String title;

  @override
  _HomeState createState() => _HomeState();
}

class _HomeState extends State<Home> {
  var title;

  Widget _swiperview() {
    List<String> imgList = [
      "https://zhijia-pro.oss-cn-shenzhen.aliyuncs.com/h5/ad/AI%E9%A3%8E%E6%A0%BCh5.png",
      "https://zhijia-pro.oss-cn-shenzhen.aliyuncs.com/h5/ad/AI%E6%99%BA%E9%80%89%20%28h5%29.png",
      "https://zhijia-pro.oss-cn-shenzhen.aliyuncs.com/h5/ad/0%E5%85%83%E6%90%9E%E5%AE%9A%E8%AE%BE%E8%AE%A1h5.png",
    ];

    return Container(
        // 必须设置宽高 或AspectRatio 设置宽高比
      child: AspectRatio(
        aspectRatio: 540 / 216,
        child: Swiper(
          itemBuilder: (BuildContext context, int index) {
            return new Image.network(
              imgList[index],
              fit: BoxFit.cover,
            );
          },
          itemCount: imgList.length,
          // pagination: new SwiperPagination(),
          pagination: SwiperPagination(
            builder: RectSwiperPaginationBuilder(
              size: Size(20.0, 8.0),
              activeSize: Size(20.0, 8.0),
              activeColor: Colors.white,
              color: Colors.black,
            ),
            alignment: Alignment.bottomCenter,
          ),

          // control: new SwiperControl(),
          autoplay: true,
          loop: true,
          // viewportFraction: 0.8,
          // scale: 0.9,
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: [
        _swiperview(),
      ],
    );
  }
}
```

### flutter_screenutil 

```
dependencies:
  flutter:
    sdk: flutter
  # 添加依赖
  flutter_screenutil: ^2.3.0
```

```
import 'package:flutter_screenutil/flutter_screenutil.dart';
```



```
https://pub.dev/packages/flutter_screenutil
```

```
// 需要放入build 中; 要放入路由之后;
ScreenUtil.init(context, width: 750, height: 1334, allowFontScaling: false);
  
   width: ScreenUtil().setWidth(335),
   height: ScreenUtil().setHeight(221),
```

### 调试工具

```
https://flutter.dev/docs/development/tools/devtools/vscode
```

获取设备信息

```
https://segmentfault.com/a/1190000014913010?utm_source=index-hottest
device_info: 
```

定位

```
amap_location: 
```

permission_handler 

```
权限
```



# 打包

参考：https://www.jianshu.com/p/04eb531da438

```dart
项目根目录/android/app/src/main/AndroidManifest.xml

android:label="flutter_app"   //配置APP的名称，支持中文
android:icon="@mipmap/ic_launcher" //APP图标的文件名称,所以这个图标文件名可以在这个地方配置
```

生成 keystore

```


在VScode输入flutter doctor -v找到Android toolchain栏目下的Java binary at：,复制这个标题项的地址。
我Mac的地址是/Applications/Android Studio.app/Contents/jre/jdk/Contents/Home/bin/java
在VScode的终端输入查询到的java根目录地址以及keytool -genkey -v -keystore F:/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key 

即：/Applications/'Android Studio.app'/Contents/jre/jdk/Contents/Home/bin/keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
回车后，他会要求你输入密钥库口令，记住你的口令，稍后会用到。
继续操作后，还会要求你的密钥密码，同样也要记住这个密码。
之后在你的user目录下生成key.jks.这个key.jks路径可以在上面的命令行中修改。记住这个文件不能共享给任何人!
有了这个key.jks文件后，可以到项目目录下的android文件夹下，创建一个名为key.properties的文件，并打开粘贴下面的代码。

```

### build.gradle

```dart
buildscript {
    ext.kotlin_version = '1.3.50'
    repositories {
//        google()
//        jcenter()
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public' }
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.0'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}

allprojects {
    repositories {
//        google()
//        jcenter()
        maven { url 'https://maven.aliyun.com/repository/google' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public' }
    }
}

rootProject.buildDir = '../build'
subprojects {
    project.buildDir = "${rootProject.buildDir}/${project.name}"
}
subprojects {
    project.evaluationDependsOn(':app')
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

```

app下 build.gradle

```
def localProperties = new Properties()
def localPropertiesFile = rootProject.file('local.properties')
if (localPropertiesFile.exists()) {
    localPropertiesFile.withReader('UTF-8') { reader ->
        localProperties.load(reader)
    }
}

def flutterRoot = localProperties.getProperty('flutter.sdk')
if (flutterRoot == null) {
    throw new GradleException("Flutter SDK not found. Define location with flutter.sdk in the local.properties file.")
}

def flutterVersionCode = localProperties.getProperty('flutter.versionCode')
if (flutterVersionCode == null) {
    flutterVersionCode = '1'
}

def flutterVersionName = localProperties.getProperty('flutter.versionName')
if (flutterVersionName == null) {
    flutterVersionName = '1.0'
}

apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
apply from: "$flutterRoot/packages/flutter_tools/gradle/flutter.gradle"

def keystorePropertiesFile = rootProject.file("key.properties")
def keystoreProperties = new Properties()
keystoreProperties.load(new FileInputStream(keystorePropertiesFile))

android {
    compileSdkVersion 28

    sourceSets {
        main.java.srcDirs += 'src/main/kotlin'
    }

    lintOptions {
        disable 'InvalidPackage'
        checkReleaseBuilds false //新增
    }

    defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.example.myjd"
        minSdkVersion 16
        targetSdkVersion 28
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }

    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile file(keystoreProperties['storeFile'])
            storePassword keystoreProperties['storePassword']
        }
    }

    buildTypes {
        release {
            // TODO: Add your own signing config for the release build.
            // Signing with the debug keys for now, so `flutter run --release` works.
            signingConfig signingConfigs.release
            // signingConfig signingConfigs.debug
        }
    }
}

flutter {
    source '../..'
}

dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
}

```

android 目录下 创建key.properties

```
storePassword=woainia520
keyPassword=woainia520
keyAlias=key
storeFile=F:/key.jks
```

打包命令

```
flutter build apk
```

在线生成图标

```
https://appiconmaker.co/Home/

https://icon.wuruihong.com

代码插件：flutter_launcher_icons
https://pub.dev/packages/flutter_launcher_icons#-readme-tab-
```

声明

```
<!--用于进行网络定位-->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"></uses-permission>
<!--用于访问GPS定位-->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"></uses-permission>
<!--用于获取运营商信息，用于支持提供运营商信息相关的接口-->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
<!--用于访问wifi网络信息，wifi信息会用于进行网络定位-->
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"></uses-permission>
<!--用于获取wifi的获取权限，wifi信息会用来进行网络定位-->
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"></uses-permission>
<!--用于访问网络，网络定位需要上网-->
<uses-permission android:name="android.permission.INTERNET"></uses-permission>
<!--用于读取手机当前的状态-->
<uses-permission android:name="android.permission.READ_PHONE_STATE"></uses-permission>
<!--用于写入缓存数据到扩展存储卡-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"></uses-permission>
<!--用于申请调用A-GPS模块-->
<uses-permission android:name="android.permission.ACCESS_LOCATION_EXTRA_COMMANDS"></uses-permission>
<!--用于申请获取蓝牙信息进行室内定位-->
<uses-permission android:name="android.permission.BLUETOOTH"></uses-permission>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"></uses-permission>
```



# 教程

```
http://laomengit.com/
```

```
咸鱼技术分享
https://www.yuque.com/xytech/flutter/lgxv30
```

