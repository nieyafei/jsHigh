# 数据类型详解

> Undefined、String、Number、Null、Boolean、Object

## Undefined类型

> 只有一个值，那就是特殊的`undefined`
如果声明的变量定义但是未对其初始化值，那么这个变量的值就是`undefined`

```
var mess;
var menn = undefined;
console.log(mess === undefined);// true
console.log(menn === undefined);// true
```

> ECMAScript第3版引入这个值，为了区分空对象指针和未经初始化的变量

**对于未声明的变量，可以使用typeof检测数据类型**

```
var mess;
console.log(typeof mess);//  undefined
console.log(typeof menn);//  undefined

对于`typeof`的判断，声明未定义的变量和未声明过的变量都返回了`undefined`值
从上面可以看出，虽然未声明的变量也赋值了`undefined`,但是如果使用也会报错的
```

## Null类型

> 是第二个只有一个值的数据类型，特殊的值是Null
表示一个空对象指针，这也是为什么typeof 检测null时会返回object的原因

```
var mess = null;
console.log(typeof mess);// object
```
> 如果准备定义一个变量来保存对象，那么初始化的变量最好是null,这样，只需要检测是否为null即可

```
var mess = null;
if (mess != null) {
  console.log("不是null")
} else {
  console.log("是null")
}// 是null
```

> undefined值是派生自null值，因此判断相等性是true

```
console.log(null == undefined);// true
console.log(null === undefined);// 注意：false
```

## Boolean类型

> 使用最多的一种类型，有两个值，分别是true和false
Boolean类型的字面值true和false，也是区分大小写的，True和False都不是Boolean值，只是标识符

任何的数据类型都可以调用Boolean

```
var str = "hello word"
console.log(Boolean(str));// true
```

**下面是各个数据类型对于的转换规则：**

| 数据类型        | 转换为true的值           | 转换为false的值  |
|:-------------:|:-------------:|:-----:|
| Boolean     | true | false |
| String | 任何非空字符串 | ""空字符串 |
| Number | 任何非零数字值（包括无穷大） | 0和NaN |
| Object |  任何对象 | null |
|Undefined | n/a | undefined |

## Number类型

> 此类型用来表示整数和浮点数值（双精度数值）
最基本的数值格式是十进制数

```
var num = 55;
var num1 = 070;// 八进制的56
八进制在严格模式下是无效的，会导致支持该模式 js 引擎抛出错误

var str = 0xA;// 16进制
console.log(str);// 10
```
- #### 浮点数值

> 所谓的浮点数值，就是值里面包括一个小数点，小数点后面必须至少有一位数字

```
var num = 10.123;// 浮点数值
```

**浮点数值需要的内存空间是保存整数值的两倍**，但是遇到一些特殊的浮点值，ECMAScript会将这些特殊的浮点值转为整数值

```
var num = 1.;// 1
var num1 = 10.0;// 10
```

- #### 数值范围

> 由于内存的限制，ECMAScript并不能保存世界上所有的数值
Number.MIN_VALUE：最小的数值，这个值是5e-324;
Number.MAX_VALUE：最大的数值，1.7976931348623157e+308

**如果计算超出范围，则会自动转换成特殊的 Infinity 值**

- #### NaN

> 非数值（Not a Number）是一个特殊的数值，表示一个本来要返回数值的操作数未返回数值的情况。

```
# 特点：
1、任何涉及NaN操作都会返回NaN;(NaN/10)
2、NaN与任何值都不相等，包括自己本身
```

**判断是否为数值的方法是isNaN(),true:不是数值，false:是数值**

```
console.log(isNaN("aaa"));// true
console.log(isNaN("2"));// false
console.log(isNaN("2.3"));// false
console.log(isNaN(NaN));// true
console.log(isNaN(true));// false   布尔值true被转换成数值1
```

- #### 数值转换

**Number()**:任何数据类型都可以使用
转换规则如下：

> 如果是Boolean值，true和false会被转成1和0
如果是数字值，只是简单的传入和返回
如果是null,返回0
如果是undefined,返回NaN
如果是字符串，则需要以下规则：
1、字符串只包括数字（包括前面带正号和负号的情况），则进行十进制数值转换
2、如果包含有效的浮点格式，则会转成对于的浮点数值。
3、如果字符串包括有效的十六进制格式，则转换为相同大小的十进制整数值
4、如果字符串是空的，则会转换成0
5、如果字符串包括上述以外的字符，则将其转换为0
如果是对象，则调用对象的 valueOf() 方法，然后依照规则转换返回值，如果转换的结果是NaN，则调用toString() 的方法，然后依次按照前面的规则进行转换

**parseInt()**：专门用于字符串转换数值，看其是否符合数值模式

> 他会忽略字符串前面的空格，直到找到第一个非空格的字符
如果第一字符不是数字字符或者负号，则会返回NaN
如果第一个字符是数字字符或者负号，会继续解析第二个字符，直到所有后续字符或者遇到非数字字符

```
console.log(parseInt(""));// NaN
console.log(parseInt("123456blue"));// 123456
```

> 也可以是吧各种整数格式（八进制、十进制、十六进制）

```
console.log(parseInt("10", 2));// 2  按照2进制解析
console.log(parseInt("10", 8));// 8  按照8进制解析
console.log(parseInt("10", 10));// 10  按照10进制解析
console.log(parseInt("AF", 16));// 175  按照16进制解析
```

**parseFloat()**：专门用于字符串转换数值

> 和parseInt()相似，但是只解析十进制，所以没有第二个参数，始终都会忽略前导的0

## String类型

> 表示由多个或者零个16位Unicode字符组成的字符序列，即字符串，字符串可用于双引号或单引号表示

- #### 字符字面量

> 转义序列，用于表示非打印字符，或者具有其他用途的字符

|字面量|含义|
|:------|:--------------|
|\n|换行|
|\t|制表|
|\b|退格|
|\r|回车|
|\f|进纸|
| \\\ |斜杠|
|\'|单引号，在单引号表示的字符串中使用|
|\"|双引号，再用双引号表示的字符串使用|
|\xnn|以十六进制代码nn表示一个字符（其中n为0-F）|
|\unnn|以十进制代码nnn表示的一个Unicode字符（其中n为0-F）|

- #### 字符串特点

> ECMAScript中的字符串不可变的，字符串一旦创建，值就不能改变，如果想改变，首先要销毁原来的字符串，然后用另外一个包含新值得字符串填充该变量

- #### 转换为字符串

> toString()方法：数值，布尔值，对象和字符串值都有此方法，但是Undefined,Null没有这个方法

> String()方法：能够将任何值进行转换为字符串

- 如果值有toString()方法，则调用该方法（没有参数），并返回相应的结果
- 如果是null,则返回“null”
- 如果值是undefined,怎返回“undefined”

## Object类型

> 一组数据和功能的集合，对象可以通过new操作符后跟要穿甲的对象类型的名称来创建
var o = new Object();

#### Object属性和方法

- constructor：保存着用于创建当前对象的函数，构造函数（constructor）就是Object()

- hasOwnProperty(propertyName)：用于检查给定的属性在当前对象实例中（而不是实例的原型中）是否存在，其中，作为参数的属性名（propertyName）必须以字符串形式指定

- isPrototypeOf(object)：用于检查传入的对象是否是当前对象的原型

- propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够通过for-in语句来枚举，与hasOwnProperty()方法一样，作为参数的属性名必须以字符串的形式指定。

- toLocaleString()：返回对象的字符串表示，该字符串与执行环境的地区对应

- toString()：返回对象的字符串表示

- valueOf()：返回对象的字符串、数值或布尔值表示。通常和toString()方法返回相同