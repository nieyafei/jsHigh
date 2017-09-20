# 函数

> 函数可以封装任意多条语句，而且可以在任何地方，任何时候调用执行
使用关键词 `function`来声明

```
function foo(name,size){
  console.log("打印")
}
foo("lily",18);// 调用函数
```
```
function sum(num1,num2){
  return num1+num2;
}
var total = sum(2,5);// 7
```

**严格模式对函数有一定的限制**

- 不能把函数命名为 `eval` 或 `arguments`
- 不能把参数命名为 `eval` 或 `arguments`
- 不能出现两个命名参数同名的情况

#### arguments

```
function Foo(){
  console.log(arguments[0]);
  console.log(arguments[1]);
  console.log(arguments[2])
}
Foo("aaa","bbb","ccc");// aaa  bbb   ccc
```