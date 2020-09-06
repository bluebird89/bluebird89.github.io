# 编译原理

利用现成的工具去生成/操作一个抽象语法树（AST），甚至可以会写一个DSL（领域特定语言）。 所以得理解词法分析、语法分析、语义分析，中间代码生成，代码优化这个基本编译的过程。学习了编译与原理，会对语言的一些设计有更深的理解，比如LISP。

* 指令系统
    - 精简指令集计算机（RISC）:供了最小的机器指令集，计算机效率高速度快且制造成本低
    - 复杂指令集计算机(CISC):提供了强大丰富的指令集，能更方便实现复杂的软件
    - 三类
        + 数据传输类指令用于将数据从一个地方移动到另一个地方。比如将主存单元的内容加载到寄存器的LOAD指令，反之将寄存器的内容保存到主存的STORE指令。此外，CPU与其它设备（键盘、鼠标、打印机、显示器、磁盘等）进行通信的指令被称为I/O指令。
        + 算术/逻辑类指令用于让控制单元请求在算术/逻辑单元内执行运算。这些运算包括算术、与、或、异或和位移等。
        + 控制类指令用于指导程序执行。比如转移（JUMP）指令，它包括无条件转移和条件转移
* Compilers: Principles,Techniques,and Tools 编译原理技术和工具 Alfred V.Aho,Ravi Sethi,Jeffrey D.Ullman
* Modern Compiler Implementation in C  Andrew W.Appel,with Jens Palsberg  现代编译原理-C语言描述
* Advanced Compiler Design and Implementation  Steven S.Muchnick  高级编译器设计与实现




## 工具

* [Compiler Expolorer](https://godbolt.org/)

## 参考

* [jamiebuilds / the-super-tiny-compiler](https://github.com/jamiebuilds/the-super-tiny-compiler):snowman Possibly the smallest compiler ever https://git.io/compiler