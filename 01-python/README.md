# Python

## 0. 关键字

###  逻辑运算符

| 关键字 | 含义 | 关键字 | 含义 | 关键字 | 含义 |
| ------ | ---- |---|---|---|---|
| `and`  | 与   | `or`   | 或   | `not`  | 非   |

## 1. 内置函数 

Python 3.12 共 [71个内置函数]()  

| **A** | **D** | **H** |  | **S** |
| --- | --- | --- | --- | --- |
| [`abs()`](https://docs.python.org/3/library/functions.html#abs) | [`delattr()`](https://docs.python.org/3/library/functions.html#delattr) | [`hasattr()`](https://docs.python.org/3/library/functions.html#hasattr) | [`memoryview()`](https://docs.python.org/3/library/functions.html#func-memoryview) | [`set()`](https://docs.python.org/3/library/functions.html#func-set) |
| [`aiter()`](https://docs.python.org/3/library/functions.html#aiter) | [`dict()`](https://docs.python.org/3/library/functions.html#func-dict) | [`hash()`](https://docs.python.org/3/library/functions.html#hash) | [`min()`](https://docs.python.org/3/library/functions.html#min) | [`setattr()`](https://docs.python.org/3/library/functions.html#setattr) |
| [`all()`](https://docs.python.org/3/library/functions.html#all) | [`dir()`](https://docs.python.org/3/library/functions.html#dir) | [`help()`](https://docs.python.org/3/library/functions.html#help) | **N**                                                        | [`slice()`](https://docs.python.org/3/library/functions.html#slice) |
| [`anext()`](https://docs.python.org/3/library/functions.html#anext) | [`divmod()`](https://docs.python.org/3/library/functions.html#divmod) | [`hex()`](https://docs.python.org/3/library/functions.html#hex) | [`next()`](https://docs.python.org/3/library/functions.html#next) | [`sorted()`](https://docs.python.org/3/library/functions.html#sorted) |
| [`any()`](https://docs.python.org/3/library/functions.html#any) | **E**                                                        | **I**                                                        | **O**                                                        | [`staticmethod()`](https://docs.python.org/3/library/functions.html#staticmethod) |
| [`ascii()`](https://docs.python.org/3/library/functions.html#ascii) | [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) | [`id()`](https://docs.python.org/3/library/functions.html#id) | [`object()`](https://docs.python.org/3/library/functions.html#object) | [`str()`](https://docs.python.org/3/library/functions.html#func-str) |
| **B**                                                        | [`eval()`](https://docs.python.org/3/library/functions.html#eval) | [`input()`](https://docs.python.org/3/library/functions.html#input) | [`oct()`](https://docs.python.org/3/library/functions.html#oct) | [`sum()`](https://docs.python.org/3/library/functions.html#sum) |
| [`bin()`](https://docs.python.org/3/library/functions.html#bin) | [`exec()`](https://docs.python.org/3/library/functions.html#exec) | [`int()`](https://docs.python.org/3/library/functions.html#int) | [`open()`](https://docs.python.org/3/library/functions.html#open) | [`super()`](https://docs.python.org/3/library/functions.html#super) |
| [`bool()`](https://docs.python.org/3/library/functions.html#bool) | **F**                                                        | [`isinstance()`](https://docs.python.org/3/library/functions.html#isinstance) | [`ord()`](https://docs.python.org/3/library/functions.html#ord) | **T**                                                        |
| [`breakpoint()`](https://docs.python.org/3/library/functions.html#breakpoint) | [`filter()`](https://docs.python.org/3/library/functions.html#filter) | [`issubclass()`](https://docs.python.org/3/library/functions.html#issubclass) | **P**                                                        | [`tuple()`](https://docs.python.org/3/library/functions.html#func-tuple) |
| [`bytearray()`](https://docs.python.org/3/library/functions.html#func-bytearray) | [`float()`](https://docs.python.org/3/library/functions.html#float) | [`iter()`](https://docs.python.org/3/library/functions.html#iter) | [`pow()`](https://docs.python.org/3/library/functions.html#pow) | [`type()`](https://docs.python.org/3/library/functions.html#type) |
| [`bytes()`](https://docs.python.org/3/library/functions.html#func-bytes) | [`format()`](https://docs.python.org/3/library/functions.html#format) | **L**                                                        | [`print()`](https://docs.python.org/3/library/functions.html#print) | **V**                                                        |
| **C**                                                        | [`frozenset()`](https://docs.python.org/3/library/functions.html#func-frozenset) | [`len()`](https://docs.python.org/3/library/functions.html#len) | [`property()`](https://docs.python.org/3/library/functions.html#property) | [`vars()`](https://docs.python.org/3/library/functions.html#vars) |
| [`callable()`](https://docs.python.org/3/library/functions.html#callable) | **G**                                                        | [`list()`](https://docs.python.org/3/library/functions.html#func-list) | **R**                                                        | **Z**                                                        |
| [`chr()`](https://docs.python.org/3/library/functions.html#chr) | [`getattr()`](https://docs.python.org/3/library/functions.html#getattr) | [`locals()`](https://docs.python.org/3/library/functions.html#locals) | [`range()`](https://docs.python.org/3/library/functions.html#func-range) | [`zip()`](https://docs.python.org/3/library/functions.html#zip) |
| [`classmethod()`](https://docs.python.org/3/library/functions.html#classmethod) | [`globals()`](https://docs.python.org/3/library/functions.html#globals) | **M**                                                        | [`repr()`](https://docs.python.org/3/library/functions.html#repr) | **_**                                                        |
| [`compile()`](https://docs.python.org/3/library/functions.html#compile) |                                                              | [`map()`](https://docs.python.org/3/library/functions.html#map) | [`reversed()`](https://docs.python.org/3/library/functions.html#reversed) | [`__import__()`](https://docs.python.org/3/library/functions.html#import__) |
| [`complex()`](https://docs.python.org/3/library/functions.html#complex) |                                                              | [`max()`](https://docs.python.org/3/library/functions.html#max) | [`round()`](https://docs.python.org/3/library/functions.html#round) |                                                              |



## 1. 变量、基本运算 




#### 简单的数学函数

|函数|作用|
|---|---|
|`abs()`|绝对值|
|`round()`|四舍五入|
|`min()`|最小值|
|`max()`|最大值|
|`divmod(a,b)`|`(div, mod)`的`tuple`|


## 2. 数据类型

### 2.1 基本数据类型 

||类型|示例|说明|
|---|----|----|---|
|整数|`int`|`1`|无大小限制|
|浮点数|`float`|`1.2`||
|复数|`complex`|`3+4j`||
|字符串|`Str`|`'hello'`|单引号或双引号引住的内容|
|列表|`List`|`[1, 1.2, 'hello']` |内部元素可以为不同类型|
|元组|`Tuple`|`('ring', 1000)`|与列表类似，元素值不可更改|
|集合|`Set`|`{1, 2, 3}`|无序不重复|
|字典|`Dict`|`{'dogs': 5, 'pigs': 3}`|无序键值对的集合|

ℹ️ **格式化字符串**和**格式化符**都非常重要，用于格式化输出内容

### 2.2 类型转换

|函数|	描述|
|---|---|
|`int(x [,base])`|将x转换为一个整数|
|`float(x)`|将x转换到一个浮点数|
|`complex(real [,imag])`|创建一个复数|
|`str(x)`|将对象 x 转换为字符串|
|`repr(x)`|将对象 x 转换为表达式字符串|
|`eval(str)`|用来计算在字符串中的有效Python表达式,并返回一个对象|
|`tuple(s)`|将序列 s 转换为一个元组|
|`list(s)`|将序列 s 转换为一个列表|
|`set(s)`|转换为可变集合|
|`dict(d)`|创建一个字典。d 必须是一个 (key, value)元组序列|
|`frozenset(s)`|转换为不可变集合|
|`chr(x)`|将一个整数转换为一个字符|
|`ord(x)`|将一个字符转换为它的整数值|
|`hex(x)`|将一个整数转换为一个十六进制字符串|
|`oct(x)`|将一个整数转换为一个八进制字符串|



