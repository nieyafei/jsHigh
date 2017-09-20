# 语法、变量、数据类型读记

## 区分大小写

> ECMAScript的一切，包括变量、函数名、操作符都要区分大小写

```
var test 和 var Test 这是两个不同的变量
``` 

## 标识符

> 标识符是指变量、函数名、属性的名字，或者函数的参数。

标识符的规则：

> 1、第一个字符必须是一个字母、下划线（_）或一个美元符号（$）
2、其他的字符可以是字母、下划线、数字、美元符号

ps:按照惯例，标识符采用驼峰大小格式

## 注释

- #### 单行注释
```
//这是单行注释
```

- #### 多行注释

```
/*
* 我是多行注释
* 我是注释
*/
```

## 语句

> 解析中以一个分号结尾，如果省略分号，则由解析器确定语句的结尾，建议不要忽略分号

## 关键字和保留字

> 具有一定的用途的关键字，关键字可用于表示控制语句的开始或结束，或执行特定的操作

- #### 关键字有哪些

```
break    do     instanceof      typeof     in     try
case    else     new    var    catch
finally     return    void    continue     for
switch     while     debugger   function     this
with     default      if       throw     delete    
```

- #### 保留字有哪些

```
abstract	enum	int	short
boolean	export	interface	static
byte	extends	long	super
char	final	native	synchronized
class	float	package	throws
const	goto	private	transient
debugger	implements	protected	volatile
double	import	public

第5 版把在非严格模式下运行时的保留字缩减为下列这些：
class	enum	extends	super
const	export	import

在严格模式下，第5 版还对以下保留字施加了限制：
implements	package	public	interface
private	static	let	protected
yield
```

## 变量

> 变量是松散型的，可以用来保存任何类型的数据，每个变量仅仅是一个用于保存值得占位符

```
var message;// 这是一个变量，未经过初始化，变量的值为`undefined`
var i = 2;
```

##  数据类型

- #### 基本数据类型

> Undefined、String、Number、Null、Boolean、Object

- #### typeof 操作符

> 一种用来验证给定变量的数据类型的手段

`undefined`:如果这个值未定义
`boolena`:如果这个值是布尔值
`string`:如果这个值是字符串
`number`:如果这个值是数值
`object`：如果这个值是函数
`function`:如果这个值是函数

```
var message = "something";
console.log(typeof message);
```