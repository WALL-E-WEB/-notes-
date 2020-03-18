https://es6.ruanyifeng.com

# 对象的拓展

### 1.简介语法

```js
const foo = 'bar';
const baz = {foo};

function f(x, y) {
  return {x, y};
}

const o = {
  method() {
    return "Hello!";
  }
};

module.exports = { getItem, setItem, clear }; //导出方法

注意，简写的对象方法不能用作构造函数，会报错。
const obj = {
  f() {
    this.foo = 'bar';
  }
};

new obj.f() //报错
```

### 2.属性名表达式

```js
let lastWord = 'last word';

const a = {
  'first word': 'hello',
  [lastWord]: 'world'
};

a['first word'] // "hello"
a[lastWord] // "world"
a['last word'] // "world"
```

### 3.方法的name属性

```js
函数的name属性，返回函数名。对象方法也是函数，因此也有name属性。
const person = {
  sayName() {
    console.log('hello!');
  },
};

person.sayName.name   // "sayName"
```

### 4.属性的可枚举性和遍历

```js
对象的每个属性都有一个描述对象（Descriptor），用来控制该属性的行为。Object.getOwnPropertyDescriptor方法可以获取该属性的描述对象。
let obj = { foo: 123 };
Object.getOwnPropertyDescriptor(obj, 'foo')
//  {
//数据属性
//    value: 123, //值
//    writable: true, //可写性
//    enumerable: true, //可枚举性
//    configurable: true //可配置性
//  }
存储属性
存储器属性是由getter和setter定义的属性
读取（get）
写入（set）
可枚举性（enumerable）
可配置性（configurable）


目前，有四个操作会忽略enumerable为false的属性。

for...in循环：只遍历对象自身的和继承的可枚举的属性。
Object.keys()：返回对象自身的所有可枚举的属性的键名。
JSON.stringify()：只串行化对象自身的可枚举的属性。
Object.assign()： 忽略enumerable为false的属性，只拷贝对象自身的可枚举的属性。
```

```js
数据属性
//    value: 123, //值
//    writable: true, //可写性
//    enumerable: true, //可枚举性
//    configurable: true //可配置性
//  }

存储属性
//存储器属性是由getter和setter定义的属性
//读取（get）
//写入（set）
//可枚举性（enumerable）
//可配置性（configurable）
```

### 5.属性遍历

```
ES6 一共有 5 种方法可以遍历对象的属性。

（1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性的键名。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

以上的 5 种方法遍历对象的键名，都遵守同样的属性遍历的次序规则。

首先遍历所有数值键，按照数值升序排列。
其次遍历所有字符串键，按照加入时间升序排列。
最后遍历所有 Symbol 键，按照加入时间升序排列。
```

### 6.super

```js
The Object.getPrototypeOf() method returns the prototype

const proto = {
  foo: 'hello'
};

const obj = {
  foo: 'world',
  find() {
    return super.foo;
  }
};

Object.setPrototypeOf(obj, proto); //指定obj原型为 proto
obj.find() // "hello"
```

### 7.对象拓展运算 符号

```js
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x // 1
y // 2
z // { a: 3, b: 

解构赋值必须是最后一个参数
解构赋值的拷贝是浅拷贝，
扩展运算符的解构赋值，不能复制继承自原型对象的属性
```

```js
上面代码中，原始函数baseFunction接受a和b作为参数，函数wrapperFunction在baseFunction的基础上进行了扩展，能够接受多余的参数，并且保留原始函数的行为。
function baseFunction({ a, b }) {
  // ...
}
function wrapperFunction({ x, y, ...restConfig }) {
  // 使用 x 和 y 参数进行操作
  // 其余参数传给原始函数
  return baseFunction(restConfig);
}
```

```js
let foo = { ...['a', 'b', 'c'] };
foo
// {0: "a", 1: "b", 2: "c"}

{...'hello'}
// {0: "h", 1: "e", 2: "l", 3: "l", 4: "o"}


```

```js
let aClone = { ...a };
// 等同于
let aClone = Object.assign({}, a);
上面的例子只是拷贝了对象实例的属性，如果想完整克隆一个对象，还拷贝对象原型的属性，可以采用下面的写法。
// 写法一
const clone1 = {
  __proto__: Object.getPrototypeOf(obj),
  ...obj
};

// 写法二
const clone2 = Object.assign(
  Object.create(Object.getPrototypeOf(obj)),
  obj
);

// 写法三
const clone3 = Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj)
)
```



```js
如果扩展运算符后面不是对象，则会自动将其转为对象。
// 等同于 {...Object(1)}
{...1} // {}
// 等同于 {...Object(true)}
{...true} // {}

// 等同于 {...Object(undefined)}
{...undefined} // {}

// 等同于 {...Object(null)}
{...null} // {}
```

### 8.链判断运算符

```
const firstName = (message
  && message.body
  && message.body.user
  && message.body.user.firstName) || 'default';
  
  const firstName = message?.body?.user?.firstName || 'default';
```

9.null判断运算符号

```js
|| //左边为false或0 也会生效
?? //只有右边为 null或 undefined
const headerText = response.settings.headerText ?? 'Hello, world!';

优先级:
使用??时 需使用()表明优先级
```

## 对象新增方法

### 1.Object.is

比较两个值是否严格相等

```js
Object.is('foo', 'foo')
// true
Object.is({}, {})
// false

不同之处
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

### 2.Object.assign

Object.assign方法用于对象的合并

```js

const target = { a: 1 };

const source1 = { b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}

浅拷贝
同名属性的替换
数组的处理
Object.assign([1, 2, 3], [4, 5])
// [4, 5, 3]

取值函数的处理
const source = {
  get foo() { return 1 }
};
const target = {};

Object.assign(target, source)
// { foo: 1 }
```

用途

**（1）为对象添加属性**

```
class Point {
  constructor(x, y) {
    Object.assign(this, {x, y});
  }
}
```

**（2）为对象添加方法**

```js
Object.assign(SomeClass.prototype, {
  someMethod(arg1, arg2) {
    ···
  },
  anotherMethod() {
    ···
  }
});

// 等同于下面的写法
SomeClass.prototype.someMethod = function (arg1, arg2) {
  ···
};
SomeClass.prototype.anotherMethod = function () {
  ···
};
```

**（3）克隆对象**

```
function clone(origin) {
  return Object.assign({}, origin);
}

function clone(origin) {
  let originProto = Object.getPrototypeOf(origin);
  return Object.assign(Object.create(originProto), origin);
}
```

**（4）合并多个对象**

```js
const merge =
  (...sources) => Object.assign({}, ...sources);
```

### Object.keys

```js
let {keys, values, entries} = Object;
let obj = { a: 1, b: 2, c: 3 };

for (let key of keys(obj)) {
  console.log(key); // 'a', 'b', 'c'
}

for (let value of values(obj)) {
  console.log(value); // 1, 2, 3
}

for (let [key, value] of entries(obj)) {
  console.log([key, value]); // ['a', 1], ['b', 2], ['c', 3]
}

Object.fromEntries([
  ['foo', 'bar'],
  ['baz', 42]
])
// { foo: "bar", baz: 42 }
该方法的一个用处是配合URLSearchParams对象，将查询字符串转为对象。
Object.fromEntries(new URLSearchParams('foo=bar&baz=qux'))
// { foo: "bar", baz: "qux" }
```

# Set Map 数据结构

## 1.Set

Set实例方法:

```js
Set 结构的实例有以下属性。

Set.prototype.constructor：构造函数，默认就是Set函数。
Set.prototype.size：返回Set实例的成员总数。
Set 实例的方法分为两大类：操作方法（用于操作数据）和遍历方法（用于遍历成员）。下面先介绍四个操作方法。

Set.prototype.add(value)：添加某个值，返回 Set 结构本身。
Set.prototype.delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
Set.prototype.has(value)：返回一个布尔值，表示该值是否为Set的成员。
Set.prototype.clear()：清除所有成员，没有返回值。
```

Set遍历操作:

```js
Set 结构的实例有四个遍历方法，可以用于遍历成员。

Set.prototype.keys()：返回键名的遍历器
Set.prototype.values()：返回键值的遍历器
Set.prototype.entries()：返回键值对的遍历器
Set.prototype.forEach()：使用回调函数遍历每个成员
需要特别指出的是，Set的遍历顺序就是插入顺序。这个特性有时非常有用，比如使用 Set 保存一个回调函数列表，调用时就能保证按照添加顺序调用。

keys方法、values方法、entries方法返回的都是遍历器对象（详见《Iterator 对象》一章）。由于 Set 结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致。


```

```js
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
  console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]

let set = new Set([1, 4, 9]);
set.forEach((value, key) => console.log(key + ' : ' + value))
// 1 : 1
// 4 : 4
// 9 : 9

let set = new Set(['red', 'green', 'blue']);
let arr = [...set];
// ['red', 'green', 'blue']
```

Set去重

```js
Array.from方法可以将 Set 结构转为数组。
function dedupe(array) {
  return Array.from(new Set(array));
}

dedupe([1, 1, 2, 3]) // [1,
```

## 2.weakSet

WeakSet 是一个构造函数，可以使用`new`命令，创建 WeakSet 数据结构。

WeakSet 可以接受一个数组或类似数组的对象作为参数

```js
const ws = new WeakSet();

const a = [[1, 2], [3, 4]];
const ws = new WeakSet(a);
// WeakSet {[1, 2], [3, 4]}
```



```js
WeakSet 结构有以下三个方法。

WeakSet.prototype.add(value)：向 WeakSet 实例添加一个新成员。
WeakSet.prototype.delete(value)：清除 WeakSet 实例的指定成员。
WeakSet.prototype.has(value)：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。


WeakSet为弱引用类型;不可遍历
```

