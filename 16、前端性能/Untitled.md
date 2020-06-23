优化方式

懒加载



repload

```js
link标签中  更早加载此文件

<link rel="preload" href="../vue.js" as="script"/>
```

prefetch

```js
闲时加载 非首页需要资源 或
Predictive prefetch

<link rel="prefetch" href="../vue.js" as="script"/>
```

cache

```

```

数据压缩优化

```
Broti
 开源数据压缩程序库
 专为HTTP传输优化
```

```
HTTP2.0 终究办法
	头文件压缩
	HPACK
	
Cookie-less domain
```

```js
Minification
 牺牲代码可读性,减少文件体积
```

