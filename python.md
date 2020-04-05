---
layout: post
title: Python学习笔记
---

人生苦短，我用Python。

# 1. 编程思路

## 1.1. 遍历所有分支

编程的时候，对于每一步操作，都可能有多种结果。把这些结果组成一个输出空间Ω（omega）。好的程序需要考虑Omega里面所有情况，并相应给出处理。不好的程序，则只会考虑自己希望发生的那个输出，结果程序一有意外就崩溃。

解决方案，一个是在所有的if语句里面，都要用elseif给出明确处理结果，else仅用来处理自己未预料到的情况，比如输出依据「OOPS，意外发生了」；另外就是增加异常处理，把各种意外情况都考虑进来，而不是让程序轻易崩溃。

## 1.2. 对结果有预判

好的程序员，在程序运行之前，就会对可能出现什么结果有大致的判断，而不是先跑着试试，根据结果来反推。

那是在碰运气。

# 2. 环境

## 2.1. Conda和Anaconda

Conda 是一款 Python 的软件包管理系统。软件包管理系统有什么东东？从 Windows 过来的朋友应该和我一样感到很陌生。Windows 以前的版本是没有这个概念的，想装什么程序就单独找个安装文件安装即可。Linux 和苹果的系统使用多些，如 iPhone 上的 App Store 就是一个软件包管理系统，所有软件集中在这里下载。之前说的 pip 也是一个软件包管理系统。

Conda 没有独立的安装文件，下载安装 Anaconda 的时候就自动安装好了 Conda。

Anaconda 是一款开源的 Python 发行版，内置了Conda、Python、IPython、Jupyter、Spyder 和 720 多个开源科学包及其依赖项。利用 Conda 安装不同版本的 Anaconda，可以实现 Python 2 和Python 3的共存。

详细可查看官网 [Cheat Sheet](https://docs.continuum.io/_downloads/Anaconda_CheatSheet.pdf)。

不知怎么回事儿，我的基于窗口的 Anaconda 始终下载不下来，就只好下载一个命令行的安装文件凑合了。

下载好后，打开 Terminal，输入

`bash ~/Download/Anaconda2-4.3.0-MacOSX-x86_64.sh`

根据提示一步步安装即可。等最后出现 “Thank you for installing Anaconda!”，说明安装成功。

重启 Terminal，输入`conda --version`，确认 conda 安装成功。现在继续安装 Python 3。在 Terminal 创建新的运行环境

`conda create --name python3 python=3`

这里吐槽一下，官网给的命令是

`conda create --name snakes python=3`

百度的时候看到有人真就输入了 snakes，还煞有介事的说要激活 snakes 模块……作者写的很清楚这样做只是图好玩好不好

>  It would be wise to name this environment a descriptive name like “python3” but that is not as much fun.

好吧，这个作者也够调皮的。官方文档这样写，真的会误导不少人好不好……比如我想切换回 Python 2，官网给的命令是

`source activate snowflakes`

好嘛，死活通不过……

配置完成后，输入命令

`conda info --envs`

可以列出当前已经安装的 Python 环境，其中当前环境用 * 标识出来。比如我的电脑上有

```
(root) zhanglidong Documents $ conda info --envs
# 3. environments:
 #
python3                  /Users/zhanglidong/anaconda2/envs/python3
root                  *  /Users/zhanglidong/anaconda2
```

想要切换不同版本，在 Mac 下用

- `source activate python3`
- `source activate root`

在 Windows 下用

- `activate python3`
- `activate root`

至此，同一台电脑安装多种互不干扰的 Python 环境设置完毕。

### 3.0.1. Jupyter

IPython 是黑客 Fernando Perez 为 Python 制作的命令行交互环境，可以理解为 Python 原生交互环境的增强。

Jupyter 原本是 IPython 的一部分，后作为一个独立产品开始开发。原来的 IPython 继续做 Python shell，同时给 Jupyter 提供内核；同时原来 IPython 里面的 notebook 及其他多语言支持转移到 Jupyter 名下。Jupyter现在已经为 Julia、 R语言、 Haskell 和 Ruby 等语言提供了支持。

运行 Jupyter Notebook 的时候，可以在命令行里面输入

`ipython nootbook &`

然后当前目录就会在 Jupyter Notebook 里显示出来。

### 3.0.2. Spyder

Spyder（Scientific PYthon Development EnviRonment）是一款 Python 科学计算开发环境，可以简单理解为基于 IPython 和其他流行的 Python libraries，如 NumPy (linear algebra), SciPy (signal and image processing) 和 matplotlib (interactive 2D/3D plotting) 的一个集成式开发环境。

# 4. Collection类操作

## 4.1. List

List 是 Python 里面最常用的顺序集合类型。List 的作用是把很多类型的数据集合成一个整体来使用，并提供从左到右的顺序。

List 可变性很强，所以可以有多种使用方法。比如嵌套其他List、任意赋值等。比如

`L = ['abc', ['def', 'ghi']]`

就可以生成一个 List。

List的详细操作可以在Python环境里输入`help(list)`来获取。比较常用的操作如下：

- L.append(4)
- L.exten([5, 6, 7])
- L.index(1)
- L.sort()
- L.pop()
- L.remove(2)

### 4.1.1. 删除List中的元素

常用方法有`L.pop()`，`L.remove()`和`del L[2]`。可根据实际情况选用。

## 4.2. Dictionary

Dictionary 是 Python 内置的一种非序列化的数据结构，被称之为映射（mapping）。Dictionary 的数据是根据索引（Key）而不是顺序来存储及使用，即用 `key: value` 的方式。比较典型的使用方式如下

`D = {'food': 'Fish', 'quantity': 2}`

当调用的时候用 key 来提取，如

`D['meal'] = 'hot pot'`

所以使用 Dictionary 的时候需要知道其 Key，有时候我们可能会用到并不知道是否存在的 Key。这时候可以用关键词 in 来判断。

```
if 'key' in D:
    print 'key is a valid key in D'
else:
    print 'key is not a valid key in D'
```

## 4.3. tuple(元组)

Tuple 与 List 很类似，都是有序列的 collection 。与 List 不同的是，Tuple 的内容是不可变的。

定义 Tuple 的时候用的是括号。这样是不是可以把比如打印时候多参数后面的括号也认为是一个 Tuple？

`print 'Is this %r tuple %r not?' % (i, j)`

## 4.4. slice

index 和 slice 是 Python 对list之类最常用的一些操作。

Both index and slice assignments are in-place changes—they modify the subject list directly, rather than generating a new list object for the result. Index assignment in Python works much as it does in C and most other languages: Python replaces the object reference at the designated offset with a new one.

Slice assignment, replaces an entire section of a list in a single step. Because it can be a bit complex, it is perhaps best thought of as a combination of two steps:

1. Deletion. The slice you specify to the left of the = is deleted.
2. Insertion. The new items contained in the object to the right of the = are inserted into the list on the left, at the place where the old slice was deleted.

This isn’t what really happens, but it tends to help clarify why the number of items inserted doesn’t have to match the number of items deleted.

In effect, slice assignment replaces an entire section, or “column,” all at once. Because the length of the sequence being assigned does not have to match the length of the slice being assigned to, slice assignment can be used to replace (by overwriting), expand (by inserting), or shrink (by deleting) the subject list. It’s a powerful operation, but frankly, one that you may not see very often in practice. There are usually more straightforward ways to replace, insert, and delete (concatenation and the insert, pop, and remove list methods, for example), which Python programmers tend to prefer in practice.

还有一个需要注意的地方是，slice 的结果是产生一个新的list，所有相关操作都是对新list的操作，而不是原来的list。但是在 NumPy 里面，slice 不会产生新的list，所有对slice的操作都会影响到原来的list。这是因为 NumPy 本身是为大数据量设计的，如果每次对很大量的数据都复制一个新list的话，会极大地影响到程序性能。

## 4.5. protocol

iteration protocol 都可以用几个for循环来展开，而且for循环可读性更好。但iteration protocol 因为是用C语言实现的，一般来说性能更好，对于大量数据甚至能优化一倍，所以还是应该掌握的。

据说尤其在Python 3.x里面，更是极大地增强了……

# 5. time

time 模块用来执行关于时间的相关内容。

## 5.1. Python时间的起点

因为处理一些时间相关的东西，查到Python的时间起点是1970年1月1日，称为「纪元」，英文为epoch。所有后面的时间都是在这上面加上间隔表示。

为什么是1970年呢？查了下，原来是继承的Unix。Unix是1969年发布的雏形，1971年底出版的《Unix Programmer's Manual》里定义的Unix Time是以1971年1月1日00:00:00作为起始时间，后来就改成了人工记忆、计算比较方便的1970年了。

在这之后，很多编程语言都遵循了这一规定。Java、Ruby之类都是。

又查了一下，Excel的时间起点是1900年1月0日，为了兼容当时的表格老大Lotus 1-2-3。至于Lotus为什么选这个，就不关心了，毕竟咱从来没用过这个古老的东东……

有了这个大多数地方都遵守的起点纪元，处理时间方面的数据就方便太多了。比如CoinGecko的API的返回里面，时间就是基于这个起点的，直接用Python处理就好了，省的自己在转换。

### 5.1.1. 参考文献：

- [Unix 时间戳为什么是自 1970 年 1 月 1 日起的绝对时间？](https://www.zhihu.com/question/21503281/answer/18438073)，知乎
- [也许是最冷的电脑冷知识：1900年闰年Bug](https://zhuanlan.zhihu.com/p/29993252)，知乎
- [Time access and conversions — Python 3.7.1rc1 documentation](https://docs.python.org/3/library/time.html)，Python

## 5.2. 怎样求两个时间之间的间隔

以下常用代码块可以给出两个时间之间的差值：

```
import time
start_time = time.time()
name = raw_input('What is your name?: ')
end_time = time.time()
total_time = end_time - start_time
print 'It took %0.2f to enter your name' % total_time
```

当然这个代码块现在并不完善，比如如果输入时间太短，导致时间差舍入后为 0 应该怎么处理？等下一步更新吧。

time.time()

Return the time in seconds since the epoch as a floating point number.

# 6. 异常调试

## 6.1. assert

assert 是 Python 一个异常调试的关键词，用来在程序设计阶段调试用。其含义为声称某判断，否则就触发异常。即 `assert <test>, <data>` 等同于以下语句：

```python
if not <test>:
  raise AssertionError(<date>)
```

例如 `assert x > 0, 'x should larger than 0'` 的含义为「声称 x 应该大于 0，否则就触发异常并发出消息 ‘x should larger than 0’，即等同于

```python
if not x > 0:
  raise AssertionError('x should larger than 0')
```

这个一般是在调试阶段用，至于后期发布阶段，嗯，等着以后研究吧。

# 7. 函数类

## 7.1. Arguments

Python 定义和调用函数的时候比较灵活。定义的时候可以用 `*` 和 `**` 定义任意参数，其中 `*` 会把传入参数集合成一个 Tuple，`**` 会把传入参数集合成一个 Dictionary。比如如下代码：

```
def f(*args):
    print args

f(1, 2, 'a')
```
运行后，输入的三个参数 `1, 2, 'a'` 合并成一个 Tuple，然后打印出来，结果为

`(1, 2, 'a')`

`**` 类似，不过是以 Dictionary的形式。具体可参阅《Learn Python》的「Arbitrary Arguments Examples」章节。

函数调用的时候，`*` 和 `**` 则与定义时恰好相反，为解包（Unpack）。`*` 解包 Tuple 然后传入参数， `**` 解包 Dictionary，然后将 Value 传入参数。比如如下代码：

`func(*(1, 2), **{'d': 4, 'c': 4})`

运行后为

`func(1, 2, 4, 4)`

具体也可参阅《Learn Python》的「Arbitrary Arguments Examples」章节。

# 8. 文本处理

## 8.1. Python的格式化文本

根据[PEP 3101](https://www.python.org/dev/peps/pep-3101/)，Python有两种典型的文本格式化方法

- The '%' operator for strings. [1]
- The string.Template module. [2]

其中`%`的方法和C语言`printf`的格式化很像，简单实用，但在Python里面有很多问题，比如处理tuples 和 dictionaries时候就容易出错。string.Template用的是类似的Format String Syntax语法，很好的解决了这些问题，而且功能更强大。但强大也带来了复杂性，Format语法比`%`要复杂的多。

### 8.1.1. CStyle

`%`风格来自C语言的`printf`，但也有一些不同。标准的C语言格式为

`%[parameter][flags][width][.precision][length]type`

Python去掉了`parameter`参数，在其位置增加了`Mapping key`。根据Python文档，其关键语法为

1. The '%' character, which marks the start of the specifier.
2. Mapping key (optional), consisting of a parenthesised sequence of characters (for example, (somename)).
3. Conversion flags (optional), which affect the result of some conversion types.
4. Minimum field width (optional). If specified as an '\*' (asterisk), the actual width is read from the next element of the tuple in values, and the object to convert comes after the minimum field width and optional precision.
Precision (optional), given as a '.' (dot) followed by the precision. If specified as '\*' (an asterisk), the actual precision is read from the next element of the tuple in values, and the value to convert comes after the precision.
5. Length modifier (optional).
6. Conversion type.

Maping Key主要是为了解决类似Dict一类参数的调用问题。但这种解决方式不太优雅，这种复杂格式还是用后面谈到的Format Syntax为妙。

具体各参数的应用，可参见Python文档[《printf-style String Formatting》](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting)。其典型应用有如下代码

```
>>> p = 'This is a test for %012.2f.' % 100.123
>>> p
'This is a test for 000000100.12.'
```

其中

1. %表示格式化开始；
2. Mapping参数省略；
3. 0为flag，代表占位符，位数不足时用它填充；
4. 12为小数点前面最小长度，不足处用flag填充；
5. .2表示小数点后面精确位数；
6. f表示浮点数类型；

### 8.1.2. Sytle

[Format Sytle](https://docs.python.org/3/library/string.html#format-string-syntax)是Python在2.6版本里面引入的一种文本格式化的方法。其主要格式为

`"string content {[replacement_field]}".format(content)`

其中，replacement_field 的典型格式为 `"{" [field_name] ["!" conversion] [":" format_spec] "}"`。

`field_name`是变量标记，`!`和`:`是分隔符，分别区分`conversion`和`format_spec`。

`conversion`有三种方法，`"r" | "s" | "a"`。虽然文档没有明说，但想来默认应该是`"s"`吧。

`format_spec`内容比较复杂，也是这种方法强大所在。其语法结构为

`[[fill]align][sign][#][0][width][grouping_option][.precision][type]`

其中

- `fill`表示填充；
- `align`表示对齐；
- `sign`表示正负号；
- `#`表示进制选择；
- `0`没搞明白是什么；
- `width`表示文字宽度；
- `grouping_option`表示千分位开关；
- `precision`表示小数点后精度；
- `type`表示类型；

其中`type`可以参考% Style，大同小异；也可以参考官方文档。其典型应用有如下代码

```
>>> s = 'This is a test for {:$^+016,.2f}.'.format(100.123)
>>> s
'This is a test for $$$$+100.12$$$$$.'
```

这个`0`还是没有搞清楚是干嘛的，难不成是打酱油的……

### 8.1.3. 参考文献

- [string — Common string operations — Format String Syntax](https://docs.python.org/3/library/string.html#format-string-syntax)
- [Built-in Types — printf-style String Formatting](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting)
- [PEP 3101 -- Advanced String Formatting - Python.org](https://www.python.org/dev/peps/pep-3101/)

## 8.2. Python字符编码

处理文本逃不开编码问题。Python 2.7 里面尤其需要注意，它默认是ASSIC。Python 3好了很多，直接支持Unicode。不过用open函数打开文件时，编码是系统相关的。想要避免跨系统的问题，就必须手动指定编码。

我推荐使用Python 3，Unicode可以避免很多可能出现的问题。如果确定自己处理的文字只有中文，可以使用 gbk 编码，否则还是乖乖指定 utf8 最好。

```
ifile = open(fname, 'r', encoding='utf8')
```

Unicode 和 utf8 并不是一回事儿，网上好多大牛就这个问题写了不少文章，Wikipedia上也有很长的文章论述这个事情。不过就像[《Learn Python the Hard Way》](https://www.learnpythonthehardway.org/)里面写的，咱普通人还是不要太去抠这些细节了。投入巨大产出甚微，莫不如把更多的精力放在自己真正要做的事情上。

关于Python编码，最权威和系统的当属官方文档。以后有疑问可以多在上面查查。

> [7.2. codecs — Codec registry and base classes — Python 3.6.1 documentation](https://docs.python.org/3.6/library/codecs.html)

其中众多Python支持的标准编码列表如下：

> [7.2. codecs — Codec registry and base classes — Python 3.6.2 documentation](https://docs.python.org/3/library/codecs.html#standard-encodings)

话说貌似`utf8`的正确写法应该是`utf_8`？

### 8.2.1. 参考文献

- [Python Documentation](https://docs.python.org/3/)

# 9. 文件系统类

## 9.1. 怎样遍历文件夹

Python遍历文件夹，有现成功能可用

```
os.walk('path')
```

所以说，在Python里面，常见的功能别急着自己动手用最原始的办法搞，诸如什么递归之类。

人生苦短，我用Python。

# 10. 系统开发

## 10.1. sys.argv

从命令行启动 Python 文件的时候，命令行参数会通过 sys 模块的 argv 属性传递，其结果为一个 List。其中默认的第一个参数始终是该 Python 文件的文件名。

比如在 test.py 里面输入以下语句：

```
arg = sys.argv
print arg
```

在命令行输入

 `python test.py`

运行后会输出 [`test`]。如果在命令行输入

`python test.py try`

运行后会输出['test', 'try']。

## 10.2. Attribute

每个 module 都有一个内置属性 `__name__`。Python 按如下规则处理该属性：

- 如果该 module 是最顶层应用，`__name__` 属性在运行时自动设置为字符串 `"__main__"`。
- 若该 module 是作为模块被导入到其它模块里，`__name__` 自动设置为该模块的文件名。

所以，我们可以利用 `__name__` 属性来检查模块是自启动还是被调用。比如可以用如下代码：

```
if __name__ == "__main__":
    print "module is run by user."
else:
    print "module is imported by other module."
```

## 10.3. \_\_init\_\_.py

Python 的模块功能很有意思，不仅能导入 .py 的 module，还可以根据文件目录按 Package 方式导入。比如 dir0/dir1/func.py，就可以按如下语句导入：

`import dir1.func.py`

但为了避免与常规文件夹混淆，Python 要求 dir1 目录下必须有一个初始化文件 `__init__.py`。这个文件可以是空文件，也可以照正常初始化函数一样有代码。

## 10.4. Mac系统下如何开机自动运行Python脚本

借助`sh`脚本。代码如下

```
#!/bin/bash

python /Users/Shared/ASyncFiles/code.me.com/startup/startup.py
```

把以上代码保存，在`Login Item`里面添加，即可在登录时自动执行Python脚本。

## 10.5. 推送及运行系统命令

Git 命令本质上是在命令行里面输入一些 git 命令，所以只要我们能在 Python 里面模拟 Shell 环境输入命令即可。在[《怎样在 Python 中调用系统程序打开文件》](https://jetorz.github.io/2017-06-15-Skill-Run-a-file-systematicly-in-python.html)里面我们提到可以用`subprocess.call(["open", "about.html"])`。今天为了写这篇文章，本着严谨一点的态度又去翻看了一下文档，结果发现这个操作现在不是推荐操作了：

> The recommended approach to invoking subprocesses is to use the run() function for all use cases it can handle. For more advanced use cases, the underlying Popen interface can be used directly.  
> [17.5. subprocess — Subprocess management — Python 3.6.2 documentation](https://docs.python.org/3.6/library/subprocess.html#using-the-subprocess-module)

一般来说推荐用`run()`，更高级的可以用`Popen()`。好吧，那就用`run()`吧。`run()`的参数可以为两类，一种是 str，包含所有命令和参数，另一种是列表，即把所有命令及相关参数按列表的方式提供。Python 文档[建议采用列表](https://docs.python.org/3.6/library/subprocess.html#frequently-used-arguments)，那就按它推荐的方法来吧。

> args is required for all calls and should be a string, or a sequence of program arguments. Providing a sequence of arguments is generally preferred, as it allows the module to take care of any required escaping and quoting of arguments (e.g. to permit spaces in file names).

那下一步问题就简单了。

### 10.5.1. 代码

```
date = datetime.datetime.today().isoformat()[0:10]
status = subprocess.run(["git", "status"])
print(status)
print('**********start git add.**********')
gadd = subprocess.run(["git", "add", "."])
print('**********git add done.**********')
print('**********start git commit.**********')
gcom = subprocess.run(["git", "commit", "-m" + date])
print('**********git commit done.**********')
print('**********start git push.**********')
gpush = subprocess.run(["git", "push", "origin", "master"])
print('**********git push done.**********')
```

运行该脚本，即可自动化执行推送，Oh yeah。

### 10.5.2. 来源

- [17.5. subprocess — Subprocess management — Python 3.6.2 documentation](https://docs.python.org/3.6/library/subprocess.html

# 11. 数据分析

研究 Pandas 的时候用到了 Ndarray，其为 NumPy 里面最常用的功能，所以需要研究一下 NumPy。

## 11.1. 重建数组

常用的重建数据方法有

- ravel
- flatten
- reshape
- resize

具体使用方法可待用到的时候细查之。

## 11.2. Slicing

正常Python里slice 的结果是产生一个新的list，所有相关操作都是对新list的操作，而不是原来的list。但是在 NumPy 里面，slice 不会产生新的list，所有对slice的操作都会影响到原来的list。这是因为 NumPy 本身是为大数据量设计的，如果每次对很大量的数据都复制一个新list的话，会极大地影响到程序性能。

如果的确需要在原来的Ndarray里面新建list，可以用fancy indexing，或显式的指明要copy。

> Keep in mind that fancy indexing, unlike slicing, always copies the data into a new array.

## 11.3. 索引(indexing)和切片(slicing)

下图为 NumPy 里面多为数组的典型示意。

![](../assets/numpy-slice-index.png)

Numpy 的索引，用分别索引和列表索引都可以，如下：

- arr2d[row][col]
- arr2d[row,col]

两者是等效的。

典型的2维数组slicing如下图所示：

![](../assets/array2d-slicing.png)

# 12. Scipy

## 12.1. CDF, PDF and PPF

PPF can be used to calculate the percentile of a certain distribution.

比如normal distribution，求0.0011的percentile，用

```Python
import scipy.stats as st
st.norm.ppf(0.0011)
3.0618141517617588
```
![](assets\ppf-normal.png)

与查表基本一致。

需要注意的是不同的分布表，其取值方向是不一样的，而Scipy的很固定，一直是从左到右。

比如t distribution，

`````python
st.t.ppf(0.95, 2)
2.919985580355516
`````

因为表格是从右到左，Scipy算的时候需要用 1-alpha。

![](assets\t-ppf.png)

具体实际使用的时候，需要区分清楚自己求的值的具体用法，比如是confidence level，还是significant level。

# 13. pandas

## 13.1. 数据观察

数据观察常见函数如下：

- df.head()，观察头部数据
- df.tail()，观察尾部数据
- df.shape，返回(行数，列数)
- df.columns，返回列标题
- df.index，返回索引数据
- df.info()，返回数据总体信息
- df.describe()，返回数据统计描述
- df.plot(y='column')，打印 column 图表

## 13.2. 数据索引和切片

设 stock 为一个 DataFrame，其中 Date 为其index。常见索引和切片操作总结如下。

| Date       | Open   | High   | Low    | Close  | Volume   |
|------------|--------|--------|--------|--------|----------|
| 2017-06-01 | 153.17 | 153.33 | 152.22 | 153.18 | 16404088 |
| 2017-06-02 | 153.58 | 155.45 | 152.89 | 155.45 | 27770715 |
| 2017-06-05 | 154.34 | 154.45 | 153.46 | 153.93 | 25331662 |
| 2017-06-06 | 153.90 | 155.81 | 153.78 | 154.45 | 26624926 |

### 13.2.1. stock['column']

用 `stock['Close']` ，输出该列内容。

### 13.2.2. stock.Column

用 `stock.Close` ，输出该列内容。

### 13.2.3. stock['column']['index']

用`stock['Close']['2017-06-01']`选择某一特定单元格。

### 13.2.4. stock.Column['index']

用 `stock.Close['2017-06-01']` 的方式选择某一特定单元格。

### 13.2.5. stock.[Column][0]

用 stock['Close'][0]选择某一特定单元格。

### 13.2.6. stock[['Column']]

用列名组成list的方式选择某一列/某些列。比如 `stock[['Close']]` 或 `stock[['Close', 'Open']]`。

### 13.2.7. 'column']

用法：stock.loc['index', 'column']

比如 `stock.loc['2017-06-01', 'Close']` 选择某一单元格。

也可以通过该格式指定范围来选择，如 `stock.loc['2017-06-01':'2017-06-05', 'Open':'Close']` 。

用`loc`不仅可以索引，还可以赋值更改。

### 13.2.8. columnNum]

使用 `.iloc` 可以通过指定行/列数选择特定数据，如 `stock.iloc[0:2, :]`，其中第一个参数为行，第二个参数为列。

用`iloc`不仅可以索引，还可以赋值更改。

### 13.2.9. col]

`ix` 是一个比较灵活的选择方式，可以同时接收`loc`/`iloc` 的参数，甚至可以混在一起接受。而且赋值也可以更改，非常方便。

不过当df的列名或行名本身就是int的时候，`ix`索引将只执行行列名索引（label based），不在执行位置索引（positional based）。这个时候推荐用更直观明了的`loc`/`iloc` 。

> However, when an axis is integer based, ONLY label based access and not positional access is supported. Thus, in such cases, it’s usually better to be explicit and use .iloc or .loc.  
> [pandas.DataFrame.ix — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.ix.html?highlight=ix#pandas.DataFrame.ix)

## 13.3. 过滤

列数据可以直接比较，如 `stock.Volume > 5e7`，会把 Volumn 列的数据与后面的条件作比较，范围 True/False。

利用这种方法可以在DataFrame里面过滤数据，生成新的DataFrame，如 `stock[stock.Volume > 5e7]` 和 `stock[stock.Close > stock.Open]` 。

过逻辑关系还可以嵌套「或」和「与」，如

`stock[(stock.Close > stock.Open) & (stock.Volume > 3e7)]`

`stock[(stock.Close > stock.Open) | (stock.Volume > 5e7)]`

## 13.4. 里面的数据

如下。

```
def CleanDataFrame(datDF):
    for col in datDF.columns:
        for row in datDF.index:
            if str.isspace(datDF.ix[row, col]) == True:
                datDF.ix[row, col] = NA
    return datDF
```

## 13.5. Structures

Pandas 主要有三种数据结构如下

Dimensions | Name      | Description
-----------|-----------|--------------------------------------------------------------------------------------------------
1          | Series    | 1D labeled homogeneouly-typed array
2          | DataFrame | General 2D labeled, size-mutable tabular structure with potentially heterogeneously-typed columns
3          | Panel     | General 3D labeled, also size-mutable array

关于 Pandas 的数据结构，最好可以将高维数据理解为低维数据的容器。比如 DataFrame 是 Series 的容器，Panel 是 DataFrame 的容器。

### 13.5.1. Series

Series is a one-dimensional labeled array capable of holding any data type (integers, strings, floating point numbers, Python objects, etc.). The axis labels are collectively referred to as the index. The basic method to create a Series is to call:

`s = pd.Series(data, index=index)`

data can be many different things:

- a Python dict
- an ndarray
- a scalar value (like 5)

The passed index is a list of axis labels.

Series 感觉像一个高级点的 dict。

### 13.5.2. DataFrame

DataFrame is a 2-dimensional labeled data structure with columns of potentially different types. You can think of it like a spreadsheet or SQL table, or a dict of Series objects. It is generally the most commonly used pandas object.

Like Series, DataFrame accepts many different kinds of input:

- Dict of 1D ndarrays, lists, dicts, or Series
- 2-D numpy.ndarray
- Structured or record ndarray
- A Series
- Another DataFrame

Along with the data, you can optionally pass index (row labels) and columns (column labels) arguments. If you pass an index and / or columns, you are guaranteeing the index and / or columns of the resulting DataFrame. Thus, a dict
of Series plus a specific index will discard all data not matching up to the passed index.

If axis labels are not passed, they will be constructed from the input data based on common sense rules.

DataFrame 可以从这么多种输入里面建立，也就意味着有其复杂性，建议需要的时候在去查手册，比如官方文档「Pandas - powerful Python data analysis toolkit.pdf」，可以从官网上下载最新版。

> Pandas Manual: [http://pandas.pydata.org/pandas-docs/stable/](http://pandas.pydata.org/pandas-docs/stable/)

简单理解的话，pandas 可以看成一个表格，用 index 作行、column 做列来索引数据。

### 13.5.3. DataFrame

There are numerous ways to construct a DataFrame, though one of the most common is from a dict of equal-length lists or NumPy arrays
```
data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9]}
frame = DataFrame(data)
```

The resulting DataFrame will have its index assigned automatically as with Series, and the columns are placed in sorted order:
```
In [38]: frame
Out[38]:
   pop   state  year
0  1.5    Ohio  2000
1  1.7    Ohio  2001
2  3.6    Ohio  2002
3  2.4  Nevada  2001
4  2.9  Nevada  2002
```

If you specify a sequence of columns, the DataFrame’s columns will be exactly what you pass:
```
In [39]: DataFrame(data, columns=['year', 'state', 'pop'])
Out[39]:
   year   state  pop
0  2000    Ohio  1.5
1  2001    Ohio  1.7
2  2002    Ohio  3.6
3  2001  Nevada  2.4
4  2002  Nevada  2.9
```

### 13.5.4. Panel

Panel is a somewhat less-used, but still important container for 3-dimensional data. The term panel data is derived from econometrics and is partially responsible for the name pandas: pan(el)-da(ta)-s. The names for the 3 axes are
intended to give some semantic meaning to describing operations involving panel data and, in particular, econometric analysis of panel data. However, for the strict purposes of slicing and dicing a collection of DataFrame objects, you
may find the axis names slightly arbitrary:

- items: axis 0, each item corresponds to a DataFrame contained inside
- major_axis: axis 1, it is the index (rows) of each of the DataFrames
- minor_axis: axis 2, it is the columns of each of the DataFrames

## 13.6. 怎样对Series里的元素进行批量操作

pandas 讲究整体操作，想对里面的一些数据进行一些批量操作的时候，挨个用纯 Python 的方法，挨个遍历。这样简单是足够简单，但很不 pandasic。那有没有更为简单一些的办法呢？

Series 有个 `map` 方法，就是把函数映射到里面每个单元上，对单元进行操作。比如昨天我们说过的用`astype`修改元素类型，用 `map` 也可以实现。

```
In [3]: df = pd.DataFrame(np.random.randn(4,3), columns=list('bde'), index=['Utah','Ohio','Texas','Oregon'])

In [4]: df
Out[4]:
               b         d         e
Utah    0.241315 -0.586773 -1.365804
Ohio    0.973860 -0.600773  0.437951
Texas   1.003621 -1.142369 -1.374085
Oregon -0.290861  0.728503 -1.356081

In [34]: b = df.b

In [35]: b
Out[35]:
Utah      0.241315
Ohio      0.973860
Texas     1.003621
Oregon   -0.290861
Name: b, dtype: float64
```

创建了一个 Series，其 dtype 类型为 float。想要把它变成 float，可以 map 之。

```
In [36]: bs = b.map(str)

In [37]: bs
Out[37]:
Utah       0.2413152528188941
Ohio       0.9738595889440395
Texas      1.0036207238625463
Oregon    -0.2908605268647543
Name: b, dtype: object
```

想再换成 float，可以继续 map 之。

```
In [6]: bf = b.map(float)

In [7]: bf
Out[7]:
Utah      0.483243
Ohio     -0.778462
Texas     1.581152
Oregon   -0.109222
Name: b, dtype: float64
```

多次转换，变的是形式，不变的内心

```
In [8]: bf == b
Out[8]:
Utah      True
Ohio      True
Texas     True
Oregon    True
Name: b, dtype: bool
```

这样换来换去意义不大，但 map 将函数映射到 Series 里面的元素这个功能，还是蛮好使的。比如做工程研究，节点位移精确到小数点后两位就足够足够了，怎么样一次性把所有结果都变成小数点后两位呢？

```
In [10]: bl = b.map(lambda x: '%.2f' % x)

In [11]: bl
Out[11]:
Utah       0.48
Ohio      -0.78
Texas      1.58
Oregon    -0.11
Name: b, dtype: object
```

Oh yeah，将数据 `lambda` 一下格式就可以了。不过这样结果就变成字符串了，虽然不影响显示，但可能影响后及分析，便可以进一步优化之。

```
In [12]: bl = b.map(lambda x: float('%.2f' % x))

In [13]: bl
Out[13]:
Utah      0.48
Ohio     -0.78
Texas     1.58
Oregon   -0.11
Name: b, dtype: float64
```

`lambda` 只能用于这种简单的情况，更复杂的操作可以干脆定义一个函数调用。话说我总觉得`lambda`有点多余，已经有功能更强大的函数了，为什么还要用它呢？仅仅是因为长得漂亮么？

## 13.7. 怎样对DataFrame里的元素进行批量操作

如何对DataFrame里面的元素进行批量操作呢？

### 13.7.1. 操作

DataFrame 有个 `apply` 方法，就是把函数映射到 DataFrame 里面每个 Series 上，对 Series 进行操作。这个等于是第一次降维。

```
In [3]: df = pd.DataFrame(np.random.randn(4,3), columns=list('bde'), index=['Utah','Ohio','Texas','Oregon'])

In [4]: df
Out[4]:
               b         d         e
Utah    0.241315 -0.586773 -1.365804
Ohio    0.973860 -0.600773  0.437951
Texas   1.003621 -1.142369 -1.374085
Oregon -0.290861  0.728503 -1.356081

In [5]: df.apply(lambda x: x.max()-x.min())
Out[5]:
b    1.737881
d    1.347365
e    3.404816
dtype: float64
```

这里的 x 就是一个 Series ，对其取最大值与最小值的差，得到一个标量；批量操作 df 形成一组标量，这组标量又形成一个 Series。Series 就可以用昨天的方法进一步降维，实施批量元素操作。

那么如果想直接对 DataFrame 的元素实施批量操作怎么办呢？很容易想到的就是把上面两个方法结合起来用。pandas 内置了该方法，即`applymap`，操作如下

```
In [12]: df.applymap(lambda x: '%.2f' % x)
Out[12]:
            b      d      e
Utah     1.31   0.53  -0.90
Ohio    -0.43   0.24   0.16
Texas    0.35   0.91  -1.74
Oregon   0.14  -0.43   1.66
```

至此，批量操作问题完美解决。然而，就在我得意的时候，看到了鱼老师对之前问题的回复，顿时觉得自己探索的好没劲：

```
In [13]: round(df, 2)
Out[13]:
           b     d     e
Utah    1.31  0.53 -0.90
Ohio   -0.43  0.24  0.16
Texas   0.35  0.91 -1.74
Oregon  0.14 -0.43  1.66
```

Python 自带的 round 就可以接受 DataFrame 对象……情何以堪啊情何以堪，又是 `apply` 又是 `map` 甚至还用上 `lambda`，呵……

### 13.7.2. 总结

今天我们讨论了如何对 DataFrame 进行降维操作，可以用`apply` 对 Series进行批量操作，也可用 `applymap`对元素进行批量操作。

而实际上，很多原先只对简单对象如 int/float 之类操作的纯 Python 函数，居然也可以对 pandas 的 Series/DataFrame 进行操作，比如`abs`/`round` 之类。但对纯 Python 的 list 就不可以。

## 13.8. 多级嵌套DataFrame操作

多级索引(Hierarchical Index)的表格在我看来并不是一个好的表格。虽然给人的体验很好，但对机体验很不好，所以应该尽量避免。但处理外部数据的时候却总会遇到，比如描述统计量的杀手级武器 `describe()`，其返回结果就是一个多级索引的 DataFrame。所以还是得研究一下。

### 13.8.1. 多级索引表格操作

多级索引表格的 index 是一个 `MultiIndex` 对象。MultiIndex的对象可以看成是一组由不同级级构成的一组 Tuple，可以用常见的方法索引之，比如`df.loc[('rowl1','rowl2'),'col1']`。很多函数中也会有`level` 选项，对应的就是这里的级级。比如`df.sum(level='LC',axis=1)`。

有时候需要对一个多级索引表格进行过滤，原先那种简单过滤只适应于单层索引。对于多级索引，需要用到`xs`方法。

```
DataFrame.xs(key, axis=0, level=None, drop_level=True)
```

> Returns a cross-section (row(s) or column(s)) from the Series/DataFrame. Defaults to cross-section on the rows (axis=0).

比如要索引所有节点的均值，就可以用`dmean = df.xs('mean', axis=0, level=1)`这种方法。

### 13.8.2. 扁平化多级索引

还是不是很喜欢多级索引……所以不妨将其改变之，比如变成单级索引。就比如对 STAAD Pro计算结果进行 describe 之后的结果

```
			Absmm        Xmm        Ymm        Zmm
Node   item                                                
269.0  count  2.600000e+01  26.000000  26.000000  26.000000
	mean  -5.150000e-02   0.005423   0.027385  -0.057077
	std    9.984077e-02   0.012113   0.076432   0.090868
	min   -2.820000e-01  -0.014000  -0.012000  -0.265000
	25%   -7.250000e-02  -0.000750  -0.001750  -0.072250
	50%   -8.000000e-03   0.005000   0.000000  -0.013500
	75%    6.750000e-03   0.009750   0.012500   0.002500
	max    6.600000e-02   0.048000   0.288000   0.052000
```

其实这个多级索引，只要把前面的第 0 级的 Node 补全了，就变成一个单级索引的常规表格了。最简单的办法，便是把索引变成普通的列了。于是有代码`rsdiff = sdiff.reset_index()`。一个`reset_index`，便可以把原来的索引变成普通列。这是在对`rsdiff`进行筛选之类就简单多了。比如可以用`rmean = rsdiff[rsdiff.item == 'mean']`这样的 filter 进行筛选。

个人还是更喜欢这种方式……

### 13.8.3. 来源

- [pandas.DataFrame.xs — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.xs.html)
- [pandas.DataFrame.reset_index — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.reset_index.html)

## 13.9. Python

pandas 提及缺失数据的时候用的是 NA，numpy 用的是 NaN，Python 则有一个 None 的类型，它们三兄弟是什么关系呢？

### 13.9.1. NA@pandas

pandas 作者在《Python for Data Analysis》](https://book.douban.com/subject/10760444/) 里面谈到 missing data 的时候说

> pandas uses the floating point value NaN (Not a Number) to represent missing data in both floating as well as in non-floating point arrays.  
> The built-in Python None value is also treated as NA in object arrays.

可以看出，作者将 NaN 和 None 都作为 NA 来处理了。但是需要注意的是，pandas 里面并没有这样一个 NA 数据类型：

```
help(NA)
```

```
NameError                                 Traceback (most recent call last)
<ipython-input-31-f4bb6feeb22e> in <module>()
----> 1 help(NA)

NameError: name 'NA' is not defined
```

或者在前面加上命名空间

```
help(pd.NA)
```

```
AttributeError                            Traceback (most recent call last)
<ipython-input-32-a44ade893616> in <module>()
----> 1 help(pd.NA)

AttributeError: module 'pandas' has no attribute 'NA'
```

所以，pandas 里面的 NA，更多是综合了 NaN 和 None 的一个概念上的表述。从 pandas 文档的众多示例来看，NA 应该是倾向于 NaN 更多一些。

### 13.9.2. NaN@Numpy

[NaN 的思想来源于 IEEE](https://en.wikipedia.org/wiki/NaN)，本意是表示「虽然在概念上是数据，但不是数字」的这样一个概念。

唉，数学里面这些概念就是这么搞人。

> In computing, NaN, standing for not a number, is a numeric data type value representing an undefined or unrepresentable value, especially in floating-point calculations. Systematic use of NaNs was introduced by the IEEE 754 floating-point standard in 1985, along with the representation of other non-finite quantities like infinities.  

典型的 NaN 如下

- The divisions 0/0 and ±∞/±∞.
- The multiplications 0×±∞ and ±∞×0.
- The additions ∞ + (−∞), (−∞) + ∞ and equivalent subtractions.
- ……

Numpy 的 NaN 基本概念与此类似。NaN 是一个 float 类型，相关概念为

```
help(np.NaN)
```

```
Help on float object:

class float(object)
 |  float(x) -> floating point number
 |  ...
```

所以，float 的特性使得含有 NaN 的 DataFrame 的 DType 都是 float……也算一个比较囧的事情了。

```
all_int = pd.DataFrame([1,2,3,4,5],columns=['a'])
print("all_int's dtype is:")
print(all_int.dtypes)
print('*'*20)
one_nan = pd.DataFrame([1,2,3,np.NaN,5],columns=['a'])
print("one_nan's dtype is:")
print(one_nan.dtypes)
```

```
all_int's dtype is:
a    int64
dtype: object
********************
one_nan's dtype is:
a    float64
dtype: object
```

pandas 作者大神 Wes McKinney 对此也[很无奈的表示](https://stackoverflow.com/questions/11548005/numpy-or-pandas-keeping-array-type-as-integer-while-having-a-nan-value)：

> NaN can't be stored in an integer array. This is a known limitation of pandas at the moment; I have been waiting for progress to be made with NA values in NumPy (similar to NAs in R), but it will be at least 6 months to a year before NumPy gets these features.

看看回答的时间，2012-07-18，说好的半到一年呢……

虽然是float类型，但很多特性却不能简单的套用float。比如判断一个值是否是NaN，不能用`if a == np.NaN`，而是得用方法`if np.isnan(a)`。

### 13.9.3. None@Python

None 是 Python 原生的关于「无」的概念。None 本身作为一个数据类型，继承自 Object Type，与诸如 int/float 之类平起平坐。

```
help(None)
```

```
Help on NoneType object:

class NoneType(object)
 |  Methods defined here:
 |  ……
```

唔，道生一，一生二，二生三，三生万物，看来这个 None，就是道啊……

### 13.9.4. 总结

今天我们大致比较了一下 pandas/Numpy/Python 里面关于「无」这个概念的数据类型。pandas称之为 NA，Numpy 称之为 NaN，Python 称之为 None。其中

- NA：概念上的意义，包括 NaN 和 None；
- NaN：float 类型，本意是表示「虽然在概念上是数据，但不是数字」的这样一个概念；
- None：Python 原生的基础类型之一，表示空，表示无，表示道，表示……

### 13.9.5. 来源

- [NaN - Wikipedia](https://en.wikipedia.org/wiki/NaN)
- [Frequently Asked Questions (FAQ) — NaN, Integer NA values and NA type promotions](http://pandas.pydata.org/pandas-docs/stable/gotchas.html#support-for-integer-na)
- [python - NumPy or Pandas: Keeping array type as integer while having a NaN value - Stack Overflow](https://stackoverflow.com/questions/11548005/numpy-or-pandas-keeping-array-type-as-integer-while-having-a-nan-value)
- [Working with missing data — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/missing_data.html)
- [《Python for Data Analysis》](https://book.douban.com/subject/10760444/)，Wes McKinney

## 13.10. idxmin/idxmax

pandas 里面的 idxmin 和 argmin 看起来比较陌生，便本着每日一 Py 的原则想搞搞清楚。idxmax 和 argmax 类似，不过今天题图的美女胸比较 mini，便只看 min 吧。max 函数同理。

### 13.10.1. 分析

先从 Series 看起。从 Series 文档里面可以看出，Series 的 argmin 等于 [numpy 的 ndarray.argmin 的 Series 版](http://pandas.pydata.org/pandas-docs/version/0.20.3/generated/pandas.Series.argmin.html)，作用是用来找出第一个最小值的 index。既然返回的是 Series 的 index，那数据类型应该也是匹配的。

测试代码如下

```
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(10).reshape(2,5),columns=list('abcde'))
print(df)
```

```
a         b         c         d         e
0  0.045384  0.484123  1.112115  0.037907  0.152338
1  0.151654 -0.056504  1.918992  1.057143  0.081632
```

分别测试一下列 Series 和行 Series。

```
a = df.a
print('a is')
print(a)
print('argmin of column a is %s.' % a.argmin())
print('*'*20)
A = df.loc[1]
print('A is ')
print(A)
print('argmin of row2 is %s.' % A.argmin())
```

```
a is
0    0.045384
1    0.151654
Name: a, dtype: float64
argmin of column a is 0.
********************
A is
a    0.151654
b   -0.056504
c    1.918992
d    1.057143
e    0.081632
Name: 1, dtype: float64
argmin of row2 is b.
```

与我们预想的一致，返回了 index。

### 13.10.2. 分析

本来寻思也用类似的方法看看 idxmin，结果在文档页赫然发现和 argmin 完全一样的介绍

> This method is the Series version of ndarray.argmin.

我有点蒙，这不完全一样的功能么，为什么又两个方法？琢磨了一下，貌似可以尝试看看源代码。这就是开源的好处吧。

结果思路对了就省事儿多了。argmin 和 idxmin 的源代码链接都指向一个链接，idxmin 的源码。而且在源码后面明明确确的写着：

```
argmin = idxmin
argmax = idxmax
```

吼吼，别名而已！

### 13.10.3. 分析

DataFrame 没有 argmin 方法，只有 idxmin。我琢磨着之所以 Series 有两个一样的函数，应该是作者为了和 numpy 保持兼容吧，而他自己更倾向于用 idxmin。

既然用 pandas，还是保持 pandas 一致吧，以后都用 idxmin。这个函数可以指定不同的轴来返回不同 Series 的最小值，代码如下

```
print(df.idxmin(axis=0))
print('*'*30)
print(df.idxmin(axis=1))
```

```
a    0
b    1
c    0
d    0
e    1
dtype: int64
******************************
0    d
1    b
dtype: object
```

### 13.10.4. 总结

今天讨论了一下 pandas 里面的 argmin / idxmin 函数。对于 Series 来说，这两个其实是一个函数的两个不同名字，从源代码里面可以看出来；对于 DataFrame，则干脆没有 argmin，只有 idxmin。

所以为了保持一致性，以后可以都统一用 idxmin。这个函数可以返回当前对象第一个出现最小值的索引。

### 13.10.5. 来源

- [pandas.Series.idxmin — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.idxmin.html#pandas.Series.idxmin)
- [pandas.Series.argmin — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/version/0.20.3/generated/pandas.Series.argmin.html)
- [pandas.DataFrame.idxmin — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.idxmin.html)
- [pandas/series.py at v0.20.3 · pandas-dev/pandas](https://github.com/pandas-dev/pandas/blob/v0.20.3/pandas/core/series.py#L1213-L1239)

## 13.11. 大小

数据分析前期准备自然不可能一下子就万事俱备，后期难免需要给原来的对象补充一些数据。那么对于 DataFrame 来说，具体如何操作呢？

### 13.11.1. 添加新列

添加新列的方法非常简单，直接将列名指定相应数据即可，如 `stock['fluctuation'] = stock['High'] - stock['Low']` 。

### 13.11.2. 生成新行

生成新行的时候可以用`loc`赋值，如 `df.loc[2]= pd.Series(np.arange(10))`

这里需要注意的是，只可以用`loc`，不可以用`iloc`。尝试用`iloc`的时候系统会报错，说新赋值的行号不在索引里面。

另外，用`loc`添加Series为新列的时候需要注意，Series 如果和原来的 df 有相同的 column，即 df 的 column 和 Series 的 index 一致，是没什么问题的，否则会显示一堆 NA，除非给出参数` ignore_index=True`。

### 13.11.3. 方法增加新行

用 append 可以把一个新的 Series/dict-like object 添加到现有 df 后面，并返回一个新的 df。

用 append 我能理解，但为什么会返回一个新的 df？百思不得其解。结果后来在 pandas 文档里面查到

> Mutability and copying of data  
> All pandas data structures are value-mutable (the values they contain can be altered) but not always size-mutable. The length of a Series cannot be changed, but, for example, columns can be inserted into a DataFrame. However, the vast majority of methods produce new objects and leave the input data untouched. In general, though, we like to favor immutability where sensible.
> [Package overview — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/overview.html)

原来如此。关键部分，诸如一个 Series 的大小之类，还是不要总想着改变了。如果的确需要，最好是基于现有的数据结构再新建一个。DataFrame 呢，个人建议也是类似……保持一致性会让代码简单很多。

反正Python的垃圾回收机制，会让不再使用的数据自动销毁。

### 13.11.4. 来源

- [Package overview — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/overview.html)

# 14. matplotlib

## 14.1. 简述

我们之前说过，matplotlib 相关概念很多，使用起来较为复杂，与其花大量的时间掌握这些东西，不如在有了需求的时候，[直接去 gallery 里面找相应的代码复用](https://jetorz.github.io/2017-08-01-Python-How-to-handle-datetime.html)。不过对于一些基础概念，还是应该掌握的。

### 14.1.1. Subplots

matplotlib 绘图的时候，是需要在一个figure对象上的axes对象上画。可以把figure当成一张画布，ax是在上面的可制图区域。那么首先需要生成这两个对象。

```python
fig1 = plt.figure()
ax1 = fig1.add_subplot(1,1,1)
print(fig1, ax1)
hist = ax1.hist(np.random.randn(100), bins = 20, rwidth=0.9)
plt.show()
```

结果如下

![](../assets/matplotlibapi01.png)

pyplot 的每次操作都是在最后一次使用的 fig/Axes 上操作。将其赋予变量可以让我们在以后很方便的调用切换。由于添加 fig 和 axes 使用特高频，所以可以用 `plt.subplots` 一次完成。

```python
fig2, ax2 = plt.subplots(2, 3)
```

这样会生成一个fig对象，和一个2行3列的ax数组，可以方便的用 `ax2[row, col]` 这样的方式调用。比如利用如下代码：

```python
ax2[0,1] = plt.plot(np.arange(10), np.random.randn(10))
plt.show()
```

![](../assets/matplotlibapi02.png)

### 14.1.2. Styles

`plt.plot` 的时候可以指定颜色、线型、标记等。简化的方法是都集合在一起，比如 `plt.plot('ko--')`。不过我不太喜欢这种方式。<Zen of Python> 明确说道

> Explicit is better than implicit.

既然如此，为什么不干脆点指定个明明白白清清楚楚呢？所以相比之下我更喜欢用下面这些代码：


```python
ax2[0,2] = plt.plot(np.arange(10), np.random.randn(10), color='k', linestyle='dashed', marker='o')
plt.show()
```

![](../assets/matplotlibapi03.png)


根据 matplotlib 文档，[默认颜色设置为](https://matplotlib.org/api/colors_api.html)：

- b: blue
- g: green
- r: red
- c: cyan
- m: magenta
- y: yellow
- k: black
- w: white

当然还有其他形式的颜色表示，比如RGB之类的，但对于普通应用，这个足够了。

对于[线条设置](https://matplotlib.org/api/lines_api.html#matplotlib.lines.Line2D.set_linestyle)，有

| linestyle         | description      |
|-------------------|------------------|
| '-' or 'solid'    | solid line       |
| '--' or 'dashed'  | dashed line      |
| '-.' or 'dashdot' | dash-dotted line |
| ':' or 'dotted'   | dotted line      |
| 'None'            | draw nothing     |
| ' '               | draw nothing     |
| ''                | draw nothing     |

对于标记 Marker，内容比较多，不在此处多列，详细可见[官方文档](https://matplotlib.org/api/markers_api.html#module-matplotlib.markers)。

### 14.1.3. Legends

大多教程里面谈到 matplotlib 的时候，使用的命令都是类似 `plt.plot()` 之类的，默认调用最后使用的 AxesSubplot 对象。我一直不是很喜欢这种方式，感觉不像编程，更像交互命令。但大家都这么用而不觉得有什么不妥，让我忍不住怀疑自己的想法。直到看了 Wes McKinney 写的

> I prefer to use the subplot instance methods myself in the interest of being explicity.

顿时有种欣欣然之感。所以我们也延续这种风格，用类似 `set_xticks` 和 `set_xticklabels` 的方法来设置坐标相关的东西。相同的命令还有 `set_xlabel` 和 `set_title`，用来设置坐标名和图名。

Legends 的使用就相对简单多了。在制图的时候加上`label`选项，最后调用添加即可，如

```
ax.plot(x, y, label='one')
ax.legend(loc='best')
```

### 14.1.4. 文字及标记

文字及标记可以用`text`、`annotate` 和`arrow` 函数完成。其中`text` 和`annotate`都可以在图上做文字标记，暂不清楚其具体区别，有待以后用到的时候进一步研究。`arrow` 则很明确，是做箭头用的。

另外，需要额外增加图元，比如圆、矩形之类，也只需调用相关函数即可。这类图元都作为 `patches` 放到了 `matplotlib.patches` 模块里面，可以用`ax.add_patch(shp)` 这样的方法添加。具体内容也是等用到的时候再细研究。

嗯，发现自己属于实战型。

### 14.1.5. 坐标轴

- plt.xlim、plt.ylim 设置横纵坐标轴范围 
- plt.xlabel、plt.ylabel 设置坐标轴名称 
- plt.xticks、plt.yticks设置坐标轴刻度

示例代码：

```python
import matplotlib.pyplot as plt
import numpy as np

#创建数据
x = np.linspace(-5, 5, 100)
y1 = np.sin(x)
y2 = np.cos(x)

#创建figure窗口
plt.figure(num=3, figsize=(8, 5))
#画曲线1
plt.plot(x, y1)
#画曲线2
plt.plot(x, y2, color='blue', linewidth=5.0, linestyle='--')
#设置坐标轴范围
plt.xlim((-5, 5))
plt.ylim((-2, 2))
#设置坐标轴名称
plt.xlabel('xxxxxxxxxxx')
plt.ylabel('yyyyyyyyyyy')
#设置坐标轴刻度
my_x_ticks = np.arange(-5, 5, 0.5)
my_y_ticks = np.arange(-2, 2, 0.3)
plt.xticks(my_x_ticks)
plt.yticks(my_y_ticks)

plt.show()
```

## 14.2. matplotlib中subplot和axes的区别

记得上次研究matplotlib的时候就被subplot和axes搞的晕头转向的。这次又遇到这个问题，决定无论如何也要消灭。

上官网查了下，感觉subplot和axes没有太大本质的区别，都是Axes基类的子类。用add_subplot()方法返回的是`matplotlib.axes._subplots.AxesSubplot object`，用add_axes()方法返回的是`matplotlib.axes._axes.Axes object`。

Github的官方教程里面写到

> The Figure is the top-level container in this hierarchy. It is the overall window/page that everything is drawn on. You can have multiple independent figures and Figures can contain multiple Axes.  
> Most plotting ocurs on an Axes. The axes is effectively the area that we plot data on and any ticks/labels/etc associated with it. Usually we'll set up an Axes with a call to subplot (which places Axes on a regular grid), so in most cases, Axes and Subplot are synonymous.

也就是说，主要操作都是在axes上，axes可以通过调用subplot（方法？）生成，所以两者大多数人情况下是同义词。

大多数情况下相同，那区别呢？继续查找，在StackOverflow上找到一个解释挺好

> Both, add_axes and add_subplot add an axes to a figure. They both return a matplotlib.axes.Axes object.  
> However, the mechanism which is used to add the axes differs substantially.

大致意思是

- subplot返回的AxesSubplot，是在Axes对象上进行了一些基本的预处理，把诸如边框、间距等都根据数据进行了调整，可以直接拿来用；
- subplot是根据subplotgrid来定位，能快速生成几行几列之类的子图；axes是根据相对坐标轴的比例来定位，更灵活更强大，也就需要更多的人工操作；

至此，绝大部分问题解决。

### 14.2.1. 思考

王兴在饭否里说过的一段话挺有意思

> 一个不会游泳的人老换游泳池是不能解决问题的。

回想自己玩编程这些年，每每遇到难关尝试了几次没能解决，就琢磨着是不是换门语言更好，其实就是想靠换泳池学会游泳。如果那会儿能拿出现在这种不达目的不罢休的劲头，想来也不至于直到现在也还是菜鸟水平了罢。

### 14.2.2. 参考文献

- [matplotlib - AnatomyOfMatplotlib](https://nbviewer.jupyter.org/github/matplotlib/AnatomyOfMatplotlib/blob/master/AnatomyOfMatplotlib-Part1-Figures_Subplots_and_layouts.ipynb)，matplotlib
- [What are the differences between add_axes and add_subplot?](https://stackoverflow.com/questions/43326680/what-are-the-differences-between-add-axes-and-add-subplot)，Stack Overflow

## 14.3. matplotlib的颜色设置

matplotlib默认颜色设置为[mc]：

- b: blue
- g: green
- r: red
- c: cyan
- m: magenta
- y: yellow
- k: black
- w: white

最后选择了自己感觉对比最鲜明的。

### 14.3.1. 参考文献

- mc: [colors — Matplotlib 2.0.2 documentation](https://matplotlib.org/api/colors_api.html)

## 14.4. 如何处理时间相关内容

今天想分析一下这几年的房价，便去国家统计局网站上找了房价数据。最简单直接的办法，自然是先打张图看看了。数据内容存成一个文本文档，如下所示。

```
2017-08-01,7142
2017-07-01,7138
2017-06-01,7095
2017-05-01,7025
2017-04-01,6968
```

本以为简单的很，谁知第一步就出了问题。

### 14.4.1. date

首先读入数据，顺便转换 date 类型。

```
import pandas as pd
import numpy as mp
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
import datetime

fname = 'house_price.txt'
columns = ['date','price']
df = pd.read_csv(fname, parse_dates=True, names=columns)
print(type(df.date[0]))
```

```
<class 'str'>
```

明明我已经要求 parse_dates 了啊，为什么 date 数据类型还是 str？查了查 pandas 文档，原来 parse_dates 是仅针对 index column 的。好吧，得试试手动转换了。

```
df['date'] = pd.to_datetime(df.date)
print(type(df.date[0]))
```

```
<class 'pandas.tslib.Timestamp'>
```

本以为会出一个 datetime 类型之类，这个 Timestamp 又是个什么鬼……好吧，好歹是时间相关的，应该差不多能用了吧？

### 14.4.2. date

作图需要横纵坐标，日期类型可以自己转换，设定起始日期为 0，然后手动转换之类。但 Python 已经内置了时间类型，所以不妨直接使用。

> Matplotlib provides sophisticated date plotting capabilities, standing on the shoulders of python datetime, the add-on modules pytz and dateutil.  
> —— Matplotlib - Python Plot library

其实搞编程，有几种数据类型是最基础的：

- 数字相关(float/int...)
- 文本相关(str/text...)
- 日期相关(date/time...)
- 逻辑相关(True/False/not/and/or)
- 文件相关(file/folder/IO...)
- 数组等复合对象(list/set/dict...)
- 更高级的类/对象(class/object...)

很多人更关注与后面那些看起来更高大上的东东，实际上前面几个才是利用的最频繁最广泛的。学编程把他们的相关搞明白了，就能处理 80% 的常见问题了。

回到 matplotlib。看 matplotlib 文档很久，越看越迷糊。各种参数和设置相互关联，内容又极庞杂；更要命的是作为制图工具，实操性比较强，看完 locator 文档却发现完全不知道怎么用！

我有点蒙。琢磨了一下，这个问题不可能是我第一个遇到，与其自己搞原创，不如学习学习前面高人的手笔。遂转战 gallery，搜 date，得到一些[完全符合我要求的代码](https://matplotlib.org/examples/api/date_demo.html)。

> api example code: date_demo.py — Matplotlib 2.0.2 documentation：https://matplotlib.org/examples/api/date_demo.html

说实话，依然有点复杂。想了想，还是先直接拿来主义了。date 如何，time 如何，什么 locator， 什么 formatter，背后机理如何，对一个初学者，貌似太过深入不是什么好事儿。

起码说，容易被打击。感觉编程这东西，屁大点个事儿都需要很多背景知识。比如我只不过想用网页做一个用户界面，却需要学习 http、request、线程、HTML、CSS 甚至正则表达式……其实我想要的不过是一个能输入一些文本，以及一个能相应的按钮罢了……

所以说，对于初学者，最重要的是能有一个成品。一方面用这个成品给自己激励打劲儿，另一方面也可以有的放矢，在做中学。在做中学到的，才是最能深入到自己脑子里的。

至于更多细节，有待以后慢慢挖么。

### 14.4.3. 行动

于是，复制代码，根据自己猜测大致修改了一下。

```
years = mdates.YearLocator()   # every year
months = mdates.MonthLocator()  # every month

# 15. ticks
fig, ax = plt.subplots()

ax.xaxis.set_major_locator(years)
ax.xaxis.set_minor_locator(months)

datemin = datetime.date(df.date.min().year, 1, 1)
datemax = datetime.date(df.date.max().year + 1, 1, 1)
ax.set_xlim(datemin, datemax)

plt.plot(df.date, df.price)
plt.show()
```

结果出来，还算不错 :)。

![](../assets/datetime.png)

### 15.0.4. 总结

今天从房价入手，讨论了 pandas 在读取文件时如果没能正确解析 date 后应该如何处理的问题，以及如何在 matplotlib 里面处理 date 相关内容。

其实没能完全搞定 …… 虽然希望能把前因后果说清楚，不过对于现阶段的自己来说难度还是大了一些。所以最后采取了比较折中的方案，在 gallery 里面找类似代码复制修改了一下，得到了自己想要的结果。

虽然这种做法挺不黑客的……不过的确好使啊！囧rz……

### 15.0.5. 来源

- [Package overview — pandas 0.20.3 documentation](http://pandas.pydata.org/pandas-docs/stable/overview.html)