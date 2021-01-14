vscode 配置自动格式化

需要的vscode插件：

- vetur+eslint+prettier

setting配置：

```json
"editor.tabSize": 2,
    "files.associations": {
        "*.vue": "vue"
    },
    "eslint.autoFixOnSave": true,//  启用保存时自动修复,默认只支持.js文件
    "eslint.options": {
        "extensions": [
            ".js",
            ".vue"
        ]
    },
    "eslint.validate": [
        "javascript",  //  用eslint的规则检测js文件
        {
            "language": "vue", // 检测vue文件
            "autoFix": true //  为vue文件开启保存自动修复的功能
        },
        "html",
        "vue"
    ],
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
        "**/dist": true
    },
    "emmet.syntaxProfiles": {
        "javascript": "jsx",
        "vue": "html",
        "vue-html": "html"
    },
    "git.confirmSync": false,
    "window.zoomLevel": -1,
    "editor.renderWhitespace": "boundary",
    "editor.cursorBlinking": "smooth",
    "editor.minimap.enabled": true,
    "editor.minimap.renderCharacters": false,
    "editor.fontFamily": "'Droid Sans Mono', 'Courier New', monospace, 'Droid Sans Fallback'",
    "window.title": "${dirty}${activeEditorMedium}${separator}${rootName}",
    "editor.codeLens": true,
    "editor.snippetSuggestions": "top",
    "eslint.migration.2_x": "off",
    "vetur.format.defaultFormatterOptions": { // 解决 vetur 冲突
        "prettier": {
          // Prettier option here
          "semi": false,
          "singleQuote": true,
          "trailingComma": "none"
        }
    },
```

简单配置:

```
{
  "explorer.confirmDelete": false,
  "editor.formatOnType": true,
  "editor.formatOnSave": true,
  "eslint.autoFixOnSave": true, //保存自动修复eslint错误
  "eslint.validate": [
      "javascript",
      "javascriptreact",
      "html",
      "vue",
      {
          "language": "vue",
          "autoFix": true
      }
  ],
  "eslint.options": { //指定eslint配置文件位置
      "configFile": ".eslintrc.js" //指定项目根目录中的eslint配置文件
  },
  "files.autoSave": "off",
}
```



```js

rules: {
    "规则名": [规则值, 规则配置]


"off"或者0    //关闭规则关闭
"warn"或者1    //在打开的规则作为警告（不影响退出代码）
"error"或者2

列:
//空行最多不能超过100行
    "no-multiple-empty-lines": [0, {"max": 100}],

```

常见配置

```json
  // 定义对象的set存取器属性时，强制定义get
 26         'accessor-pairs': 0,
 27         // 在数组括号内强制实现一致的间距。
 28         'array-bracket-newline': 0,
 29         // 指定数组的元素之间要以空格隔开(, 后面)， never参数：[ 之前和 ] 之后不能带空格，always参数：[ 之前和 ] 之后必须带空格
 30         'array-bracket-spacing': [2, 'never'],
 31         // 强制数组方法的回调函数中有 return 语句
 32         'array-callback-return': 1,
 33         // 强制数组元素间出现换行
 34         'array-element-newline': 0,
 35         // 要求箭头函数体使用大括号
 36         'arrow-body-style': 2,
 37         // 要求箭头函数的参数使用圆括号
 38         'arrow-parens': 2,
 39         // 要求箭头函数空格
 40         'arrow-spacing': [2, {'before': true,'after': true}],
 41         // 强制把变量的使用限制在其定义的作用域范围内
 42         'block-scoped-var': 2,
 43         // 禁止或强制在单行代码块中使用空格(禁用)
 44         'block-spacing': 0,
 45         //强制使用一致的缩进 第二个参数为 'tab' 时，会使用tab，
 46         // if while function 后面的{必须与if在同一行，java风格。
 47         'brace-style': [2, '1tbs', { 'allowSingleLine': true }],
 48         // require return statements after
 49         'callback-return': 0,
 50         // 双峰驼命名格式
 51         'camelcase': 2,
 52         // 注释 大写字母开头，不推荐 注释的代码会报错
 53         'capitalized-comments': 0,
 54         // 如果一个类方法没有使用this，它有时可以变成一个静态函数。如果将该方法转换为静态函数，那么调用该特定方法的类的实例也必须转换为静态调用
 55         'class-methods-use-this': 2,
 56         // 数组和对象键值对最后一个逗号， never参数：不能带末尾的逗号, always参数：必须带末尾的逗号，
 57         // always-multiline：多行模式必须带逗号，单行模式不能带逗号
 58         'comma-dangle': [2, 'never'],
 59         // 控制逗号前后的空格
 60         'comma-spacing': [2, {'before': false,'after': true}],
 61         // 控制逗号在行尾出现还是在行首出现 (默认行尾)
 62         // http: //eslint.org/docs/rules/comma-style
 63         'comma-style': [2,'last'],
 64         // 限制圈复杂度，也就是类似if else能连续接多少个
 65         'complexity': 0,
 66         //'SwitchCase' (默认：0) 强制 switch 语句中的 case 子句的缩进水平
 67         // 以方括号取对象属性时，[ 后面和 ] 前面是否需要空格, 可选参数 never, always
 68         'computed-property-spacing': [2,'never'],
 69         // 要求 return 语句要么总是指定返回的值，要么不指定
 70         'consistent-return': 2,
 71         // 用于指统一在回调函数中指向this的变量名，箭头函数中的this已经可以指向外层调用者，应该没卵用了
 72         // e.g [0,'that'] 指定只能 var that = this. that不能指向其他任何值，this也不能赋值给that以外的其他值
 73         'consistent-this': [2, '_this'],
 74         // 强制在子类构造函数中用super()调用父类构造函数，TypeScrip的编译器也会提示
 75         'constructor-super': 0,
 76         // 强制所有控制语句使用一致的括号风格
 77         'curly': [2,'all'],
 78         // switch 语句强制 default 分支，也可添加 // no default 注释取消此次警告
 79         'default-case': 2,
 80         // 强制object.key 中 . 的位置，参数:
 81         // property，'.'号应与属性在同一行
 82         // object, '.' 号应与对象名在同一行
 83         'dot-location': [2,'property'],
 84         // 强制使用.号取属性
 85         // 参数： allowKeywords：true 使用保留字做属性名时，只能使用.方式取属性
 86         // false 使用保留字做属性名时, 只能使用[]方式取属性 e.g [2, {'allowKeywords': false}]
 87         // allowPattern: 当属性名匹配提供的正则表达式时，允许使用[]方式取值,否则只能用.号取值 e.g [2, {'allowPattern': '^[a-z]+(_[a-z]+)+$'}]
 88         'dot-notation': 0,
 89         // 文件末尾强制换行
 90         'eol-last': 0,
 91         // 使用 === 替代 == allow-null允许null和undefined==
 92         'eqeqeq': [2, 'allow-null'],
 93         //强制 “for” 循环中更新子句的计数器朝着正确的方向移动
 94         'for-direction': "error",
 95         // 要求或禁止函数标识符与其调用之间的间隔
 96         'func-call-spacing': [0, 'always'],
 97         // 要求函数名称与它们所分配的变量或属性的名称相匹配
 98         'func-name-matching': 2,
 99         // 强制使用命名的 function 表达式
100         'func-names': 0,
101         // 强制一致地使用函数声明或函数表达式，方法定义风格，参数：
102         // declaration: 强制使用方法声明的方式，function f(){} e.g [2, 'declaration']
103         // expression：强制使用方法表达式的方式，var f = function() {} e.g [2, 'expression']
104         // allowArrowFunctions: declaration风格中允许箭头函数。 e.g [2, 'declaration', { 'allowArrowFunctions': true }]
105         'func-style': 0,
106         // 在函数括号内强制执行一致的换行符
107         'function-paren-newline': 0,
108         // 强制 generator 函数中 * 号周围使用一致的空格
109         'generator-star-spacing': [2, {'before': true,'after': true}],
110         // 强制在 getter 属性中出现一个 return 语句。每个 getter 都期望有返回值。
111         'getter-return': 2,
112         // 要求 require() 出现在顶层模块作用域中
113         'global-require': 1,
114         // 要求 for-in 循环中有一个 if 语句
115         'guard-for-in': 1,
116         // 要求回调函数中有容错处理
117         'handle-callback-err': [2,'^(err|error)$'],
118         // 禁止使用指定的标识符
119         'id-blacklist': 0,
120         // 强制标识符的最新和最大长度
121         'id-length': 0,
122         // 要求标识符匹配一个指定的正则表达式
123         'id-match': 0,
124         // 强制执行箭头函数体的位置,一个箭头函数体可以包含一个隐式返回，而不是一个块体。对隐式返回的表达式执行一致的位置可能很有用。
125         'implicit-arrow-linebreak': 0,
126         // 强制执行一致的缩进
127         'indent': [2, 4],
128         // 要求或禁止 var 声明中的初始化(初值)
129         'init-declarations': 2,
130         // 强制在 JSX 属性中一致地使用双引号或单引号
131         'jsx-quotes': 2,
132         // 强制在对象字面量的属性中键和值之间使用一致的间距
133         // 'key-spacing': [2, {'beforeColon': false,'afterColon': true}],
134         // 强制在关键字前后使用一致的空格 (前后腰需要)
135         // 'keyword-spacing': [2, {'beforeColon': true, 'afterColon': true}],
136         // 行注释可以位于代码上方或旁边。该规则有助于团队保持一致的风格。
137         'line-comment-position': 0,
138         // 强制使用一致的换行风格
139         'linebreak-style': 0,
140         // 要求在注释周围有空行 ( 要求在块级注释之前有一空行)
141         'lines-around-comment': 0,
142         // 这条规则要求或禁止围绕指令序言的空白换行符。此规则不强制执行有关各个指令之间空白换行符的任何约定。另外，它不需要在指令序言前留出空行，除非它们之前有评论。如果这是您想强制执行的样式，请使用填充块规则。
143         'lines-around-directive': 0,
144         // 要求或禁止class成员之间的空行
145         'lines-between-class-members': 2,
146         // 强制执行嵌套块的最大深度，以降低代码复杂度。"max"（默认为4)
147         'max-depth': [2,6],
148         // 强制一行的最大长度
149         'max-len': [1, 200, { 'ignoreTemplateLiterals': true }],
150         // 强制最大行数
151         'max-lines': 0,
152         // 强制回调函数最大嵌套深度 5层
153         'max-nested-callbacks': [2, 5],
154         // 强制 function 定义中最多允许的参数数量
155         'max-params': [2, 4],
156         // 强制 function 块最多允许的的语句数量
157         'max-statements': [2, 200],
158         // 强制每一行中所允许的最大语句数量
159         'max-statements-per-line': 2,
160         // 强化多行评论的特定风格。
161         'multiline-comment-style': 0,
162         // 强制或禁止三元表达式的操作数之间的换行符
163         'multiline-ternary': 0,
164         // 要求构造函数首字母大写 （要求调用 new 操作符时有首字母大小的函数，允许调用首字母大写的函数时没有 new 操作符。）
165         'new-cap': 0,
166         // 要求调用无参构造函数时有圆括号
167         'new-parens': 0,
168         // 要求或禁止 var 声明语句后有一行空行
169         'newline-after-var': 0,
170         // 要求 return 语句之前有一空行
171         'newline-before-return': 0,
172         // 要求方法链中每个调用都有一个换行符
173         'newline-per-chained-call': 0,
174         // 禁用 alert、confirm 和 prompt
175         'no-alert': 2,
176         // 禁止使用 Array 构造函数
177         'no-array-constructor': 0,
178         // 不允许await在循环体内使用。
179         'no-await-in-loop': 0,
180         // 禁用按位运算符
181         'no-bitwise': 1,
182         // 不允许调用和构造Buffer()构造函数。
183         'no-buffer-constructor': 0,
184         // 禁用 arguments.caller 或 arguments.callee
185         'no-caller': 2,
186         // 不允许在 case 子句中使用词法声明
187         'no-case-declarations': 0,
188         // 不允许 catch 子句的参数与外层作用域中的变量同名
189         'no-catch-shadow': 2,
190         // 禁止修改类声明的变量
191         'no-class-assign': 2,
192         // 检测对象文字中的尾随逗号。因此，只要遇到对象字面上的尾随逗号，就会发出警告。
193         // 'no-comma-dangle': 2,
194         // 针对试图与-0进行比较的代码发出警告，因为这不会按预期工作。也就是说，像x === -0这样的代码将通过+0和-0。作者可能打算 Object.is（x，-0）。
195         'no-compare-neg-zero': 2,
196         // 禁止条件表达式中出现赋值操作符
197         'no-cond-assign': 2,
198         // 不允许箭头功能，在那里他们可以混淆的比较
199         'no-confusing-arrow': 0,
200         // 禁用 console
201         'no-console': 0,
202         // 禁止修改 const 声明的变量
203         'no-const-assign': 2,
204         // 禁止在条件中使用常量表达式
205         // if (false) {
206         // doSomethingUnfinished();
207         // } //cuowu
208         'no-constant-condition': 2,
209         // 禁用 continue 语句
210         'no-continue': 0,
211         // 禁止在正则表达式中使用控制字符 ：new RegExp('\x1f')
212         'no-control-regex': 0,
213         // 禁用 debugger
214         'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
215         // 禁止删除变量
216         'no-delete-var': 2,
217         // 禁止除法操作符显式的出现在正则表达式开始的位置
218         'no-div-regex': 1,
219         // 禁止 function 定义中出现重名参数
220         'no-dupe-args': 2,
221         // 禁止类成员中出现重复的名称
222         'no-dupe-class-members': 2,
223         // 禁止对象字面量中出现重复的 key
224         'no-dupe-keys': 2,
225         // 禁止重复的 case 标签
226         'no-duplicate-case': 2,
227         // 不允许复制模块的进口
228         'no-duplicate-imports': 2,
229         // 禁止 if 语句中有 return 之后有 else
230         'no-else-return': 0,
231         // 禁止空语句块
232         'no-empty': 2,
233         // 禁止在正则表达式中使用空字符集 (/^abc[]/)
234         'no-empty-character-class': 2,
235         // 禁止出现空函数.如果一个函数包含了一条注释，它将不会被认为有问题。
236         'no-empty-function': 0,
237         // 禁止使用空解构模式no-empty-pattern
238         'no-empty-pattern': 2,
239         // 禁止在没有类型检查操作符的情况下与 null 进行比较
240         'no-eq-null': 2,
241         // 禁用 eval()
242         'no-eval': 2,
243         // 禁止对 catch 子句的参数重新赋值
244         'no-ex-assign': 2,
245         // 禁止扩展原生类型
246         'no-extend-native': 0,
247         // 禁止不必要的 .bind() 调用
248         'no-extra-bind': 0,
249         // 禁止不必要的布尔转换
250         'no-extra-boolean-cast': 1,
251         // 禁用不必要的标签
252         'no-extra-label: ': 0,
253         // 禁止不必要的括号 //(a * b) + c;//报错
254         'no-extra-parens': 0,
255         // 禁止不必要的分号
256         'no-extra-semi': 0,
257         // 禁止 case 语句落空
258         'no-fallthrough': 0,
259         // 禁止数字字面量中使用前导和末尾小数点
260         'no-floating-decimal': 2,
261         // 禁止对 function 声明重新赋值
262         'no-func-assign': 2,
263         // 此规则不允许修改只读全局变量。
264         'no-global-assign': 2,
265         // 禁止使用短符号进行类型转换(!!fOO)
266         'no-implicit-coercion': 2,
267         // 禁止在全局范围内使用 var 和命名的 function 声明
268         'no-implicit-globals': 0,
269         // 禁止使用类似 eval() 的方法
270         'no-implied-eval': 2,
271         // 禁止在代码行后使用内联注释
272         'no-inline-comments': 0,
273         // 禁止在嵌套的块中出现 function 或 var 声明
274         'no-inner-declarations': [2,'both'],
275         // 禁止 RegExp 构造函数中无效的正则表达式字符串
276         'no-invalid-regexp': 2,
277         // 禁止 this 关键字出现在类和类对象之外
278         'no-invalid-this': 0,
279         // 禁止在字符串和注释之外不规则的空白
280         'no-irregular-whitespace': 2,
281         // 禁用 __iterator__ 属性
282         'no-iterator': 2,
283         // 不允许标签与变量同名
284         'no-label-var': 2,
285         // 禁用标签语句
286         'no-labels': 2,
287         // 禁用不必要的嵌套块
288         'no-lone-blocks': 2,
289         // 禁止 if 作为唯一的语句出现在 else 语句中
290         'no-lonely-if': 2,
291         // 禁止在循环中出现 function 声明和表达式
292         'no-loop-func': 1,
293         // 禁用魔术数字(3.14什么的用常量代替)
294         'no-magic-numbers': 0,
295         // 禁止混合使用不同的操作符
296         'no-mixed-operators': 2,
297         // 禁止混合常规 var 声明和 require 调用
298         'no-mixed-requires': 1,
299         // 不允许空格和 tab 混合缩进
300         'no-mixed-spaces-and-tabs': 2,
301         // 不允许在单个语句中使用多个分配。a = b = c = d;
302         'no-multi-assign': 2,
303         // 禁止使用多个空格
304         'no-multi-spaces': 2,
305         // 禁止使用多行字符串，在 JavaScript 中，可以在新行之前使用斜线创建多行字符串
306         'no-multi-str': 0,
307         // 不允许多个空行
308         'no-multiple-empty-lines': [2, {'max': 2}],
309         // 不允许否定的表达式
310         'no-negated-condition': 0,
311         // 禁止在 in 表达式中出现否定的左操作数
312         'no-negated-in-lhs': 0,
313         // 不允许使用嵌套的三元表达式 var foo = bar ? baz : qux === quxx ? bing : bam;
314         'no-nested-ternary': 1,
315         // 禁止在非赋值或条件语句中使用 new 操作符
316         'no-new': 1,
317         // 禁止对 Function 对象使用 new 操作符
318         'no-new-func': 1,
319         // 禁止使用 Object 的构造函数
320         'no-new-object': 0,
321         // 禁止调用 require 时使用 new 操作符
322         'no-new-require': 2,
323         // 禁止 Symbol 的构造函数
324         'no-new-symbol': 1,
325         // 禁止对 String，Number 和 Boolean 使用 new 操作符
326         'no-new-wrappers': 0,
327         // 禁止把全局对象 (Math 和 JSON) 作为函数调用 错误：var math = Math();
328         'no-obj-calls': 2,
329         // 禁用八进制字面量
330         'no-octal': 2,
331         // 禁止在字符串中使用八进制转义序列
332         'no-octal-escape': 2,
333         // 不允许对 function 的参数进行重新赋值
334         'no-param-reassign': 2,
335         // 禁止对 __dirname 和 __filename进行字符串连接
336         'no-path-concat': 0,
337         // 禁止使用一元操作符 ++ 和 --
338         'no-plusplus': 0,
339         // 禁用 process.env
340         'no-process-env': 1,
341         // 禁用 process.exit()
342         'no-process-exit': 1,
343         // 禁用 __proto__ 属性
344         'no-proto': 0,
345         // 禁止直接使用 Object.prototypes 的内置属性
346         'no-prototype-builtins': 0,
347         // 禁止使用 var 多次声明同一变量
348         'no-redeclare': 2,
349         // 禁止正则表达式字面量中出现多个空格
350         'no-regex-spaces': 1,
351         // 禁用特定的全局变量
352         'no-restricted-globals': 0,
353         // 允许指定模块加载时的进口
354         'no-restricted-imports': 0,
355         // 允许你指定你不想在你的应用程序中使用的模块。
356         'no-restricted-modules': 0,
357         // 对象上的某些属性可能在代码库中被禁止。这对于取消API或限制模块方法的使用很有用。例如，您可能希望使用不允许describe.only使用摩卡或者告诉人们使用时Object.assign代替_.extend。
358         'no-restricted-properties': 0,
359         // 禁止使用特定的语法
360         'no-restricted-syntax': 0,
361         // 禁用指定的通过 require 加载的模块
362         'no-return-assign': 0,
363         // 禁止 return await ；这个规则旨在防止由于缺乏对async function语义的理解而导致的可能的常见性能危害。
364         'no-return-await': 2,
365         // 禁止使用 javascript: url
366         'no-script-url': 0,
367         // 禁止自我赋值
368         'no-self-assign': 2,
369         // 禁止自身比较
370         'no-self-compare': 2,
371         // 禁用逗号操作符
372         'no-sequences': 2,
373         // 禁止 var 声明 与外层作用域的变量同名
374         'no-shadow': 0,
375         // 禁止覆盖受限制的标识符
376         'no-shadow-restricted-names': 2,
377         // 禁用稀疏数组
378         'no-sparse-arrays': 2,
379         // 禁用同步方法
380         'no-sync': 0,
381         // 不允许使用制表符
382         'no-tabs': 2,
383         // 警告常规字符串包含看起来像模板字面占位符的内容。"Hello ${name}!";
384         'no-template-curly-in-string': 0,
385         // 不允许使用三元操作符
386         'no-ternary': 0,
387         // 禁止在构造函数中，在调用 super() 之前使用 this 或 super
388         'no-this-before-super': 2,
389         // 禁止抛出非异常字面量
390         'no-throw-literal': 2,
391         // 禁用行尾空格
392         'no-trailing-spaces': 2,
393         // 禁用未声明的变量，除非它们在 /*global */ 注释中被提到
394         'no-undef': 2,
395         // 禁止将变量初始化为 undefined
396         'no-undef-init': 2,
397         // 禁止将 undefined 作为标识符
398         'no-undefined': 0,
399         // 禁止标识符中有悬空下划线_bar
400         'no-underscore-dangle': 0,
401         // 禁止出现令人困惑的多行表达式
402         'no-unexpected-multiline': 0,
403         // 禁用一成不变的循环条件
404         'no-unmodified-loop-condition': 2,
405         // 禁止可以在有更简单的可替代的表达式时使用三元操作符
406         'no-unneeded-ternary': 0,
407         // 禁止在return、throw、continue 和 break语句之后出现不可达代码
408         /*
409         function foo() {
410         return true;
411         console.log('done');
412         }//错误
413         */
414         'no-unreachable': 2,
415         // 禁止在 finally 语句块中出现控制流语句
416         'no-unsafe-finally': 0,
417         // 不允许否定关系运算符的左操作数 disallow negating the left operand of relational operators
418         'no-unsafe-negation': 2,
419         // 禁止出现未使用过的表达式
420         'no-unused-expressions': 2,
421         // 禁用未使用过的标签
422         'no-unused-labels': 2,
423         // 禁止出现未使用过的变量
424         'no-unused-vars': 2,
425         // 不允许在变量定义之前使用它们
426         'no-use-before-define': 2,
427         // 禁止不必要的 .call() 和 .apply()
428         'no-useless-call': 2,
429         // 禁止不必要的计算性能键对象的文字
430         'no-useless-computed-key': 2,
431         // 禁止不必要的字符串字面量或模板字面量的连接
432         'no-useless-concat': 2,
433         // ES2015 会提供默认的类构造函数。因此，没有必要提供一个空构造函数或一个简单地委托给它的父类的构造函数，
434         'no-useless-constructor': 2,
435         // 禁用不必要的转义字符
436         'no-useless-escape': 0,
437         // 不允许将导入、导出和解构分配重命名为相同的名称。
438         'no-useless-rename': 2,
439         // 多余的return语句。
440         'no-useless-return': 2,
441         // 要求使用 let 或 const 而不是 var
442         'no-var': 2,
443         // 禁用 void 操作符
444         'no-void': 2,
445         // 禁止在注释中使用特定的警告术语
446         'no-warning-comments': 0,
447         // 禁止属性前有空白
448         'no-whitespace-before-property': 2,
449         // 禁用 with 语句
450         'no-with': 1,
451         // 当写if，else，while，do-while，和for语句，身体部分可以是单个语句而不是块。为这些单一语句强制执行一个一致的位置会很有用。
452         'nonblock-statement-body-position': 1,
453         // 强制花括号内换行符的一致性
454         'object-curly-newline': 0,
455         // 强制在花括号中使用一致的空格
456         'object-curly-spacing': 2,
457         // 强制将对象的属性放在不同的行上
458         'object-property-newline': 0,
459         // 要求或禁止对象字面量中方法和属性使用简写语法
460         'object-shorthand': 2,
461         // 强制函数中的变量要么一起声明要么分开声明
462         'one-var': 0,
463         // 要求或禁止在 var 声明周围换行
464         'one-var-declaration-per-line': 0,
465         // 要求或禁止在可能的情况下要求使用简化的赋值操作符
466         'operator-assignment': 0,
467         // 强制操作符使用一致的换行符
468         'operator-linebreak': 0,
469         // 要求或禁止块内填充
470         'padded-blocks': 0,
471         // 所有return语句之前需要空行，如换行前换行符规则。
472         'padding-line-between-statements': 0,
473         // 要求使用箭头函数作为回调
474         'prefer-arrow-callback': 0,
475         // 要求使用 const 声明那些声明后不再被修改的变量
476         'prefer-const': 2,
477         // 采用两组配置对象。第一个对象参数决定了规则适用的解构类型
478         'prefer-destructuring': 0,
479         // 禁止调用parseInt()或Number.parseInt()使用两个参数调用：一个字符串; 和2（二进制），8（八进制）或16（十六进制）的基数选项。
480         'prefer-numeric-literals': 2,
481         // 确保承诺只被Error对象拒绝。
482         'prefer-promise-reject-errors': 0,
483         // 要求在合适的地方使用 Reflect 方法
484         'prefer-reflect': 0,
485         // Suggest using the rest parameters instead of arguments
486         'prefer-rest-params': 2,
487         // 要求使用扩展运算符而非 .apply()
488         'prefer-spread': 2,
489         // 要求使用模板字面量而非字符串连接
490         'prefer-template': 1,
491         // 要求对象字面量属性名称用引号括起来
492         'quote-props': 0,
493         // 强制使用一致的反勾号、双引号或单引号
494         'quotes': 0,
495         // 强制在parseInt()使用基数参数
496         'radix': 0,
497         // 异步函数必须具有await表达式
498         'require-await': 2,
499         // 要求使用 JSDoc 注释
500         'require-jsdoc': 0,
501         // 要求generator 函数内有 yield
502         'require-yield': 2,
503         // enforce spacing between rest and spread operators and their expressions
504         'rest-spread-spacing': 0,
505         // 要求或禁止使用分号而不是 ASI（这个才是控制行尾部分号的，）
506         'semi': 0,
507         // 强制分号之前和之后使用一致的空格
508         'semi-spacing': 0,
509         // 强制分号位于配置的位置。
510         'semi-style': 0,
511         // 强制模块内的 import 排序
512         'sort-imports': 0,
513         // 所有属性定义并验证所有变量是按字母顺序排序的。
514         'sort-keys': 0,
515         // 要求同一个声明块中的变量按顺序排列
516         'sort-vars': 0,
517         // 强制在块之前使用一致的空格
518         'space-before-blocks': [2,'always'],
519         // 强制在 function的左括号之前使用一致的空格
520         'space-before-function-paren': [2,'always'],
521         // 强制在圆括号内使用一致的空格
522         'space-in-parens': [2,'never'],
523         // 要求操作符周围有空格
524         'space-infix-ops': 2,
525         // 强制在一元操作符前后使用一致的空格
526         'space-unary-ops': 2,
527         // 强制在注释中 // 或 /* 使用一致的空格
528         'spaced-comment': 0,
529         // 要求或禁止使用严格模式指令
530         'strict': 0,
531         // switch语句内的空格
532         'switch-colon-spacing': 2,
533         // var foo = Symbol("some description"); 一定要有描述
534         'symbol-description': 2,
535         // 要求或禁止模板字符串中的嵌入表达式周围空格的使用
536         'template-curly-spacing': [2, 'never'],
537         // 模板标签函数与其模板文字之间是否有空格
538         'template-tag-spacing': 0,
539         // 要求或禁止 Unicode BOM
540         'unicode-bom': 0,
541         // 不允许比较'NaN'。判断数字是否是NaN，得用isNaN
542         'use-isnan': 2,
543         // 强制使用有效的 JSDoc 注释
544         'valid-jsdoc': 0,
545         // 强制 typeof 表达式与有效的字符串进行比较
546         // typeof foo === 'undefimed' 错误
547         'valid-typeof': 2,
548         // 要求所有的 var 声明出现在它们所在的作用域顶部
549         'vars-on-top': 2,
550         // 要求 IIFE 使用括号括起来
551         'wrap-iife': 0,
552         // 要求正则表达式被括号括起来
553         'wrap-regex': 0,
554         // 强制在 yield* 表达式中 * 周围使用空格
555         'yield-star-spacing': 2,
556         // 要求或禁止 “Yoda” 条件
557         'yoda': 0,
```

# vue 配置

```
https://eslint.vuejs.org/rules/
eslint-plugin-vue

https://www.cnblogs.com/dreamsqin/p/10906951.html
```

