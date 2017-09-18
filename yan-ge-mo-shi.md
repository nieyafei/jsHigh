# 严格模式(use strict)

> "use strict"; // 即在严格的条件下运行。

`严格模式`是在`ECMAScript5`新增的，**严格模式下你不能使用未声明的变量**，体现了Javascript更合理、更安全、更严谨的发展方向。

`严格模式`是为js定义了一种不同的解析和执行模型，在此模式下，对于`ECMAScript3`种的一些不确定行为将会处理，对于不安全的操作也会抛出错误的。一般都是在js的顶部添加此模式代码。

> 非严格的模式，也会被称为“马虎模式/稀松模式/懒散模式”

## 严格模式的好处

> 1、消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
> 2、消除代码运行的一些不安全之处，保证代码运行的安全;
> 3、提高编译器效率，增加运行速度；
> 4、为未来新版本的Javascript做好铺垫。

## 严格模式的调用开启

- ##### 针对整个脚本文件的调用

> 在整个脚本文件最开始的地方引入，整个脚本都将以"严格模式"运行

```
<script>
　　"use strict";
　　console.log("这是严格模式。");
</script>
<script>
　　console.log("这是正常模式。");
</script>
// 第一个是严格模式，第二个则是正常模式
```

- ##### 单个函数的严格模式

> 声明在函数体的首行
```
function foo() {
  "use strict";
  console.log("函数严格模式执行");
}
```

- ##### 脚本文件的变通写法

> 因为多个文件的合并不利于`严格模式`的声明，因此对第二种方法进行改造,将整个脚本文件放在一个立即执行的匿名函数之中。

```
(function (){
　　"use strict";
　　// do someing
})();
```

## 严格模式和正常模式的区别

- ##### 1、严格模式下你不能使用未声明的变量，必须先声明再使用

```
"use strict";
x = 5;// ReferenceError: x is not defined

或
"use strict";
x = {a: 1};// ReferenceError: x is not defined

正常模式中，如果一个变量没有声明就赋值，默认是全局变量
```
- #### 2、不能删除变量或对象

```
"use strict";
var i = 1;
delete i;// 删除变量
// SyntaxError: Delete of an unqualified identifier in strict mode.
```
> 只有configurable设置为true的对象属性，才能被删除。
`configurable`：能否使用delete、能否需改属性特性、或能否修改访问器属性、，false为不可重新定义，默认值为true

```
"use strict";
var i = 1;
var j = Object.create(null, {
  "i": {
    value: 1,
    configurable: true
  }
})

console.log(delete j.i);// true
```

- ##### 3、禁止使用with语句

> Javascript语言的一个特点，就是允许"`动态绑定`"，即某些属性和方法到底属于哪一个对象，不是在编译时确定的，而是在运行时（runtime）确定的。
`严格模式`对动态绑定做了一些限制。某些情况下，只允许`静态绑定`。也就是说，属性和方法到底归属哪个对象，在编译阶段就确定。这样做有利于编译效率的提高，也使得代码更容易阅读，更少出现意外。

```
"use strict";
var i = 1;
with(0) { i = 2;}
SyntaxError: Strict mode code may not include a with statement
```

> with语句：由于大量使用with语句会导致性能下降，也会给调试代码造成困难，因此不建议使用with语句。
with语句所引起的问题是块内的任何名称可以映射(map)到with传进来的对象的属性, 也可以映射到包围这个块的作用域内的变量(甚至是全局变量), 这一切都是在运行时决定的: 在代码运行之前是无法得知的. 严格模式下, 使用 with 会引起语法错误, 所以就不会存在 with 块内的变量在运行是才决定引用到哪里的情况了

- ##### 创设eval作用域

> 正常模式下，Javascript语言有两种变量作用域（scope）：全局作用域和函数作用域。严格模式创设了第三种作用域：eval作用域。
正常模式下，eval语句的作用域，取决于它处于全局作用域，还是处于函数作用域。严格模式下，eval语句本身就是一个作用域，不再能够生成全局变量了，它所生成的变量只能用于eval内部。

```
# 严格模式

"use strict";
var i = 1;
var j = eval("var i = 5; i");
console.log(i, j);// 1  5

# 正常模式
var i = 1;
var j = eval("var i = 5; i");
console.log(i, j);// 5  5
```

- ##### 4、禁止this关键字指向全局对象

```
# 正常模式
function foo() {
  return !this;
}
console.log(foo());// false  此时this指向全局对象

# 严格模式
function foo() {
  "use strict"
  return !this;
}
console.log(foo());// true  此时this的值为undefined
```

- ##### 5、禁止在函数内部遍历调用栈

```
function foo() {
  "use strict"
  foo.caller;
  foo.arguments;//
}
console.log(foo());
// TypeError: 'caller' and 'arguments' are restricted function properties and cannot be accessed in this context.
```

- ##### 6、不允许对只读属性赋值

> `writable`：对象属性是否可修改,flase为不可修改，默认值为true
```
"use strict";
var obj = {};
Object.defineProperty(obj, "x", {
  value: 0,
  writable: false
});
obj.x = 3;
// TypeError: Cannot assign to read only property 'x' of object '#<Object>'
```

- #### 7、不允许删除一个不允许删除的属性

```
"use strict";
delete Object.prototype; // 报错
```

- #### 8、不允许变量重名

```
"use strict";
function foo(p, p) {
  console.log("不允许变量重名")
}
foo(1, 2);
// SyntaxError: Duplicate parameter name not allowed in this context
```

- #### 9、禁止八进制表示法

```
"use strict";
var i = 0100;
// SyntaxError: Octal literals are not allowed in strict mode.
```

- #### 10、不允许使用转义字符

```
"use strict";
var x = \010;
// SyntaxError: Invalid or unexpected token
```

- #### 11、不允许对arguments赋值

```
"use strict";
arguments++; // 语法错误
var obj = {set p(arguments) {}}; // 语法错误
try {} catch (arguments) {} // 语法错误
function arguments() {} // 语法错误
var f = new Function("arguments", "'use strict'; return 17;"); // 语法错误
```

- #### 12、arguments不再追踪参数的变化

```
"use strict";
function foo(a) {
  a = 2;
  console.log(a, arguments[0]);
}
foo(1);//2  1  如果是正常模式，则结果是2  2
```

- #### 13、禁止使用arguments.callee

```
// 无法在匿名函数内部调用自身了
"use strict";　　
var f = function() {
  return arguments.callee;
};　　
f();// TypeError: 'caller', 'callee', and 'arguments' properties may not be accessed on strict mode functions or the arguments objects for calls to them
```
- #### 14、保留关键字

> 为了向将来Javascript的新版本过渡，严格模式新增了一些保留字，禁止用关键字声明变量:
implements
interface
let
package
private
protected
public
static
yield
ECMAscript第五版本身还规定了另一些保留字（class, enum, export, extends, import, super），以及各大浏览器自行增加的const保留字，也是不能作为变量名的

## 备注：

> 主流浏览器现在实现了严格模式。但是不要盲目的依赖它，因为市场上仍然有大量的浏览器版本只部分支持严格模式或者根本就不支持（比如IE10之前的版本）。严格模式改变了语义。依赖这些改变可能会导致没有实现严格模式的浏览器中出现问题或者错误。谨慎地使用严格模式，通过检测相关代码的功能保证严格模式不出问题。最后，记得在支持或者不支持严格模式的浏览器中测试你的代码。如果你只在不支持严格模式的浏览器中测试，那么在支持的浏览器中就很有可能出问题，反之亦然。


引用参考文章：

[严格模式-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)
[严格模式-阮一峰](http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html)



