# Python

Guido van Rossum在1989年圣诞节期间，为了打发无聊的圣诞节而编写的一个编程语言。

编译器首先会进行语法检查，代码检查

为了不带入过多的累赘，Python 3.0在设计的时候没有考虑向下兼容。不同版本的python.exe使用不同的命名，命令行中可以调用的到`python` `python3`.virtualenv 和 virtualenvwrapper 来管理不同项目的依赖环境，通过 workon 、 mkvirtualenv 等命令进行虚拟环境切换

* 网络应用，包括网站、后台服务等等；
* 许多日常需要的小工具，包括系统管理员需要的脚本任务等等；
* 把其他语言开发的程序再包装起来，方便使用。
* 1行代码能实现的功能，决不写5行代码。请始终牢记，代码越少，开发效率越高。

缺点

* 代码少的代价是运行速度慢，C程序运行1秒钟，Java程序可能需要2秒，而Python程序可能就需要10秒。Python是解释型语言，你的代码在执行时会一行一行地翻译成CPU能理解的机器码，这个翻译过程非常耗时，所以很慢。而C程序是运行前直接编译成CPU能执行的机器码，所以非常快。

## 解释器

* 官方版本的解释器：CPython。这个解释器是用C语言开发的，所以叫CPython。在命令行下运行python就是启动CPython解释器。
* Python是基于CPython之上的一个交互式解释器，也就是说，IPython只是在交互方式上有所增强，但是执行Python代码的功能和CPython是完全一样的。CPython用>>>作为提示符，而IPython用In [序号]:作为提示符。
* 目标是执行速度。PyPy采用JIT技术，对Python代码进行动态编译（注意不是解释），所以可以显著提高Python代码的执行速度。绝大部分Python代码都可以在PyPy下运行，但是PyPy和CPython有一些是不同的，这就导致相同的Python代码在两种解释器下执行可能会有不同的结果。
* Jython是运行在Java平台上的Python解释器，可以直接把Python代码编译成Java字节码执行。

## 环境管理

### MAC

```shell
brew install python3
```

### 版本管理工具pyenv:修改系统环境变量 PATH

多版本python共存的环境工具，可以在不改变系统环境的情况下，可以随意切换不同python版本。基于某个版本开发的工具，在更换了不同python版本之后，就会导致工具中的某个模块、代码错误，而不能正常使用。

```shell
brew install pyenv

pyenv versions   // 查看当前系统中所有可用的 Python 版本
pyenv commands
pyenv install -l  //可使用版本列表
pyenv install 3.5.1 // 安装
pyenv uninstall 3.5.1
pyenv which python // 显示路径
pyenv global 3.5.2  // 从三个维度来管理 Python 环境，简称为： 当前系统 、 当前目录 、 当前shell 。这三个维度的优先级从左到右依次升高，即 当前系统 的优先级最低、 当前shell 的优先级最高。
pyenv local 3.5.2
pyenv shell 3.5.2

$ curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
export PATH=$HOME/.pyenv/bin:$PATH  //加进系统的环境变量 ～／.zshrc
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

pyenv -v
pyenv doctor
pyenv update
pyenv install --list
cat ~/.pyenv/version
pyenv version
```

### 虚拟沙盒virtualenv

virtualenv为应用提供了隔离的Python运行环境，解决了不同应用间多版本的冲突问题。

```shell
pip install virtualenv
virtualenv --no-site-packages app_env
source app_env/bin/activate
deactivate

brew install pyenv-virtualenv  // 集成安装
virtualenv
virtualenv-delete
virtualenv-init
virtualenv-prefix
virtualenvs

pyenv virtualenvs // 看到本地所有的项目环境
pyenv virtualenv 3.5.0 v_env_3.5.0
pyenv activate v_env_3.5.0
pyenv deactivate
pyenv uninstall v_env_3.5.0
pyenv virtualenv PYTHON_VERSION PROJECT_NAME
```

## wheel

Wheels are the new standard of python distribution and are intended to replace eggs.`pip install wheel`

## 包管理工具easy_install.py和pip(pip3 python3)第三方包的安装管理

Python2.7的安装包中，easy_install.py是默认安装的，而pip需要我们手动安装

```shell
python get-pip.py   //windows

sudo apt-get install python-pip

sudo easy_install pip
pip install 'Markdown<2.0'
pip install 'Markdown>2.0,<2.0.3'
pip show --files SomePackage
pip install selenium   # 安装模块包
pip list                        # 列出已安装的包
pip list --outdated             # 查看哪些软件需要更新
pip show --files Package        # 查看安装包时安装了哪些文件
pip uninstall Package           # 卸载软件包
pip search Package              # 搜索软件包
pip install --upgrade/-U Package        # 升级软件包

pip freeze > requirements.txt        # 导出 //Requirements文件 一般记录的是依赖软件列表，通过pip可以一次性安装依赖软件包:
pip install -r requirements.txt         # 安装

pip completion --bash >> ~/.profile // Bash  pip命令自动补全
~/.profile

pip completion --zsh >> ~/.zprofile  //对于zsh
 ~/.profile
```

## 工具

* [iPython](https://github.com/ipython/ipython) - 更强大的python交互shell，支持变量自动补全，自动缩进，支持 bash shell 命令，内置了许多很有用的功能和函数
* [Anaconda](https://github.com/DamnWidget/anaconda):有命令行与图形界面两种方式,Anaconda turns your Sublime Text 3 in a full featured Python development IDE including autocompletion, code linting, IDE features, autopep8 formating, McCabe complexity checker Vagrant and Docker support for Sublime Text 3 using Jedi, PyFlakes, pep8, MyPy, PyLint, pep257 and McCabe that will never freeze your Sublime Text 3
* jupyter

## 教程

### 执行环境

* 命令行模式下
    * 可以直接运行.py文件 `python hello.py`
    * 添加`#!/usr/bin/env python3`,文件添加执行权限`./basic.py`
* 交互模式：`python` `exit()`
*  (代码助手)[https://raw.githubusercontent.com/michaelliao/learn-python3/master/teach/learning.py]

### 基础

计算机要根据编程语言执行任务，就必须保证编程语言写出的程序决不能有歧义，所以，任何一种编程语言都有自己的一套语法，编译器或者解释器就是负责把符合语法的程序代码转换成CPU能够执行的机器码，然后执行

#### 输入与输出

* `#开头的语句是注释`
* print()在括号中加上字符串，就可以向屏幕上输出指定的文字
* 可以接受多个字符串，用逗号“,”隔开，就可以连成一串输出（会依次打印每个字符串，遇到逗号“,”会输出一个空格）
* 输入计算过程
* input()，可以让用户输入字符串，并存放到一个变量里

```python
print('hello, world')
print('The quick brown fox', 'jump over', 'the lazy dog')
print('100 + 200 =', 100 + 200)
name = input('please enter your name: ') // 有提示框
print('hello,', name)
```

#### 数据类型与变量

在计算机内部，可以把任何数据都看成一个“对象”，而变量就是在程序中用来指向这些数据对象的，对变量赋值就是把数据和变量给关联起来。对变量赋值x = y是把变量x指向真正的对象，该对象是变量y所指向的。随后对变量y的赋值不影响变量x的指向。
* 基本类型
    - 整数:Python可以处理任意大小的整数，当然包括负整数，在程序中的表示方法和数学上的写法一模一样，例如：1，100，-8080，0，等等。二进制、十六进制表示整数比较方便，十六进制用0x前缀和0-9，a-f表示，例如：0xff00，0xa5b4c3d2，等等。
    - 浮点数:浮点数也就是小数，之所以称为浮点数，是因为按照科学记数法表示时，一个浮点数的小数点位置是可变的，比如，1.23x109和12.3x108是完全相等的。浮点数可以用数学写法，如1.23，3.14，-9.01，等等。或者用科学计数法表示，把10用e替代，1.23x10^9就是1.23e9，或者12.3e8，0.000012可以写成1.2e-5，等等。整数和浮点数在计算机内部存储的方式是不同的，整数运算永远是精确的（除法难道也是精确的？是的！），而浮点数运算则可能会有四舍五入的误差。也没有大小限制，但是超出一定范围就直接表示为inf（无限大）
    - 字符串:以单引号'或双引号"括起来的任意文本，比如'abc'，"xyz"等等。请注意，''或""本身只是一种表示方式，不是字符串的一部分，因此，字符串'abc'只有a，b，c这3个字符。如果'本身也是一个字符，那就可以用""括起来，比如"I'm OK"包含的字符是I，'，m，空格，O，K这6个字符。
        + 字符串内部既包含'又包含"怎么办？可以用转义字符\来标识.\n表示换行，\t表示制表符，字符\本身也要转义，所以\\表示的字符就是\
        + 用r''表示''内部的字符串默认不转义
        + 用'''...'''的格式表示多行内容,输入时换行时添加空格
    - 布尔值:只有True、False两种值,可以直接用True、False表示布尔值（请注意大小写）
    - 空值:Python里一个特殊的值，用None表示。None不能理解为0，因为0是有意义的，而None是一个特殊的空值。
* 复合元素
    - 列表：list是一种有序的集合，可以随时添加和删除其中的元素。元素的数据类型也可以不同。可以嵌套(多维数组).查找元素，全表遍历。list越大，查找越慢。
    - 有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改.
        + 当定义一个tuple时，在定义的时候，tuple的元素就必须被确定下来
        + 可以嵌套list：可以修改
    - dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度.无论这个表有多大，查找速度都不会变慢.先在字典的索引表里（比如部首表）查这个字对应的页码（索引遍历）。通过key计算位置的算法称为哈希算法（Hash），要保证hash的正确性，作为key的对象就不能变。字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key
        + 一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉
        + dict的key必须是不可变对象
        + 如果获取的key不存在，dict就会报错：两种方法判断
        + dict内部存放的顺序和key放入的顺序是没有关系的
    - dict与list比较：用空间来换取时间的一种方法
        + 查找和插入的速度极快，不会随着key的增加而变慢；
        + 需要占用大量的内存，内存浪费多。
    - set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key
        + 提供一个list作为输入集合
        + 重复元素在set中自动被过滤
        + 数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集
        + set和dict的唯一区别仅在于没有存储对应的value，但是，set的原理和dict一样，所以，同样不可以放入可变对象，因为无法判断两个可变对象是否相等，也就无法保证set内部“不会有重复元素”。
* 变量不仅可以是数字，还可以是任意数据类型 
    - 必须是大小写英文、数字和_的组合，且不能用数字开头
    - 等号=是赋值语句，可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量
    - 变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言。静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。例如Java是静态语言
    - 变量创建过程：在内存中创建了一个'ABC'的字符串；在内存中创建了一个名为a的变量，并把它指向'ABC'。
* *可变对象与不可变对象* （值操作与引用操作）
    - a是变量，而'abc'才是字符串对象！有些时候，我们经常说，对象a的内容是'abc'，但其实是指，a本身是一个变量，它指向的对象的内容才是'abc'
    - replace方法创建了一个新字符串'Abc'并返回
    - 对于不变对象来说，调用对象自身的任意方法，也不会改变该对象自身的内容。相反，这些方法会创建新的对象并返回，这样，就保证了不可变对象本身永远是不可变的。
    - 因为不变对象一旦创建，对象内部的数据就不能修改，这样就减少了由于修改数据导致的错误。此外，由于对象不变，多任务环境下同时读取对象不需要加锁，同时读一点问题都没有。我们在编写程序时，如果可以设计一个不变对象，那就尽量设计成不变对象。
* 常量：用全部大写的变量名表示常量。不能变的变量。事实上PI仍然是一个变量，Python根本没有任何机制保证PI不会被改变，所以，用全部大写的变量名表示常量只是一个习惯上的用法
```python
print('I\'m ok.')
print('I\'m learning\nPython.')
print('\\\n\\')
print(r'\\\t\\')
print('''line1
line2
line3''')
print(r'''hello,\n
world''')
True
3 > 2
True and True
True or False
5 > 3 or 1 > 3
not 1 > 2

classmates = ['Michael', 'Bob', 'Tracy']
classmates[0] #  'Michael'  获取元素
classmates[-1] # 'Tracy' 
classmates.append('Adam')  # ['Michael', 'Bob', 'Tracy', 'Adam']
classmates.insert(1, 'Jack') # ['Michael', 'Jack', 'Bob', 'Tracy', 'Adam']
classmates.pop() # 'Adam'   删除list末尾的元素
classmates.pop(1)  # 'Jack' 删除指定索引
classmates[1] = 'Sarah' # 元素赋值

s = ['python', 'java', ['asp', 'php'], 'scheme']
len(s) # 4
s[2][1]
L = []

d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
d['Adam'] = 67 # 添加
'Thomas' in d # 判断是否存在
d.get('Thomas', -1) # 添加默认值
d.pop('Bob') # 删除

s = set([1, 2, 3])
s.add(4)
s.remove(4)
s1 = set([1, 2, 3])
s2 = set([2, 3, 4])
s1 & s2
s1 | s2

a = 'ABC'
b = a.replace('A', 'a')
a # 'ABC'
b # 'aBC'
```
##### 高级特性

* 切片（slice）：取一个list或tuple的部分元素.倒数第一个元素的索引是-1 L[begin:end:foot].还支持tuple str
* 迭代：通过for循环来遍历这个list或tuple，这种遍历我们称为迭代（Iteration）。只要是可迭代对象(list、tuple、dict、set、str)，无论有无下标，都可以迭代.enumerate函数可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代索引和元素本身
* 列表生成式即List Comprehensions，是Python内置的非常简单却强大的可以用来创建list的生成式.运用列表生成式，可以快速生成list，可以通过一个list推导出另一个list
* 生成器generator:通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。是否可以在循环的过程中不断推算出后续的元素.
    - generator保存的是算法，每次调用next(g)，就计算出g的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误。
    - 只要把一个列表生成式的[]改成()，就创建了一个generator.通过next()函数获得generator的下一个返回值,通过for循环来迭代
    - 一个函数定义中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator.遇到yield就中断，下次又继续执行
* 迭代器Iterator：可以被next()函数调用并不断返回下一个值的对象称为迭代器：Iterator。
    - Iterator对象表示的是一个数据流，Iterator对象可以被next()函数调用并不断返回下一个数据，直到没有数据时抛出StopIteration错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过next()函数实现按需计算下一个数据，所以Iterator的计算是惰性的，只有在需要返回下一个数据时它才会计算。
* 可迭代对象Iterable：可以直接作用于for循环的对象统称为可迭代对象：一类是集合数据类型，如list、tuple、dict、set、str等；一类是generator，包括生成器和带yield的generator function。
    - 生成器都是Iterator对象，但list、dict、str虽然是Iterable，却不是Iterator。把list、dict、str等Iterable变成Iterator可以使用iter()函数
```python
s = ['python', 'java', ['asp', 'php'], 'scheme']
s[0:3] # ['python', 'java', ['asp', 'php']]
s[:3] # ['python', 'java', ['asp', 'php']]
s[1:3] # ['java', ['asp', 'php']]
s[-2:] # [['asp', 'php'], 'scheme']

L = list(range(100))
L[:10]
L[-10:] # [90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
L[10:20] # [10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
L[:10:2] # [0, 2, 4, 6, 8]
L[::5] # [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]
L[:] # [0, 1, 2, 3, ..., 99] 原样复制一个list
(0, 1, 2, 3, 4, 5)[:3] # (0, 1, 2)
'ABCDEFG'[::2] # 'ACEG'
'ABCDEFG'[:3] # 'ABC'
classmates = ('Michael', 'Bob', 'Tracy'，['A', 'B'])
t[2][1] = 'Y'
t = () # 定义一个空的tuple
t = (1,) # 只有1个元素的tuple定义时必须加一个逗号

from collections import Iterable
isinstance('abc', Iterable) # str是否可迭代

d = {'a': 1, 'b': 2, 'c': 3}
for key in d
for value in d.values()
for k, v in d.items()
for ch in 'ABC'

for i, value in enumerate(['A', 'B', 'C']):
    print(i, value)

for x, y in [(1, 1), (2, 4), (3, 9)]:
    print(x, y)

[x * x for x in range(1, 11)]
[x * x for x in range(1, 11) if x % 2 == 0]
[m + n for m in 'ABC' for n in 'XYZ'] # ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

import os # 导入os模块，模块的概念后面讲到
[d for d in os.listdir('.')] # os.listdir可以列出文件和目录

d = {'x': 'A', 'y': 'B', 'z': 'C' }
[k + '=' + v for k, v in d.items()]  # ['y=B', 'x=A', 'z=C']

g = (x * x for x in range(10))
for n in g:
    print(n)

def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
g = fib(5)
next(g)
next(g)
next(g)

while True:
     try:
         x = next(g)
         print('g:', x)
     except StopIteration as e:
         print('Generator return value:', e.value)
         break

from collections import Iterator
isinstance([], Iterable) # True

from collections import Iterator
isinstance((x for x in range(10)), Iterator) # True
isinstance([], Iterator) # False
isinstance(iter([]), Iterator) # True
```

##### 运算符

* /除法计算结果是浮点数，即使是两个整数恰好整除，结果也是浮点数
* //，称为地板除，两个整数的除法仍然是整数
* 余数运算，可以得到两个整数相除的余数
```python
10 / 3
10 // 3
10 % 3
```

##### 编码

字符与字节的转换 *区分字符与字节*

* Python 3版本中，字符串是以Unicode编码的
* 把Unicode编码转化为“可变长编码”的UTF-8编码。UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。如果你要传输的文本包含大量英文字符，用UTF-8编码就能节省空间
* 单个字符的编码，Python提供了ord()函数获取字符的整数表示，chr()函数把编码转换为对应的字符(单字符与码的转换)
* 字符串类型是str，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把str变为以字节为单位的bytes。
* bytes类型的数据用带b前缀的单引号或双引号表示：'ABC'和b'ABC'，前者是str，后者虽然内容显示得和前者一样，但bytes的每个字符都只占用一个字节
* 纯英文的str可以用ASCII编码为bytes，内容是一样的，含有中文的str可以用UTF-8编码为bytes。含有中文的str无法用ASCII编码，因为中文编码的范围超过了ASCII编码的范围，Python会报错。
* 在bytes中，无法显示为ASCII字符的字节，用\x##显示。
* 从网络或磁盘上读取了字节流，那么读到的数据就是bytes。要把bytes变为str，就需要用decode()方法
* bytes中包含无法解码的字节，decode()方法会报错
* 如果bytes中只有一小部分无效的字节，可以传入errors='ignore'忽略错误的字节
* len()函数计算的是str的字符数，如果换成bytes，len()函数就计算字节数
* 遇到str和bytes的互相转换。为了避免乱码问题，应当始终坚持使用UTF-8编码对str和bytes进行转换。
* `#!/usr/bin/env python3` 告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释
* 由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。`# -*- coding: utf-8 -*-`当Python解释器读取源代码时，为了让它按UTF-8编码读取，申明了UTF-8编码并不意味着你的.py文件就是UTF-8编码的，必须并且要确保文本编辑器正在使用UTF-8 without BOM编码
* 格式化输出：%运算符就是用来格式化字符串的。在字符串内部，有几个%?占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个%?，括号可以省略。格式化整数和浮点数还可以指定是否补0和整数与小数的位数
    - %s表示用字符串替换
    - %d表示用整数替换
    - %f    浮点数
    - %x    十六进制整数
    - 不太确定应该用什么，%s永远起作用，它会把任何数据类型转换为字符串
    - 字符串里面的%是一个普通字符怎么办？这个时候就需要转义，用%%来表示一个%
* 另一种格式化字符串的方法是使用字符串的format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}……
```python
ord('A')
ord('中')
chr(66)
chr(25991)
'\u4e2d\u6587' # '中文'
x = b'ABC'
'ABC'.encode('ascii')   # b'ABC'
'中文'.encode('utf-8') # b'\xe4\xb8\xad\xe6\x96\x87'

b'ABC'.decode('ascii')  # 'ABC'
b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8') #  '中文'
b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore') # '中'

len('ABC') # 3
len('中文') # 2

len(b'ABC') # 3
len(b'\xe4\xb8\xad\xe6\x96\x87') # 6
len('中文'.encode('utf-8')) # 6

#!/usr/bin/env python3  
# -*- coding: utf-8 -*-

'Hi, %s, you have $%d.' % ('Michael', 1000000)
print('%2d-%02d' % (3, 1)) # 3-01
print('%.2f' % 3.1415926) # 3.14

'Age: %s. Gender: %s' % (25, True) # 'Age: 25. Gender: True'

'growth rate: %d %%' % 7 # 'growth rate: 7 %'

'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)  # 'Hello, 小明, 成绩提升了 17.1%'
```

##### 控制语句

* 判断语句
* 循环:for while
* break语句可以提前退出循环
* continue语句，跳过当前的这次循环，直接开始下一次循环
```python
age = 3
if age >= 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')

if x:  # 只要x是非零数值、非空字符串、非空list等，就判断为True，否则为False。
    print('True')

s = input('birth: ') # input()返回的数据类型是str，str不能直接和整数比较，必须先把str转换成整数
birth = int(s)

sum = 0
for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    sum = sum + x
print(sum)
for x in range(11):
    sum = sum + x
print(sum)

sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)

n = 1
while n <= 100:
    if n > 10: # 当n = 11时，条件满足，执行break语句
        break # break语句会结束当前循环
    print(n)
    n = n + 1
print('END')

n = 0
while n < 10:
    n = n + 1
    if n % 2 == 0: # 如果n是偶数，执行continue语句
        continue # continue语句会直接继续下一轮循环，后续的print()语句不会执行
    print(n)
```

##### 函数

函数就是最基本的一种代码抽象的方式。

* 函数名其实就是指向一个函数对象的引用，完全可以把函数名赋给一个变量
    - abs(-10)是函数调用，而abs是函数本身
    - 函数名其实就是指向函数的变量
* 内置函数：调用一个函数，需要知道函数的名称和参数（个数与数据类型），数据类型转换
* 定义一个函数要使用def语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用return语句返回。
    - 一旦执行到return时，函数就执行完毕，并将结果返回
    - 如果没有return语句，函数执行完毕后也会返回结果，只是结果为None。return None可以简写为return
    - 函数引用：把my_abs()的函数定义保存为abstest.py文件了，用from abstest import my_abs来导入my_abs()函数，注意abstest是文件名（不含.py扩展名）
    - pass语句什么都不做，实际上pass可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个pass，让代码能运行起来。
    - 多值返回：返回值是一个tuple！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值
* 参数
    - 位置参数：power(x, n)函数有两个参数：x和n，这两个参数都是位置参数，调用函数时，传入的两个值按照位置顺序依次赋给参数x和n
    - 默认参数：含有默认值，调用时可以省略赋值。能降低调用函数的难度（减少对默认参数的顾虑）
        + 必选参数在前，默认参数在后。
        + 变化大的参数放前面，变化小的参数放后面。变化小的参数就可以作为默认参数。
        + 也可以不按顺序提供部分默认参数。当不按顺序提供部分默认参数时，需要把参数名写上。比如调用enroll('Adam', 'M', city='Tianjin')
        + 因为默认参数L也是一个变量，它指向对象[]，每次调用该函数，如果改变了L的内容，则下次调用时，默认参数的内容就变了，不再是函数定义时的[]了。(作用域)
    - 可变参数：传入的参数个数是可变的。`*nums`表示把nums这个list的所有元素作为可变参数传进去。`*args`是可变参数，args接收的是一个tuple；可变参数既可以直接传入：func(1, 2, 3)，又可以先组装list或tuple，再通过`*args`传入：func(*(1, 2, 3))
    - 关键字参数：扩展函数的功能，如果调用者愿意提供更多的参数，也能收到，`**kw`是关键字参数，kw接收的是一个dict.可以直接传入：func(a=1, b=2)，又可以先组装dict，再通过**kw传入：func(**{'a': 1, 'b': 2})
    - 命名关键字参数：限制关键字参数的名字，例如，只接收city和job作为关键字参数。必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错
        + 命名关键字参数需要一个特殊分隔符*，*后面的参数被视为命名关键字参数
        + 如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了
        + 命名关键字参数必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错
    - 以上参数方法可以相互组合：参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。
* 递归函数：如果一个函数在内部调用自身本身，这个函数就是递归函数
    - 定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。
    - 注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。
    - 解决栈溢出：尾递归优化，事实上尾递归和循环的效果是一样的，所以，把循环看成是一种特殊的尾递归函数也是可以的。
        + 尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。(算法优化)
        + 大多数编程语言没有针对尾递归做优化，Python解释器也没有做优化，所以，即使把上面的fact(n)函数改成尾递归方式，也会导致栈溢出。

```python
abs(-10) # 函数调用
abs # 函数本身

abs(100)
help(abs)
max(2, 3, 1, -5)
int('123')
int(12.34) # 12
float('12.34')
str(100)
bool(1) # True
bool('') # False
a = abs # 变量a指向abs函数
a(-1) # 所以也可以通过a调用abs函数
hex(100) # 一个整数转换成十六进制表示的字符串

def my_abs(x):
    if not isinstance(x, (int, float)):  # 参数检测
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x

def nop():  #空函数
    pass

import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
x, y = move(100, 100, 60, math.pi / 6)

def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s

def enroll(name, gender, age=6, city='Beijing'):
    print('name:', name)
    print('gender:', gender)
    print('age:', age)
    print('city:', city)
enroll('Adam', 'M', city='Tianjin')

def add_end(L=[]):
    L.append('END')
    return L
add_end()
add_end() # ['END', 'END']
def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L

def calc(numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
calc([1, 2, 3]) # 14
calc(1, 2, 3) # 报错

def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
nums = [1, 2, 3]
calc(*nums)

def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
person('Adam', 45, gender='M', job='Engineer') # name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
extra = {'city': 'Beijing', 'job': 'Engineer'}
person('Jack', 24, **extra)

def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
person('Jack', 24, city='Beijing', job='Engineer')
person('Jack', 24, job='Engineer')
def person(name, age, *args, city, job):
    print(name, age, args, city, job)

def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)
f1(1, 2, 3, 'a', 'b', x=99) # a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
def f2(a, b, c=0, *, d, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)

args = (1, 2, 3, 4)
kw = {'d': 99, 'x': '#'}
f1(*args, **kw) # a = 1 b = 2 c = 3 args = (4,) kw = {'d': 99, 'x': '#'}

args = (1, 2, 3)
kw = {'d': 88, 'x': '#'}
f2(*args, **kw) # a = 1 b = 2 c = 3 d = 88 kw = {'x': '#'}

def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)

def fact(n):
    return fact_iter(n, 1)

def fact_iter(num, product):
    if num == 1:
        return product
    return fact_iter(num - 1, num * product)
```

##### 函数是式编程 Functional Programming

函数式编程就是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用
一个特点就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！Python对函数式编程提供部分支持。由于Python允许使用变量，因此，Python不是纯函数式编程语言。

* 高阶函数：函数的参数能够接收别的函数
    - map()函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回.
    - reduce把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算
    - filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素.关键在于正确实现一个“筛选”函数
    - 排序算法 sorted（），可以接收一个key函数来实现自定义的排序
* 返回函数：

```python
def add(x, y, f):
    return f(x) + f(y)
print(add(-5, 6, abs))

def f(x):
     return x * x
r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
list(r) # [1, 4, 9, 16, 25, 36, 49, 64, 81]  由于结果r是一个Iterator，Iterator是惰性序列，因此通过list()函数让它把整个序列都计算出来并返回一个list
def normalize(name):
        return  name.capitalize()
L1 = ['adam', 'LISA', 'barT']
L2 = list(map(normalize, L1))
print(L2)

from functools import reduce
def fn(x, y):
     return x * 10 + y
reduce(fn, [1, 3, 5, 7, 9]) # 13579

def str2int(s):
    def fn(x, y):
        return x * 10 + y
    def char2num(s):
        return {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}[s]
    return reduce(fn, map(char2num, s)) # 13579

def char2num(s):   # lambda 写法
    return {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}[s]
def str2int(s):
    return reduce(lambda x, y: x * 10 + y, map(char2num, s))

def not_empty(s):
    return s and s.strip()
list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))

def _odd_iter():  # 构造素数
    n = 1
    while True:
        n = n + 2
        yield n
def _not_divisible(n):
    return lambda x: x % n > 0
def primes():
    yield 2
    it = _odd_iter() # 初始序列
    while True:
        n = next(it) # 返回序列的第一个数
        yield n
        it = filter(_not_divisible(n), it) # 构造新序列
for n in primes():
    if n < 1000:
        print(n)
    else:
        break

sorted([36, 5, -12, 9, -21])
sorted([36, 5, -12, 9, -21], key=abs)
sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)
sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)

```

## 框架

* [django/django](https://github.com/django/django)The Web framework for perfectionists with deadlines. <https://www.djangoproject.com/>
* [pallets/flask](https://github.com/pallets/flask)A microframework based on Werkzeug, Jinja2 and good intentions <http://flask.pocoo.org/>
* [tornadoweb/tornado](https://github.com/tornadoweb/tornado)Tornado is a Python web framework and asynchronous networking library, originally developed at FriendFeed. <http://www.tornadoweb.org/>

## 搭建服务器todo

## 教程

- [python3](http://www.runoob.com/python3)
- [Python教程 廖雪峰](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)
- <http://www.cnblogs.com/linhaifeng/p/7278389.html>

## basic

- map:函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回

- reduce:把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算 `reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`

## 插件

- [xadmin](https://github.com/sshwsfc/xadmin) [文档](https://xadmin.readthedocs.io/en/latest/index.html)
- [django-bootstrap-toolkit](https://github.com/dyve/django-bootstrap-toolkit)

## 库

- numpy
- scipy
- matplotlib
- scikit-learn
- pandas

## 扩展

- [faif/python-patterns](https://github.com/faif/python-patterns)A collection of design patterns/idioms in Python
- [requests/requests](https://github.com/requests/requests)Python HTTP Requests for Humans™ ✨🍰✨ <http://python-requests.org>
- [scrapy/scrapy](https://github.com/scrapy/scrapy)Scrapy, a fast high-level web crawling & scraping framework for Python. <https://scrapy.org>
- [fchollet/keras](https://github.com/fchollet/keras)
- [kennethreitz/python-guide](https://github.com/kennethreitz/python-guide)
- [ipython/ipython](https://github.com/ipython/ipython)
- [binux/pyspider](https://github.com/binux/pyspider)A Powerful Spider(Web Crawler) System in Python. <http://docs.pyspider.org/>
- [fabric/fabric](https://github.com/fabric/fabric)Simple, Pythonic remote execution and deployment. <http://fabfile.org>
- [vinta/awesome-python](https://github.com/vinta/awesome-python):A curated list of awesome Python frameworks, libraries, software and resources https://awesome-python.com/
- [keon/algorithms](https://github.com/keon/algorithms)Minimal examples of data structures and algorithms in Python

## 工具

- ipython:`pip3 install ipython`
- [nvbn/thefuck](https://github.com/nvbn/thefuck):Magnificent app which corrects your previous console command.
- [donnemartin/interactive-coding-challenges](https://github.com/donnemartin/interactive-coding-challenges)Huge update! Interactive Python coding interview challenges (algorithms and data structures). Includes Anki flashcards.
- [requests/requests](https://github.com/requests/requests):Python HTTP Requests for Humans™ ✨🍰✨ http://python-requests.org
### Anaconda

专注于数据分析的Python发行版本，包含了conda、Python等190多个科学包及其依赖项。适用于企业级大数据分析的Python工具。其包含了720多个数据科学相关的开源包，在数据可视化、机器学习、深度学习等多方面都有涉及。不仅可以做数据分析，甚至可以用在大数据和人工智能领域。

conda 是开源包（packages）和虚拟环境（environment）的管理系统。

- packages 管理： 可以使用 conda 来安装、更新 、卸载工具包 ，并且它更关注于数据科学相关的工具包。在安装 anaconda 时就预先集成了像 Numpy、Scipy、 pandas、Scikit-learn 这些在数据分析中常用的包。另外值得一提的是，conda 并不仅仅管理Python的工具包，它也能安装非python的包。比如在新版的 Anaconda 中就可以安装R语言的集成开发环境 Rstudio。
- 虚拟环境管理： 在conda中可以建立多个虚拟环境，用于隔离不同项目所需的不同版本的工具包，以防止版本上的冲突。

#### 使用

- Anaconda Navigator ：用于管理工具包和环境的图形用户界面，后续涉及的众多管理命令也可以在 Navigator 中手工实现。
- Jupyter notebook ：基于web的交互式计算环境，可以编辑易于人们阅读的文档，用于展示数据分析的过程。
- qtconsole ：一个可执行 IPython 的仿终端图形界面程序，相比 Python Shell 界面，qtconsole 可以直接显示代码生成的图形，实现多行代码输入执行，以及内置许多有用的功能和函数。
- spyder ：一个使用Python语言、跨平台的、科学运算集成开发环境。

```shell
// 更改镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 
conda config --set show_channel_urls yes

echo 'export PATH="~/User/henry/anaconda/bin:$PATH"' >> ~/.zshrc // 添加环境变量
source ~/.zshrc
conda upgrade --all   //升级工具包
conda install numpy scipy pandas
conda install numpy=1.10   conda install -n python34 numpy
conda remove package_name
conda update package_name
conda list -n python34
conda  search search_term
conda update conda
conda update anaconda

conda create -n env_name  list of packages // 默认的环境是 root，你也可以创建一个新环境,-n 代表 name，env_name 是需要创建的环境名称，list of packages 则是列出在新环境中需要安装的工具包。
conda create -n py2 python=2.7 pandas
source activate env_name // 进入名为 env_name 的环境
source deactivate  // 退出当前环境
python --version //查看版本
conda env remove -n env_name  // 删除名为 env_name 的环境
conda env list // 显示所有的环境
conda env export > environment.yaml  // 分享代码的时候，同时也需要将运行环境分享给大家，执行如下命令可以将当前环境下的 package 信息存入名为 environment 的 YAML 文件中
conda env create -f environment.yaml //  用对方分享的 YAML 文件来创建一摸一样的运行环境。
```

#### Jupyter Notebook

[官网](http://jupyter.org/)

```shell
conda install jupyter notebook
pip install jupyter notebook

Anaconda，可以在其 Navigator 图形界面中点击打开 Notebook。
jupyter notebook
```

Notebook 文档是由一系列单元（Cell）构成，主要有两种形式的单元：

代码单元：这里是你编写代码的地方，通过按 Shift + Enter 运行代码，其结果显示在本单元下方。代码单元左边有 In [1]: 这样的序列标记，方便人们查看代码的执行次序。

Markdown 单元：在这里对文本进行编辑，采用 markdown 的语法规范，可以设置文本格式、插入链接、图片甚至数学公式。同样使用 Shift + Enter 运行 markdown 单元来显示格式化的文本。

- 编辑数学公式：LaTeX `$$ z = \frac{x}{y} $$`
- 幻灯片

#### IPython

[官网](https://ipython.org/)

### [pypy](http://pypy.org/)


### docker
- mkdir -p ~/python ~/python/myapp  myapp目录将映射为python容器配置的应用目录
- 创建Dockerfile

```
FROM buildpack-deps:jessie

# remove several traces of debian python
RUN apt-get purge -y python.*

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

# gpg: key F73C700D: public key "Larry Hastings <larry@hastings.org>" imported
ENV GPG_KEY 97FC712E4C024BBEA48A61ED3A5CA953F73C700D

ENV PYTHON_VERSION 3.5.1

# if this is called "PIP_VERSION", pip explodes with "ValueError: invalid truth value '<VERSION>'"
ENV PYTHON_PIP_VERSION 8.1.2

RUN set -ex \
        && curl -fSL "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" -o python.tar.xz \
        && curl -fSL "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" -o python.tar.xz.asc \
        && export GNUPGHOME="$(mktemp -d)" \
        && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" \
        && gpg --batch --verify python.tar.xz.asc python.tar.xz \
        && rm -r "$GNUPGHOME" python.tar.xz.asc \
        && mkdir -p /usr/src/python \
        && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
        && rm python.tar.xz \
        \
        && cd /usr/src/python \
        && ./configure --enable-shared --enable-unicode=ucs4 \
        && make -j$(nproc) \
        && make install \
        && ldconfig \
        && pip3 install --no-cache-dir --upgrade --ignore-installed pip==$PYTHON_PIP_VERSION \
        && find /usr/local -depth \
                \( \
                    \( -type d -a -name test -o -name tests \) \
                    -o \
                    \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
                \) -exec rm -rf '{}' + \
        && rm -rf /usr/src/python ~/.cache

# make some useful symlinks that are expected to exist
RUN cd /usr/local/bin \
        && ln -s easy_install-3.5 easy_install \
        && ln -s idle3 idle \
        && ln -s pydoc3 pydoc \
        && ln -s python3 python \
        && ln -s python3-config python-config

CMD ["python3"]
```

- docker build -t python:3.5 .
- docker run  -v $PWD/myapp:/usr/src/myapp  -w /usr/src/myapp python:3.5 python helloworld.py

## selenium

`python3 -m pip install selenium`

安装 chromedriver

## 参考

- [python/cpython](https://github.com/python/cpython):The Python programming language
- [donnemartin/data-science-ipython-notebooks](https://github.com/donnemartin/data-science-ipython-notebooks):Data science Python notebooks: Deep learning (TensorFlow, Theano, Caffe, Keras), scikit-learn, Kaggle, big data (Spark, Hadoop MapReduce, HDFS), matplotlib, pandas, NumPy, SciPy, Python essentials, AWS, and various command lines.
- [kennethreitz/python-guide](https://github.com/kennethreitz/python-guide):Python best practices guidebook, written for Humans. http://docs.python-guide.org
- [faif/python-patterns](https://github.com/faif/python-patterns):A collection of design patterns/idioms in Python
