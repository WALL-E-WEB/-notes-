when

```less
.wmixin(24); //声明 .wmixin为命名 而不是 class
.wmixin(@n, @i: 1) when (@i =< @n) { // if
  &.w-col-span-@{i} {
    width: @i / 24 * 100%;
  }
  .wmixin(@n, (@i + 1)); //递归
}
```

