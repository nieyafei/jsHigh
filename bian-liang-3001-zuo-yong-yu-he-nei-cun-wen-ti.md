# 变量、作用域和内存问题

## 基本类型和引用类型的值

> 变量可能包含两种不同数据类型的值：基本数据类型（`Undefined`,`Null`,`String`,`Number`,`Boolean`）和引用数据类型（`Object`）

将一个值赋给对象时，解析器必须确定这个值是基本数据类型值还是引用数据类型值

### 动态属性

> 创建对象并且给对象赋值

```
var num = new Object();
num.name="aaa";
console.log(num.name);
```
### 复制变量值

> 如果复制一个基本类型的值，则在变量对象上创建一个心智，然后把该值复制到新的变量位置上

```
var a = "aaa";
var b = a;// 虽然a和b的值是一样的，但是值是完全独立的，这两个变量可以参与任何操作而不受影响
```
> 如果复制一个引用类型的变量，也会将储存在变量中的值复制一份到新的变量的储存空间上，但是这个值的副本其实是一个指针，而这个指针指向存储在堆中的一个变量

```

var obj = new Object();
var obj2 = obj;
obj.name = "liLy";
console.log(obj2.name);// liLy
```
### 传递参数

> 所有函数的参数都是`按值传递`的，也就是说函数外部的值复制给函数内部的参数，

```
var count = 20;
function sum(num){
  num +=10;
  return num;
}
sum(count);// count：20    结果是30
```
```
function setName(obj, name) {
  obj.name = name;
}

var person = new Object();
var person2 = new Object();
setName(person, "lily");
setName(person2, "lily2");

console.log(person, person2);// { name: 'lily' } { name: 'lily2' }
```
### 检测类型

> typeof 操作符是确定变量是字符串，数字，布尔值还是undefined的最佳工具，如果变量是一个对象或者null或者数组，则typeof会返回Object
对于引用类型的检测，提供了`instanceof`操作符

```
var person = new Object();
console.log(typeof(person));// object
console.log(person instanceof Object);// true

var person2 = [1, 2, 3];
console.log(typeof(person2));// object
console.log(person2 instanceof Object);// true

var person3 = null;
console.log(typeof(person3));// object
console.log(person3 instanceof Object);// false
```
```
var person2 = [1, 2, 3];
console.log(typeof(person2))；// object
console.log(person2 instanceof Array);// true   这是一个数组

var person3 = new RegExp();
console.log(typeof(person3));// object
console.log(person3 instanceof RegExp);// true   正则表达式
```

## 执行环境及作用域

> 执行环境定义了变量或函数有权访问的其他数据，决定了各自的行为
每个执行环境都有一个与之关联的`变量对象`，环境中定义的所有变量和函数都保存在这个对象中

> 全局执行环境是最外围的一个执行环境，在web浏览器中，全局执行环境被认为是window对象

每个函数都有自己的执行环境，当执行流进入一个函数时，函数的环境就会被推入一个环境栈中。函数执行之后，栈将其环境弹出，控制权返回给之前的执行环境。
当代码在一个环境中执行是，会创建变量对象的一个 `一个作用域链`，保证对执行环境的有权访问所有变量和函数的有序访问。
如果这个环境是函数，则将其 ` 活动对象`作为变量对象。活动对象最开始只包含一个变量`arguments`(全局对象不存在)

```
var color = "blue";// 全局变量

function changeColor() {
  // 在此可以调用全局变量，并且更改其值
  if (color === "blue") {
    color = "black";
  } else {
    color = "red";
  }
  var temColor = "#333";// 外部无法调取此变量
}

changeColor();
```

**延长作用域链**
> try-catch语句的catch语块：会创建一个新的对象
with语句：会将指定的对象添加到作用域链中
这两个语句都会在作用域链前端添加一个变量对象

```
var localObj = {
  name: "前端蜗牛",
  size: 25
}

function getName() {
  var start = "我是",
    start2 = "今年";
  with(localObj) {
    var totalName = start + name + start2 + size;
  }
  return totalName;
}
console.log(getName());// 我是前端蜗牛今年25
```
**没有块级作用域**

```
# if语句中的变量声明会将变量添加到当前的执行环境

if (true) {
  var col = "nihao";
}
console.log(col);// nihao
```
**声明变量**
> 使用var来声明变量，会自动添加到最接近的环境中。在函数内部，最接近的环境就是函数内部环境
with语句中，最接近的环境是函数环境
如果初始化时没有使用var声明，该变量就会被自动添加到全局环境

**查询标识符**
> 在某个环境中读取或写入而引用一个标识符时，必须通过搜索来确定该标识符实际代表什么，搜索过程中从作用链前端开始，向上逐级查询与给定的名字匹配的标识符，如果局部环境找到该标识符，则搜索停止，如果没有找到该变量名，则沿作用域链向上搜索，一直追溯到全局环境的变量对象，如果全局环境中没有找到，说明为定义该变量

## 垃圾收集

> javascript有自动垃圾收集机制

- 标记清除

- 引用次数

- 性能问题

- 管理内存






