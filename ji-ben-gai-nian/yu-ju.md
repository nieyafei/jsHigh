# 语句

##  if语句

> if(condition) statement1 else statement2

## do-while语句

> 一种后测试循环语句，即只有在循环体中的代码执行之后，才会测试出口条件
在对条件表达是求值之前，循环体内的代码至少会被执行一次

```
var i = 9;
do {
  console.log(i++);
} while (i < 11);// 9   10

var i = 9;
do {
  console.log(i++);
} while (i < 9);// 9
```

## while语句

> 前测试循环语句，在循环体执行之后，就会对出口条件求值

```
var i = 9;
while (i < 11) {
  console.log(i++);
}// 9  10

var i = 9;
while (i < 9) {
  console.log(i++);
}// 不打印
```

## for语句

> 前测试循环语句，但它具有在执行循环之前初始化变量和定义变量循环后要执行的代码能力

```
for(var i=0;i<20;i<<){
  //other
}

for(;;){
  无限循环
}
```

## for-in语句

> 精准的迭代语句，用来枚举对象的属性
for(property in expression) statement

```
for (var pName in window) {
  console.log("123456")
}
```

## label语句

> 可以在代码中添加标签，以便将来使用

```
label: statement

start: function(;;){
  // other
}
```

## breack 和 continue 语句

> 用于在循环中精确地控制代码的执行
break:立即退出循环，强制继续执行循环后面的语句
continue:立即退出循环，但是退出循环之后会从循环的顶部继续执行

```
# break语句
for (var i = 1; i < 10; i++) {
  if (i % 5 == 0) {
    break;
  }
}
console.log(i);// 5
```
```
# continue语句
for (var i = 1; i < 10; i++) {
  if (i % 5 == 0) {
    continue;
  }
  console.log(i);// 1 2 3 4 6 7 8 9
}
```

```
# label语句的结合
start:
  for (var i = 1; i < 10; i++) {
    if (i % 5 == 0) {
      break start;
    }
  }
console.log(i)

start:
  for (var i = 1; i < 10; i++) {
    if (i % 5 == 0) {
      continue start;
    }
    console.log(i)
  }
```

## with语句

> 将代码的作用域设置到一个特定的对象中
> 严格模式不支持此语法

## switch语句

> 语句在比较值时使用的是全等操作符，因此不会发生类型转换

```
function sw(i) {
  switch (i) {
    case 1:
      console.log(1)
      break;
    case 2:
      console.log(2);
      break;
    case 3:
      //合并两种情况
    case 4:
      console.log("公用");
      break;
    default:
      console.log("默认")
  }
}

sw(1);// 1
sw(2);// 2
sw(3);// 公用
sw(3);// 公用
sw();// 默认
```