# C++

## 学习

* 学好C++，一定要学习C++11，搞懂内存管理，
* 熟悉智能指针和RAII等基本内存管理原则，
* 搞懂虚函数和继承，函数重载与重写，
* 熟悉C++调试等
* 不要死抠语法细节
* 了解Big picture，从做项目中去掌握和理解C++的这些特性
* 看完基本的C++语法，类，继承之后就可以开始写代码了。遇到模板或者STL容器不懂的时候，再去针对性地阅读相关的章节和Google查找资料来学习

## 环境搭建

```sh
sudo apt install gcc g++ gdb

## sublime  C++.sublime-build
{
    "shell_cmd": "g++ \"${file}\" -o \"${file_path}/${file_base_name}\"",
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "working_dir": "${file_path}",
    "selector": "source.c, source.c++",

    "variants":
    [
        {
            "name": "Run",
            "shell_cmd": "g++ \"${file}\" -o \"${file_path}/${file_base_name}\" && \"${file_path}/${file_base_name}\""
        }
    ]
}

cc -v

# IDE
sudo apt intall kdevelop
```

## 变量

* 局部变量：函数内的作用域
    - 如果定义了与全局变量一致，比全局变量 优先级高
* 全局变量：函数外的变量
* {} 标志一个作用域
* 静态变量：程序运行期间分配固定的存储空间， `static`
    - 分配在一块静态存储区的内存，调用结束后,不会回收
* `extern`
    - 提前声明全局变量，避免 使用未声明变量报错
    - 多文件共享

## 结构体(struct)

* 由一系列具有相同类型或不同类型的数据构成的数据集合
* 每一个成员可以是一个基本数据类型或者又是一个构造类型
* 结构即是一种“构造”而成的数据类型， 那么在说明和使用之前必须先定义它，也就是构造它
* 作用
    - 封装一些属性来组成新的类型
* 大小与内存对齐
    - 各成员变量在存放的时候根据在结构中出现的顺序依次申请空间
    - 同时按照前面的数据结构对齐方式调整位置，空缺的字节会自动填充
    - 为了确保结构的大小为结构的字节边界数（即该结构中占用最大空间的类型所占用的字节数）的倍数，所以在为最后一个成员变量申请空间后，还会根据需要自动填充空缺的字节

## 数组

* 字符串是用字符数组来存储.系统自动分配 `\0` 表示字符串的结束
* 数组是指向数组第一个元素的指针，在指针上进行数学运算指向数组中的元素

## 指针

* `char *p = &c`:定义了一个指向char类型变量指针
* p：存放变量地址，做数学运算
    - *p++: a[i++]:先取指向的变量值 `(*p)` p =p+1
    - *p--: a[i--]
    - *--p: a[--i]：先运算，再取值
    - *++p: a[++i]
* &c 取地址操作
* `*p +1`: *p 取得指针所指向的变量值
* 生命时为指针标识符，使用时为取值操作

## 运算符

* short char 自动转换 int
* float 自动转换double

## 引用

* 方法在单独文件中声明，编译时需要加上该文件
* 使用 #include "max.c"

## 标准库STL

* 提供了丰富的算法库支持和各种容器
* C++ 标准库提供了包括最基础的标准输入输出iostrem、各种容器vector、set、string ，熟练掌握标准库
* queue
    - front():队列头部
    - pop():从头部开始
    - push();压人尾部
    - back():队列尾部
* stack
* priority_queue:二叉堆，最大（小）值先出
    - pop()：弹出栈顶元素（最大值）

## 标准化输入输出

* printf
    - d 十进制 5d 设定对齐长度
    - o 八进制
    - x 十六进制
    - u 无符号
    - c 字符
    - s 字符串
    - f 浮点
    - e 科学计数法
* scanf
    - 定义了输入格式
    -  一次输入多个变量：遇到 空格 制表符 enter 为变量结束

## 控制

* 分支
    - 关系运算符
    - 逻辑运算符
    - 条件运算符（三元）
    - switch
        + 没有break,会执行所以分支
        + 符合条件的作处理

## 编译

* 多个文件，必须有且只有一个main函数
* 预处理 Pre-Process：处理源文件中 #ifdef #include #define,生成中间文件`*.i`
    - #include <myinc.h> 在预装的库里查找 /usr/include，/usr/local/include，/usr/lib/gcc-lib/i386-linux/2.95.2/include /usr/include/c++/9
    - #include "myinc.h" 在当前目录内查找文件
* 编译 Compiling：输入中间文件，生成汇编语言文件 *.s
* 汇编 Asssembling:将汇编 转换回二进制机器代码
    - main 函数不是必须的
* 链接 Linking：将二进制机器代码文件生成可执行文件
* gcc 参数
    - -c 只编译，不链接
    - -g 产生调试器 gdb,用于对源代码调试
    - -O 优化编译、链接
    - -O2 更好的优化
    - -Wall 输出警告信息
    - -w 关闭警告信息

```sh
gcc -E file.c -o test.i # 预处理
gcc -S test.i -o test.s # 编译
gcc  -c test.s -o test.o # 汇编
gcc test.o -o test
gcc -o test test2.c test3.c test2.c
```

## 头文件与函数定义分离

* 函数声明和定义分离开来
* 加快编译速度:未修改的函数，公共框架和公共类编译生成静态库

## main函数中的参数

```sh
// 将输出保存到t.txt.错误保存到f.txt.从input.txt读入数据
./main.out 1>true.txt 2>false.txt < input.txt
```

## [细节](https://mp.weixin.qq.com/s/HLmZzFtNF9kVbIGS47E-BA)

* 尽量以const，enum，inline 替换 #define
    - #define 是不被视为语言的一部分，它在程序编译阶段中的预处理阶段的作用，就是做简单的替换
    - 遇到了编译错误，那么这个错误信息也许会提到 3.14 而不是 PI
    - 定义常量字符串，则必须要 const 两次，目的是为了防止指针所指内容和指针自身不能被改变     `const char* const myName = "小林coding";`
    - 对于单纯常量，最好以 const 对象或 enum 替换 #define
    - 对于形式函数的宏，最好改用 inline 函数替换 #define
    - #define 不重视作用域，所以对于 class 的专属常量，应避免使用宏定义 `const std::string myName("小林coding");`
* 尽可能使用 const:告诉编译器和其他程序员某值应该保持不变
    - 面对指针，可以指定指针自身、指针所指物，或两者都（或都不）是 const
    - 面对迭代器，你也指定迭代器自身或自迭代器所指物不可被改变
    - 希望迭代器所指的物不可被改动，需要的是 const_iterator（即声明一个 const T* 指针）

```c++
char myName[] = "小林coding";
char *p = myName;             // non-const pointer, non-const data 指针所指物是常量（不能改变 *p 的值）
const char* p = myName;       // non-const pointer, const data 表示指针自身是常量（不能改变 p 的值）
char* const p = myName;       // const pointer, non-const data
const char* const p = myName; // const pointer, const data 表示指针所指物和指针自身都是常量
```

## C++11新标准

* 新标准提供了解决现有问题更优雅、更 C++ 的实现。现行的大部分 C++ 软件还是 C++98 的标准，C++98 是 C++ 的第一个标准，经历这么多年的发展，从前你需要从Boost库（一个在 C++98 年代的准 C++ 标准）获得的对 C++ 的扩充支持的大部分功能已经纳入了 C++11 和甚至 C++2X 更新的标准当中，与时俱进拿起更先进的生产工具，工具就是效率

## 面试

* 指针和引用的区别

* define和const
* 内联函数和define
* c++内存管理
* 栈和堆区别，全局变量和局部变量
* c++多态，虚函数，纯虚函数
* 多态的好处
* 数据库索引，给一个语句问有没有用到索引，底层怎么实现的
* B树和B+树
* 哈希冲突
* 说一说常见的排序算法和时间，空间复杂度
* TCP,UDP,可靠传输，网络什么时候拥塞
* 为什么要内存对齐
* 非对称加密和对称加密
* static变量和局部变量知道不
* 内存溢出
* 服务器什么操作会不
* c++用的多吗
* 想做什么岗位
* linux命令会吗
* epoll和select
* sed和grep知道不
* awk
* 你会gdb调试？说一下gdb调试的原理
* 你用过git，讲一下原理
* 你熟悉哪些linux命令，回答了解复制之类的，然后问，cpu的原理你讲一下
* https1.1和2.0的区别，答出来了，为什么，怎么实现的？
* c++11有哪些特性，你实现一下shared_ptr
* tcp为什么可靠？tcp重传的时间怎么设的，（一个消息都得不到ACK）
* 多线程怎么进行调度
* 用过mysql吗，说一下B+树
* 这是你的笔试题啊，考察一下你的算法吧，这个第三题你做错了，有思路吗，说没有，那你现在想一下
* memcpy写一下
* strcpy写一下
* 了解c++多态吗，那你用c实现一下。


* 擅长的语言（C语言，C++），对C++的了解程度
* Linux的项目平台经验多吗？
* malloc和new分配内存的区别
* malloc内部的实现原理
* malloc能够分配的最大内存空间（32位）（提到了段），如果申请了2G的内存，会立即与物理地址对应吗，如果不会，往里面写数据的时候
* 否会产生缺页中断
* 如何查看段的范围和大小
* elf目标可执行文件的组成部分，elf文件中的段跟运行时的段有什么区别
* 如何装载目标文件到内存当中
* 缺页中断的处理过程
* 提到了换页换出的时候会产生缺页中断，反问是否一定是换页产生的吗？上面提到的未分配空间呢？
* 这种缺页中断在系统和硬件中是由哪些CPU，寄存器参与的。
* 提到了MMU，CR3寄存器
* 为了加快页表的转换，会使用一些什么样的硬件和软件
* 了解大页内存吗？它是什么概念，有什么优点和缺点。
* 优点：减少页表
* 对于汇编这部分了解多吗？C语言的函数调用在汇编的角度是怎么实现的？
* 提到了ebp，esp函数栈，jmp跳转
* Linux库函数memcpy，能不能想出比较高效的内存拷贝方式。除了按字节拷贝还有没有性能更好的方法。
* Linux上运行的进程的CPU有什么组成部分，整体的CPU占用和每一块的CPU的占用。怎么用top去看一个进程的CPU占用的组成部分。（是
* 是做的性能优化这部分的工作比较少）
* C++ STL里面有很多性能优化相关的类，这个你了解吗？STL的string类本身有多大，如何保存字符串的？vector如何动态扩展空间？
* 提到了size()和capacity()
* 挑一个研究的最深的技术点。挑自己最擅长的说，比如说网络编程、系统内核啊等等
* 乐观锁和悲观锁的区别
* 提到了CAS
* 问到了CAS的应用场景，CAS允许有短暂的访问迟滞吗？
* CAS为了实现锁的原语，在Linux系统上是怎么去实现的？
* 谈的是RING中的源码，使用多个struct，但是他说没有谈到点上，想问的是背后原理（汇编也好，x86架构上也好）（可能是单句汇编语言
* 或者是总线锁）
* volatile关键字的作用？主要是为了解决什么问题？为了防止编译器进行哪种方式的优化？
* 为了防止编译器优化，最核心的是做了什么优化，怎么理解直接去读这个值
* 缓存是一个什么样的硬件？
* 寄存器也算是缓存的一部分吗？
* CPU访问寄存器、访问缓存、访问内存哪个快？访问的时间周期是多少？快多少倍？
* 本科、研究生、实习做的项目和事情中哪个事情比较满意，能够体现自己的能力的？
* 技术也好、做事情的方式也好的优势和劣势？

* 为什么不用CNN，用LSTM
* LSTM为什么可以缓解梯度消失
* 什么是梯度消失和梯度爆炸
* 为什么要提取时序信息
* 说一下RNN和CNN
* 你说一下虚指针
* 写一下单例模式
* 别的进程可以访问这个进程的创建的单例模式的实例吗
* 你说一下内存泄漏
* 有几个虚函数表
* while(1)死循环
* attention机制
* 说一下继承中的构造函数和析构函数
* 野指针讲一下
* 你学过哪些课程，那你说说红黑树
* 你说一下平衡二叉树怎么插入一个结点
* TCP怎么重传
* 共享内存为什么可以实现进程通信
* 每个进程都有自己的内存，为什么可以访问共享内存
* 你知道希尔排序吗，比直接插入排序快吗，为什么，时间复杂度平均多少
* 单链表快排
* 写一下反转单链表

## 教程

* [changkun/modern-cpp-tutorial](https://github.com/changkun/modern-cpp-tutorial):📚 C++11/14/17 On the Fly https://changkun.de/modern-cpp/

## 图书

* 《The C++ Programming Language》
* **《C++ Primer》**
* 《Effective C++》：写过几万行C++代码之后，再去阅读会更好。而且推荐每年都至少读一遍。
* 《More Effective C++（中文版）》
* 《C++ 标准程序库》
* 《STL源码剖析》
* 《深度探索C++对象模型》
* Think in C++
* Modern C++ Tutorial
    - [changkun / modern-cpp-tutorial](https://github.com/changkun/modern-cpp-tutorial)
* 《深入理解C++11》

## 工具

* IDE
    - [Code::Blocks](http://www.codeblocks.org) <https://launchpad.net/~codeblocks-devs/+archive/ubuntu/release>
        + `sudo add-apt-repository ppa:codeblocks-devs/release`
        + sudo apt-get update
        + `sudo apt-get install codeblocks codeblocks-contrib`
    - Qtcreator
* 队列
    - [cameron314/concurrentqueue](https://github.com/cameron314/concurrentqueue):A fast multi-producer, multi-consumer lock-free concurrent queue for C++11
* [Tencent/phxpaxos](https://github.com/Tencent/phxpaxos)：The Paxos library implemented in C++ that has been used in the WeChat production environment.
* JSON
    - [nlohmann / json](https://github.com/nlohmann/json):JSON for Modern C++ https://nlohmann.github.io/json/
    - [Tencent/rapidjson](https://github.com/Tencent/rapidjson):A fast JSON parser/generator for C++ with both SAX/DOM style API http://rapidjson.org/
* [Tencent/libco](https://github.com/Tencent/libco)libco is a coroutine library which is widely used in wechat back-end service.
* [envoyproxy/envoy](https://github.com/envoyproxy/envoy):C++ front/service proxy https://www.envoyproxy.io
* [lupoDharkael/flameshot](https://github.com/lupoDharkael/flameshot):Powerful yet simple to use screenshot software
* [onqtam/doctest](https://github.com/onqtam/doctest):The fastest feature-rich C++11 single-header testing framework for unit tests and TDD http://bit.ly/doctest-docs
* package manager
    - [Microsoft/vcpkg](https://github.com/Microsoft/vcpkg):C++ Library Manager for Windows, Linux, and MacOS
* [catchorg/Catch2](https://github.com/catchorg/Catch2):A modern, C++-native, header-only, test framework for unit-tests, TDD and BDD - using C++11, C++14, C++17 and later (or C++03 on the Catch1.x branch) https://discord.gg/4CWS9zD
* [Boost.Hana](https://www.boost.org/doc/libs/1_61_0/libs/hana/doc/html/index.html):Hana is a header-only library for C++ metaprogramming suited for computations on both types and values
* [google / benchmark](https://github.com/google/benchmark):A microbenchmark support library

## 参考

* [C/C++ 开源库及示例代码](https://github.com/programthink/opensource/blob/master/libs/cpp.wiki)
* [cppreference](https://en.cppreference.com/)
* Guidelines
    - [isocpp/CppCoreGuidelines](https://github.com/isocpp/CppCoreGuidelines):The C++ Core Guidelines are a set of tried-and-true guidelines, rules, and best practices about coding in C++http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines
    - [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
* [fffaraz/awesome-cpp](https://github.com/fffaraz/awesome-cpp):A curated list of awesome C++ (or C) frameworks, libraries, resources, and shiny things. Inspired by awesome-... stuff. http://fffaraz.github.io/awesome-cpp/
* [Awesome C/C++](https://fffaraz.github.io/awesome-cpp/)：一系列优秀的`C/C++`框架、库和资源
* [huihut/interview](https://github.com/huihut/interview):📚 C/C++面试知识总结
* Qt
    - [Awesome Qt](https://github.com/fffaraz/awesome-qt)：一系列优秀的`Qt`库和资源
    - [3rd-party-applications](https://github.com/Razor-qt/razor-qt/wiki/3rd-party-applications)：一系列优秀的`Qt`第三方程序
