all

```js
const all = (arr, fn = Boolean) => arr.every(fn);
EXAMPLES
all([4, 2, 3], x => x > 1); // true
all([1, 2, 3]); // true]()
```

```js
const any = (arr, fn = Boolean) => arr.some(fn);
EXAMPLES
any([0, 1, 2, 0], x => x >= 2); // true
any([0, 0, 1, 0]); // true
```

```js
const compact = arr => arr.filter(Boolean);
EXAMPLES
compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34]); // [ 1, 2, 3, 'a', 's', 34 ]
```

```js
const difference = (a, b) => {
  const s = new Set(b);
  return a.filter(x => !s.has(x));
};
EXAMPLES
difference([1, 2, 3], [1, 2, 4]); // [3]
```

