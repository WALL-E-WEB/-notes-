https://www.cnblogs.com/MrZhujl/p/12073771.html

# 选择器插值

```less
//Less
@name: blocked;
.@{name} {
    color: black;
}

//输出css
.blocked {
    color: black;
}
```

# 字符串插值

```less
@base-url: "http://baidu.com";
background-image: url("@{base-url}/images/bg.png");
```



# less递归

```less
.wmixin(24); //声明 .wmixin为命名 而不是 class
.wmixin(@n, @i: 1) when (@i =< @n) { // if
  &.w-col-span-@{i} {
    width: @i / 24 * 100%;
  }
  .wmixin(@n, (@i + 1)); //递归
}

.generate-col(30);
.generate-col(@n, @i: 2) when (@i =< @n) {
  .p_@{i} {
    padding:@i
  }

  .p_l_@{i} {
    padding-left: @i;
  }
  .p_r_@{i} {
    padding-right: @i;
  }
  .p_b_@{i} {
    padding-bottom: @i;
  }
  .p_t_@{i} {
    padding-top: @i;
  }
  .generate-col(@n, (@i+2));
}

```

# 拼接类名

```css
.box{
  &_a{
 	height:10px 
  }
}
----

.box_a{
	height:10px 
}
```

# mixin

```less
.hairline-common() {
  position: absolute;
  box-sizing: border-box;
  content: ' ';
  pointer-events: none;
}

.hairline{
  .hairline-common();
  top: -50%;
  right: -50%;
  bottom: -50%;
  left: -50%;
}

```

