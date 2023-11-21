## Python-01
> 基于[廖雪峰](https://www.liaoxuefeng.com/wiki/1016959663602400), 后续根据学习内容补充

#### 简介

1. print()打印输出，`,`会在打印时作为1个空格
2. input，Python2中`input()`默认输入的是数字，字符串需要用`""`，`raw_input`则默认输入的是字符串，如果是数字则需要用`int()` `float()` 进行强制类型转换；Python3中只有`input()`，其用法和Python2中的`raw_input()`相同

### Python基础

#### 数据类型和变量

1. 字符串：`'` `"`都可以表示字符串，同时可以`'"'` `"'"`，可以用双引号打印单引号，单引号同理。
2. `\`为转义字符，`\n`换行，`\t`制表符, `\\`表示\本身
3. `r'str'`表示引号内的字符串默认不转义
4. `''' '''` 三引号可以多行打印，替代`\n`
5. 布尔运算符为`and` `or` `not` ,运算结果为 `True` `False`
6. 除法：`/`在Python2中结果会根据是否都为整数，结果显示为整数或浮点数，Python3中则无论除数被除数形式，全部为浮点数。`floor`除法，即取整运算，`//`在Python2,3中会向下取整

```python
>>> (-4.2)//2
-3.0
>>> 4.2//2
2.0
>>> 4//2
2
```

7. 取余运算：`%`，整数类型取余仍为整数，浮点数取整后仍为浮点数

```python
>>> 10%3
1
>>> 10.0%3
1.0
```

#### 编码

`ASCII`最早的127个字符被编码到计算机里，也就是大小写英文字母、数字和一些符号

`Unicode`把所有语言都统一到一套编码里，这样就不会再有乱码问题，但是，如果你写的文本基本上全部是英文的话，用Unicode编码比ASCII编码需要多一倍的存储空间，在存储和传输上就十分不划算  

`UTF-8`把`Unicode`编码转化为“可变长编码”的编码。UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。如果你要传输的文本包含大量英文字符，用UTF-8编码就能节省空间

> 在计算机内存中，统一使用Unicode编码，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码。用记事本编辑的时候，从文件读取的UTF-8字符被转换为Unicode字符到内存里，编辑完成后，保存的时候再把Unicode转换为UTF-8保存到文件
>
> 浏览网页的时候，服务器会把动态生成的Unicode内容转换为UTF-8再传输到浏览器 

#### Str

1. Python3采用`Unicode`编码，即支持多语言
2. `ord()`函数获取单一字符的十进制整数表示
3. `chr()`函数将十进制编码转化为对应字符

4. 转码：大致了解即可

由于Python的字符串类型是`str`，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把`str`变为以字节为单位的`bytes`。

Python对`bytes`类型的数据用带`b`前缀的单引号或双引号表示：

```python
x = b'ABC'
```

要注意区分`'ABC'`和`b'ABC'`，前者是`str`，后者虽然内容显示得和前者一样，但`bytes`的每个字符都只占用一个字节。

以Unicode表示的`str`通过`encode()`方法可以编码为指定的`bytes`，例如：

```Python
>>> 'ABC'.encode('ascii')
b'ABC'
>>> '中文'.encode('utf-8')
b'\xe4\xb8\xad\xe6\x96\x87'
>>> '中文'.encode('ascii')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)
```

纯英文的`str`可以用`ASCII`编码为`bytes`，内容是一样的，含有中文的`str`可以用`UTF-8`编码为`bytes`。含有中文的`str`无法用`ASCII`编码，因为中文编码的范围超过了`ASCII`编码的范围，Python会报错。

在`bytes`中，无法显示为ASCII字符的字节，用`\x##`显示。

反过来，如果我们从网络或磁盘上读取了字节流，那么读到的数据就是`bytes`。要把`bytes`变为`str`，就需要用`decode()`方法：

```Python
>>> b'ABC'.decode('ascii')
'ABC'
>>> b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
'中文'
```

如果`bytes`中包含无法解码的字节，`decode()`方法会报错：

```Python
>>> b'\xe4\xb8\xad\xff'.decode('utf-8')
Traceback (most recent call last):
  ...
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xff in position 3: invalid start byte
```

如果`bytes`中只有一小部分无效的字节，可以传入`errors='ignore'`忽略错误的字节：

```Python
>>> b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore')
'中'
```

5. `len()`函数计算`str`的字符数，如果是转化的`bytes`，则返回字节数
6. 格式化输出：`%d` `%f` `%s` `%x`分别表示 整数、浮点数、字符串、十六进制整数 占位符

```python
name = kewei
score = 99
print('Hi, $s, your score is %d.' % (name, score))
# 有几个%?占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个%?，括号可以省略。
```

#### List

1. `list`是一种有序的集合，可以随时添加和删除其中的元素, 用`[ ]`定义
2. `len()`返回list元素个数
3. 增：`listName.append()`在末尾增加元素，`listName.insert(index, )`在特定位置插入
4. 删：`listName.pop()`删除末尾元素，`listName.pop(index)`删除特定位置元素
5. 改：直接赋值给相应位置元素即可,`listName[i] = var`
6. 查：用`listName[i]` 索引，可以用`-1`返回最后一个元素
7. list内元素类型可以不同，`str` `int` `float` `bool` ,或者也是一个list
8. 没有元素的list为空list，长度为0。`listName = []`

#### tuple

1. 定义后不可变的列表，用`( )`定义
2. 没有增、删、改操作
3. 空tuple，`tupleName = ()`
4. 一个元素，为了与数学公式区分，需要加`,`，`tupleName = (1,)`
5. tuple的不变是指元素指向不变，而元素的子内容不能保证不变。当tuple的元素是list时，指向的list是不变的，但是list内的元素可变

#### dict

1. dict全称dictionary，在其他编程语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。 
2. `key`不能重复，由不可变元素组成(int, str),用`{ }`定义

```python
d = {'Michael':95, 'Bob':75, 'Tracy:85'}
```

3. 增：三种方式可以向字典增加元素

```python
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}	#create dict
d.update({'hh':22})	#1 直接传入一个字典
d.update(hh=22)		#2 直接给出key,value,此时key不需要引号
d['hh']=22			#3 直接赋值法
```

4. 删：要删除一个key，用`pop(key)`方法，对应的value也会从dict中删除：

```
   >>> d.pop('Bob')
   75
   >>> d
   {'Michael': 95, 'Tracy': 85}
```

5. 改：一个`key`对应一个`value`，如果多次对一个key赋值， 后面的值会把前面的值冲掉。如果不存在，就会报错：

```
>>> d['Thomas']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'Thomas'
```

要避免key不存在的错误，有两种办法，一是通过`in`判断key是否存在：

```
>>> 'Thomas' in d
False
```

二是通过dict提供的`get()`方法，如果key不存在，可以返回`None`，或者自己指定的value：

```
>>> d.get('Thomas')
>>> d.get('Thomas', -1)
-1
```

注意：返回`None`的时候Python的交互环境不显示结果。

6. 查： dict内部存放的顺序和key放入的顺序是没有关系，通过key查找value

==和list比较，dict有以下几个特点：==

1. 查找和插入的速度极快，不会随着key的增加而变慢；
2. 需要占用大量的内存，内存浪费多。

而list相反：

1. 查找和插入的时间随着元素的增加而增加；
2. 占用空间小，浪费内存很少。

所以，dict是用空间来换取时间的一种方法。

#### set

1. 和dict类似，也是一组key的集合，但不存储value。
2. key不可重复，不能是可变对象，在set内无序
3. 创建：`set()`函数只接收一个参数，因此需要输入一个list，或者字符串。重复元素会被自动过滤

```
>>> s = set('abcc')
>>> s
{'c', 'a', 'b'}

>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```

4. 增：`.add(key)`可以添加元素，重复元素没有效果

```python
>>> s.add(4)
>>> s
{1, 2, 3, 4}
>>> s.add(4)
>>> s
{1, 2, 3, 4}
```

5. 删：`.remove(key)`删除元素

```python
>>> s.remove(4)
>>> s
{1, 2, 3}
```

6. set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：

```
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```

## Python-02
> 基于[廖雪峰](https://www.liaoxuefeng.com/wiki/1016959663602400), 后续根据学习内容补充

### 函数

1. 函数名是一个函数对象的应用，可以赋值给变量，相当于给函数取了别名
2. [python3 内置函数文档]( https://docs.python.org/3/library/functions.html#abs ) 

##### 强制数据类型转换

`int()` `str()` `float()` `bool()` 

#### 函数定义

1. `def`关键字自定义函数

```python
def myabs(x):
    if x>=0:
        return x
    else:
        return -x
```

2. 通过`import`导入自定义或者第三方函数。`from absFile import myabs`语句是导入`asbFile.py`中的`myabs`函数
3. 空函数：什么都不做的函数，即用`pass`做占位符，

```python
def nop():
    pass
# 同样可以用在其他语句中，先占位，这样就不会有语法错误
if a > 90:
    pass
```

##### 参数检查

1. 可以用内置函数`isinstance()`做参数类型检查

```python
def myAbs(x):
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```

##### 返回多个值

比如在游戏中经常需要从一个点移动到另一个点，给出坐标、位移和角度，就可以计算出新的坐标：

```
import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
```

`import math`语句表示导入`math`包，并允许后续代码引用`math`包里的`sin`、`cos`等函数。

然后，我们就可以同时获得返回值：

```
>>> x, y = move(100, 100, 60, math.pi / 6)
>>> print(x, y)
151.96152422706632 70.0
```

但其实这只是一种假象，Python函数返回的仍然是单一值：

```
>>> r = move(100, 100, 60, math.pi / 6)
>>> print(r)
(151.96152422706632, 70.0)
```

原来返回值是一个`tuple`！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个`tuple`，但写起来更方便。

#### 函数的参数

##### 位置参数

1. 普通参数，按照位置依次传入，也是必须传入的参数

##### 默认参数

1. 针对重复度很高的参数，比如计算幂次时的2，输入学生信息时的年龄，可以设置为默认参数。这样可以降低函数的调用难度

2. 位置：在必选参数之后

3. 形式：`def myFun(x, y, z = 10):`，其中x,y为必选参数，即位置参数，z为默认参数

4. 调用方式有两种：

   * 按顺序输入: `myFun(1,2,3)`即按照位置参数的用法，输入参数即可。这样的方式对于只有很少的 默认参数是方便的，尤其是只有1个的时候，但是几个默认参数意味着要按顺序全部输入才行。

   * 按照参数名就行赋值: `myFun(1,2,z=5)`的方式，可以按照默认参数名进行调用，此时不需要按照默认参数顺序，更方便。

5. **默认参数必须指向不变对象** ，list这种对象会变，而默认参数只是默认了参数指向，当list本身改变时，会改变默认参数的值

##### 可变参数

1. 可变参数就是传入的参数个数是可变的，可以是1个、2个到任意个，还可以是0个。 
2. 可变参数在函数调用时自动组装为一个`tuple`, 可以在函数内对参数进行`tuple`数据类型操作
3. 形式为`def calc(*numbers):`定义时用`*`标记为可变参数
4. 非可变参数情况下，需要传入一个list/tuple，`calc([1,2,3])`，如果在定义时定义为可变参数，则可以直接调用为`calc(1,2,3)` ，这是目前看到的最大意义
5. **无法在写程序时确定变量长度的情况**，都可以通过直接传入一个list/tuple解决，并不需要用可变参数。`calc(numbers)`中`numbers`可以是随时改变大小的list，不会影响运算，同样可以用可变参数的方式写`calc(*numbers)`，这样也是可以的，不过后一种情况的list每个元素均被视为一个参数

##### 关键字参数

1. 关键字参数允许传入0个或任意个**含参数名的参数**
2. 关键字参数在函数内部自动组装为一个`dict`
3. 定义方式为：`def person(name, age, **kw):`，`**`标记为关键字参数
4. 应用场景： 它可以扩展函数的功能。比如，在`person`函数里，我们保证能接收到`name`和`age`这两个参数，但是，如果调用者愿意提供更多的参数，我们也能收到。试想你正在做一个用户注册的功能，除了用户名和年龄是必填项外，其他都是可选项，利用关键字参数来定义这个函数就能满足注册的需求。 
5. 定义过关键字参数后，可以用`key-value`的方式传入任意个变量，也可以直接传入一个`dict`

```python
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
# 和可变参数类似，也可以先组装出一个dict，然后，把该dict转换为关键字参数传进去：            
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, city=extra['city'], job=extra['job'])
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
# 上面复杂的调用可以用简化的写法：
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}          
```

**值得注意**,最后一种的调用方式， `**extra`表示把`extra`这个dict的所有key-value用关键字参数传入到函数的`**kw`参数，`kw`将获得一个dict，注意`kw`获得的dict是`extra`的一份拷贝，对`kw`的改动不会影响到函数外的`extra`。 

6. 缺点：**关键字参数**无法确定到底传入了哪些关键字，需要`if..in..`语句判断。但这种判断是被动的，并不能限制输入的关键字。

```python
def person(name, age, **kw):
    if 'city' in kw:
        # 有city参数
        pass
    if 'job' in kw:
        # 有job参数
        pass
    print('name:', name, 'age:', age, 'other:', kw)
```



##### 命名关键字参数

1. **命名关键字参数**是限制关键字名字的**关键字参数**，本质上输入的还是`dict`
2. 定义方式：用`*`占一个参数位置用以声明后续的参数都是命名关键字参数。如果有可变参数，则无需该声明符，可变参数后续的参数都是命名关键字参数

```python
def person(name, age, *, city, job):
    print(name, age, city, job)
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

3. 调用方式：必须传入参数名，否则会人为是位置参数，造成参数数目报错

```
>>> person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer
```

```
>>> person('Jack', 24, 'Beijing', 'Engineer')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: person() takes 2 positional arguments but 4 were given
```

4. 命名关键字参数可以有缺省值，从而简化调用：

```python
def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
```

由于命名关键字参数`city`具有默认值，调用时，可不传入`city`参数：

```
>>> person('Jack', 24, job='Engineer')
Jack 24 Beijing Engineer
```

##### 参数组合

1. 定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。
2. **定义顺序**必须是：`必选参数`、`默认参数`、`可变参数`、`命名关键字参数`和`关键字参数`。
3.  对于必选参数、可变参数，可以用一个`tuple`传入，命名关键字参数和关键字参数可以用一个`dict`，即： 对于任意函数，都可以通过类似`func(*args, **kw)`的形式调用它，无论它的参数是如何定义的。 

 #### 递归函数

1. 定义： 如果一个函数在内部调用自身本身，这个函数就是递归函数。 

2. 举个例子，我们来计算阶乘`n! = 1 x 2 x 3 x ... x n`，用函数`fact(n)`表示，可以看出：

   fact(n) = n! = 1 x 2 x 3 x ... x (n-1) x n = (n-1)! x n = fact(n-1) x n

   所以，`fact(n)`可以表示为`n*fact(n-1)`，只有n=1时需要特殊处理。

   于是，`fact(n)`用递归的方式写出来就是：

   ```
   def fact(n):
       if n==1:
           return 1
       return n * fact(n - 1)
   ```

3. 递归函数的优点是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。 

4. 栈溢出：使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（`stack`）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。 
5. ==尾递归==：解决递归调用栈溢出的方法是通过**尾递归**优化，事实上尾递归和循环的效果是一样的，所以，把循环看成是一种特殊的尾递归函数也是可以的。 

尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

上面的`fact(n)`函数由于`return n * fact(n - 1)`引入了乘法表达式，所以就不是尾递归了。要改成尾递归方式，需要多一点代码，主要是要把每一步的乘积传入到递归函数中：

```python
def fact(n):
    return fact_iter(n, 1)

def fact_iter(num, product):
    if num == 1:
        return product
    return fact_iter(num - 1, num * product)
```

可以看到，`return fact_iter(num - 1, num * product)`仅返回递归函数本身，`num - 1`和`num * product`在函数调用前就会被计算，不影响函数调用。

==尾递归==的设计思路是将`return`语句中的计算，放在递归函数内部

6. 尾递归调用时，如果做了优化，栈不会增长，因此，无论多少次调用也不会导致栈溢出。

   遗憾的是，大多数编程语言没有针对尾递归做优化，Python解释器也没有做优化，所以，即使把上面的`fact(n)`函数改成尾递归方式，也会导致栈溢出。


## Python-03

> 基于[廖雪峰](https://www.liaoxuefeng.com/wiki/1016959663602400), 后续根据学习内容补充

### 高级特性

* 用更少的代码实现更高级的功能

#### 切片

1. 方括号加数字的方式直接索引：`L[start:end:step]` ,如果从第一个或最后一个开始索引，可以缺省参数

```python
>>> L = list(range(100))
>>> L
[0, 1, 2, 3, ..., 99]
>>> L[:10]	# 0可以省略
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> L[-10:]	# 负数也可以
[90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
>>> L[10:20]
[10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
>>> L[::5]	# 按步长取
[0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]
```

2.  tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple 

3.  字符串`'xxx'`也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串 

在很多编程语言中，针对字符串提供了很多各种截取函数（例如，substring），其实目的就是对字符串切片。Python没有针对字符串的截取函数，只需要切片一个操作就可以完成，非常简单。 

**练习题** 

利用切片操作，实现一个trim()函数，去除字符串首尾的空格，注意不要调用str的`strip()`方法：

```
# -*- coding: utf-8 -*- 
def trim(s): 
	if s[:1]==' ':
        s=trim(s[1:])
    elif s[-1:]==' ':
        s=trim(s[:-2])

    return s
```

以上代码参考自评论区，利用递归实现，简直太方便了

#### 迭代

1.  迭代(Iteration): 通过for循环进行遍历
2. 不同于其他语言，通过遍历下标来进行迭代，Python中任何可以迭代的数据对象，均可以直接用`for x in X`的结构实现，`x`是`X`内的元素，不需要有下标

3. `dict`迭代：`key`,`value`，因为dict的存储不是按照list的方式顺序排列，所以，迭代出的结果顺序很可能不一样。

```
d = {'a': 1, 'b': 2, 'c': 3}
for key in d:
for value in d.values()
for k, v in d.items()
```

4. `str`迭代：`for ch in 'ABC':`可以循环打印字符串的每个字符
5. 如何判断是否可以迭代： collections模块的Iterable类型判断 

```
>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
False
```

5.  内置的`enumerate`函数可以把一个list变成==索引-元素对==，可以在`for`循环中同时迭代索引和元素本身

```
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C
```

6. `for`循环可以同时引用几个变量

```
>>> for x, y in [(1, 1), (2, 4), (3, 9)]:
...     print(x, y)
...
1 1
2 4
3 9
```

**练习题**： 

请使用迭代查找一个list中最小和最大值，并返回一个tuple： 

```python
# -*- coding: utf-8 -*-
def findMinAndMax(L):
	if L == []:
        return (None, None)
    max = min = L[0]
    for x in L:
        if x > max:
            max = x
        elif x < min:
            min = x
    return min,max
```

#### 列表生成式

1. ==List Comprehensions==,可以用来创建List的生成式。
2. `range`函数生成：`list(range(1,11))`，生成`[1,2,..,10]`
3. 将`for`,`if`放在列表生成式内，直接用一行代码生成目标list，既可以结合`range()`生成list，也可对现有的可迭代对象进行处理

```python
# 生成x^2
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
# 生成偶数的x^2
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
# 使用两层循环，可以生成全排列：
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
# 也可以使用两个变量来生成list：
>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> [k + '=' + v for k, v in d.items()]
['y=B', 'x=A', 'z=C']
# 把一个list中所有的字符串变成小写
>>> L = ['Hello', 'World', 'IBM', 'Apple']
>>> [s.lower() for s in L]
['hello', 'world', 'ibm', 'apple']
```

**练习** 

如果list中既包含字符串，又包含整数，由于非字符串类型没有`lower()`方法，所以列表生成式会报错：

```
>>> L = ['Hello', 'World', 18, 'Apple', None]
>>> [s.lower() for s in L]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 1, in <listcomp>
AttributeError: 'int' object has no attribute 'lower'
```

使用内建的`isinstance`函数可以判断一个变量是不是字符串：

```python
# -*- coding: utf-8 -*-
L1 = ['Hello', 'World', 18, 'Apple', None]
L2 = [s.lower for s in L1 if isinstance(s,str)]
```

#### 生成器

1. 列表生成式生成的列表有容量限制，会占用巨大的内存空间
2. ==generator==是一种记录元素算法，但不一次全部结算出来，而是在循环中不断计算的机制
3. 生成方法 1：直接把列表生成式的`[]`改成`()` 
4. `list`可以直接打印出来，`generator`需要用`next()`函数逐个打印，遇到`StopIteration`错误停止，更常用的是`for`循环打印
5. 生成方法 2：经常会遇到复杂的数列，无法用列表生成式实现，可以通过函数来实现，关键字为`yield`

```python
# 对比function, generator
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        print(b)
        a, b = b, a + b	# 非常方便的赋值语句，无需中间变量
        n = n + 1
    return 'done'
#---------------------------------------#
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```

6.  如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator 。 这里，最难理解的就是generator和函数的执行流程不一样。函数是顺序执行，遇到`return`语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次返回的`yield`语句处继续执行。 
7.  用`for`循环调用generator时，发现拿不到generator的`return`语句的返回值。如果想要拿到返回值，必须捕获`StopIteration`错误，返回值包含在`StopIteration`的`value`中 

```python
>>> g = fib(6)
>>> while True:
...     try:
...         x = next(g)
...         print('g:', x)
...     except StopIteration as e:
...         print('Generator return value:', e.value)
...         break
...
g: 1
g: 1
g: 2
g: 3
g: 5
g: 8
Generator return value: done
```

**练习**

用一个generator不断输出杨辉三角的下一行：

```python
# -*- coding: utf-8 -*-
def triangles():    
    L=[1]
    while True:
        yield L
        L=[1]+[L[i]+L[i+1] for i in range(len(L)-1)]+[1]
```

* `list(range(0))`生成一个空列表

#### 迭代器

