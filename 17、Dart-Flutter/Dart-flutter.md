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

