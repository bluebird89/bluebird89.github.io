# Computer 组成原理

* 最原始部件——晶体管。晶体管是一种半导体材料，其最重要的作用就是半导：可以通过电流的变化，实现电路的切换。比如计算机最基础的与或非运算，都可以通过晶体管组成的电子元件实现。而通过晶体管的电位差不同，就可以体现"二进制数据"，即0和1。再加上电容和电阻，就能把这种二进制数据临时保存起来。综合这些特性，大牛们发现把晶体管用作精密的数学计算，可以极大的提高运算的效率。比如有2个电容，分别是充满电和没有电，对他们同时释放电信号，电容就会把其中的电子放出来，经过特定的逻辑电路，如与门，得到了0的结果。要计算1+1，实际上也是类似的原理。先设计一个加法电路，把若干电容组合成的"数字"流过这个电路，把结果存入目标电容，就得到了结果。大规模的复杂运算以此类推。最早期的计算机真的就是用许多结晶体管实现的复杂电路结构，通过控制输入电流得到希望的输出结果。后来人们发现，这种计算可以用某些形式抽象成多种指令，不用针对每次计算设计复杂的电路，只要调用指令就可以实现任何一种计算组合，于是诞生了cpu。只有cpu，每次都要自己配置输入信号，实在太痛苦，就做了纸带输入给计算机。后来又发现纸带还是很麻烦，于是发明了输入终端和对应的存储设备。后来又发现很多数据要临时保存起来，供连续计算使用，于是发明了内存

* 形式语言与自动机

* CPU有哪些指令，如何执行这些指令，如果实现数组，结构体，函数调用，这就涉及到汇编的知识。像原码，反码，补码，定点数、浮点数的表示和运算也是编程中必备的知识，几乎每种语言都要涉及
* CPU中的缓存，缓存一致性协议，DMA的异步思想都会在应用层中有所体现

## 冯·诺依曼体系结构

* 计算机处理的数据和指令一律用二进制数表示
* 顺序执行程序:计算机运行过程中，把要执行的程序和处理的数据首先存入主存储器（内存），计算机执行程序时，将自动地并按顺序从主存储器中取出指令一条一条地执行，这一概念称作顺序执行程序。
* 计算机硬件由运算器、控制器、存储器、输入设备和输出设备五大部分组成。

## 概念

* 机器数
  - 计算机中符号和数字一样,都必须用二进制数串来表示,因此,正负号也必须用0、1来表示。用最高位0表示正、1表示负
  - 这种正负号数字化的机内表示形式就称为“机器数”,而相应的机器外部用正负号表示的数称为“真值”,将一个真值表示成二进制字串的机器数的过程就称为编码。
* 原码就是符号位加上真值的绝对值, 即用第一位表示符号, 其余位表示值
* 反码
  - 正数的反码是其本身
  - 负数的反码是在其原码的基础上, 符号位不变，其余各个位取反.
* 补码
  - 正数的补码就是其本身
  - 负数的补码是在其原码的基础上, 符号位不变, 其余各位取反, 最后+1
* 定点数与浮点数
  - 定点数是小数点固定的数。在计算机中没有专门表示小数点的位，小数点的位置是约定默认的。一般固定在机器数的最低位之后，或是固定在符号位之后。前者称为定点纯整数，后者称为定点纯小数。
  - 定点数表示法简单直观，但是数值表示的范围太小，运算时容易产生溢出。
  - 浮点数是小数点的位置可以变动的数。为增大数值表示范围，防止溢出，采用浮点数表示法。浮点表示法类似于十进制中的科学计数法。
    + 把浮点数分成阶码和尾数两部分来表示，其中阶码一般用补码定点整数表示，尾数一般用补码或原码定点小数表示。为保证不损失有效数字，对尾数进行规格化处理，也就是平时所说的科学记数法，即保证尾数的最高位为1，实际数值通过阶码进行调整
    + 阶符表示指数的符号位、阶码表示幂次、数符表示尾数的符号位、尾数表示规格化后的小数值。
* 位："位(bit)"是电子计算机中最小的数据单位。每一位的状态只能是0或1。
* 字节：8个二进制位构成1个"字节(Byte)"，它是存储空间的基本计量单位。1个字节可以储存1个英文字母或者半个汉字，换句话说，1个汉字占据2个字节的存储空间。
* 字："字"由若干个字节构成，字的位数叫做字长，不同档次的机器有不同的字长。例如一台8位机，它的1个字就等于1个字节，字长为8位。如果是一台16位机，那么，它的1个字就由2个字节构成，字长为16位。字是计算机进行数据处理和运算的单位。
* 字节序
  - 字节顺序是指占内存多于一个字节类型的数据在内存中的存放顺序
  - Little Endian 小端字节序:指低字节数据存放在内存低地址处，高字节数据存放在内存高地址处；
  - Big Endian 大端字节序 高字节数据存放在低地址处，低字节数据存放在高地址处。
  - 基于X86平台的PC机是小端字节序的，而有的嵌入式平台则是大端字节序的。
  - 所有网络协议也都是采用big endian的方式来传输数据的。所以有时也会把big endian方式称之为网络字节序。
* 字节对齐
  - 在访问特定类型变量的时候经常在特定的内存地址访问，这就需要各种类型数据按照一定的规则在空间上排列，而不是顺序的一个接一个的排放
  - 最根本的原因是效率问题，字节对齐能提⾼存取数据的速度
  - 原则
    + 数据成员对齐规则：结构(struct)(或联合(union))的数据成员，第一个数据成员放在 offset 为0的地方，以后每个数据成员存储的起始位置要从该成员大小或者成员的子成员大小（只要该成员有子成员，比如说是数组，结构体等）的整数倍开始(比如int在32位机为4字节,则要从4的整数倍地址开始存储。
    + 结构体作为成员:如果一个结构里有某些结构体成员,则结构体成员要从其内部最大元素大小的整数倍地址开始存储。(struct a里存有struct b,b里有char,int ,double等元素,那b应该从8的整数倍开始存储。)
    + 收尾工作:结构体的总大小，也就是sizeof的结果，必须是其内部最大成员的整数倍，不足的要补齐。

```
[+1] = [00000001]原 = [00000001]反 = [00000001]补
[-1] = [10000001]原 = [11111110]反 = [11111111]补

N = 尾数×基数阶码（指数）

Big Endian
低地址                                            高地址
---------------------------------------------------->
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     12     |      34    |     56      |     78    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

Little Endian
低地址                                            高地址
---------------------------------------------------->
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     78     |      56    |     34      |     12    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

## 启动 Boot

* 主板:管理所有设备
* 操作系统:各种资源都能得到良好组织，更快访问。用户界面更好看，使用更方便，功能更强大
  - 接管主板对于系统资源的管理，加入中间层——驱动程序
    + 进程管理
    + 存储管理
    + 输入/出设备管理
    + 网络管理
    + 安全管理
  * 另一方面又充分发挥了人机交互的接口——gui界面，成为了计算机必不可少的组成部分
* 流程
  - 通过bios引导，即作为应用程序开始运行。程序本质上就是在cpu上运行种种指令，比如操作系统需要把硬盘上的模块放入内存，实际上就是运行了一系列复杂的cpu指令，cpu指令通过主板bus（实际上就是传递指令的电路）发送指令给硬盘（比如从哪个扇区偏移多少读多少数据），硬盘再通过芯片组转动磁头，把数据读到缓存中，完成后给cpu发送一个信号（即中断），cpu收到这个信号，就在寄存器中寻址该信号对应的地址（即我们说的中断向量表），运行该地址中的指令，发现该指令是发送拷贝指令给主板芯片组，主板就会在cpu的指导下不断的发送信号，告诉硬盘缓存放电，再把接收的电信号存到指定的内存位置去，如此反复，直到完成cpu的一系列指令为止
  - 通过种种cpu指令，实现自身的所有功能。当然这些指令也不是一条条写进去的，而是通过编程语言完成人类较容易识别的逻辑，然后再通过编译器把这些逻辑翻译成cpu指令，这就涉及编译原理的东西了。既然操作系统对硬件的访问都是通过cpu指令来完成的，那为什么大家都感觉是操作掌管了硬件呢？这就涉及操作系统最本质的功能之一：对系统资源的管控了。
* 运行的所有程序，实际上都是操作系统运行。操作系统背后进行了很多的工作
  - 如虚拟地址空间的分配，cpu分时调度，硬件中断信号的响应等。这样对于硬件资源的访问，也是通过操作系统安排的
  - 通过把短时间内硬盘读写合并成顺序的方式，以提高磁头的利用率，降低磁头转向的时间
  - 对内存地址的访问也是由操作系统管控的，某个程序中的内存地址具体落到内存条的哪个位置，还是硬盘中的虚拟内存，就看操作系统的心情了。至此，操作系统和硬件的交互也介绍的差不多了

## 硬件 Hardware

* BIOS with [MBR](https://wiki.archlinux.org/title/MBR "MBR") 
	* 主引导记录 Master Boot Record MBR 任何硬盘或软盘的第一扇区中的信息，用于标识操作系统的放置方式和位置，以便可以将其加载到计算机的主存储器或随机存取存储器中
* UEFI with [GPT](https://wiki.archlinux.org/title/GPT "GPT")
* 块设备(block devices) 一个能存储固定大小块信息的设备，它支持以固定大小的块，扇区或群集读取和（可选）写入数据。每个块都有自己的物理地址。通常块的大小在 512 - 65536 之间。所有传输的信息都会以连续的块为单位。块设备的基本特征是每个块都较为对立，能够独立的进行读写。常见的块设备有 硬盘、蓝光光盘、USB 盘
* 字符设备(character devices)：另一类 I/O 设备是字符设备。字符设备以字符为单位发送或接收一个字符流，而不考虑任何块结构。字符设备是不可寻址的，也没有任何寻道操作。常见的字符设备有 打印机、网络设备、鼠标、以及大多数与磁盘不同的设备
* 设备控制器(device controller)：设备控制器是处理 CPU 传入信号和传出信号的系统。设备通过插头和插座连接到计算机，并且插座连接到设备控制器
* 显卡(Video card)，是个人电脑最基本组成部分之一，用途是将计算机系统所需要的显示信息进行转换驱动显示器，并向显示器提供逐行或隔行扫描信号，控制显示器的正确显示，是连接显示器和个人电脑主板的重要组件，是人机对话的重要设备之一
* 挂载(mounting) ：挂载是指操作系统会让存储在硬盘、CD-ROM 等资源设备上的目录和文件，通过文件系统能够让用户访问的过程
* RAID Redundant Array of Inexpensive Disks ，廉价磁盘或驱动器的冗余阵列，它是一种数据存储虚拟化的技术，将多个物理磁盘驱动器组件组合成一个或多个逻辑单元，以实现数据冗余，改善性能
* 可抢占资源(preemptable resource)：可以从拥有它的进程中抢占而并不会产生任何副作用
* 不可抢占资源(nonpreemptable resource)：与可抢占资源相反，如果资源被抢占后，会导致进程或任务出错
* 触摸屏
  - 电阻式触摸屏(Resistive touchscreens)：电阻式触摸屏基于施加到屏幕上的压力来工作。电阻屏由许多层组成。当按下屏幕时，外部的后面板将被推到下一层，下一层会感觉到施加了压力并记录了输入。电阻式触摸屏用途广泛，可以用手指，指甲，手写笔或任何其他物体进行操作
  - 电容式触摸屏(capacitive touchscreen)：通过感应物体（通常是指尖上的皮肤）的导电特性来工作。手机或智能手机上的电容屏通常具有玻璃表面，并且不依赖压力。当涉及到手势（如滑动和捏合）时，它比电阻式屏幕更具响应性。电容式触摸屏只能用手指触摸，而不能用普通的手写笔，手套或大多数其他物体来响应
* GDI (Graphics Device Interface)：图形接口，是微软视窗系统提供的应用程序接口，也是其用来表征图形对象、将图形对象传送给诸如显示器、打印机之类输出设备的核心组件
* 设备上下文(device context)：设备上下文是 Windows 数据结构，其中包含有关设备（例如显示器或打印机）的图形属性的信息。所有绘图调用都是通过设备上下文对象进行的，该对象封装了用于绘制线条，形状和文本的 Windows API。设备上下文可用于绘制到屏幕，打印机或图元文件
* 系统检查点(system checkpointed)：操作系统（OS）的可启动实例。检查点是计算机在特定时间点的快照
* 沙盒(sandboxing)一种软件管理策略，可将应用程序与关键系统资源和其他程序隔离。它提供了一层额外的安全保护，可防止恶意软件或有害应用程序对你的系统造成负面影响

## CPU Central Processing Unit 处理器

* 计算机中控制数据操控的电路
* AMD 3600，6核心12线程（超线程）
* 内部封装了1个或者多个物理核，物理核有独立的各级缓存和电路结构，如果只有1个物理核心就是单核CPU，有多个物理核心就是多核CPU`物理核心数=总CPU数*单CPU中物理核心数`
  - 物理 CPU 核心数：真正插在物理插槽上 CPU 的核心数,每个物理核下的逻辑核共用 L1/L2 Cache
  - 逻辑 CPU 核心数：结合 CPU 多核以及超线程技术得到的 CPU 核心数，最终核心数以逻辑 CPU 核心数为准
* 算术/逻辑单元 ALU:处理算数和逻辑运算
* 控制单元:协调机器活动,操作主存中的数据
* 寄存器单元:用来暂存指令、数据和地址
  - 通用寄存器:用于临时存放CPU正在使用的数据
  - 专用寄存器:用于CPU专有用途，比如指令寄存器和程序计数器
* CPU将主存的指令加载进来解码并执行，其中涉及两个重要寄存器
  - 指令寄存器与程序计数器。指令寄存器用于存储正在执行的指令
  - 程序计数器则保持下一个待执行的指令地址
* 阶段
  - 取指令阶段是将内存中的指令读取到 CPU 中寄存器的过程，程序寄存器用于存储下一条指令所在的地址
  - 指令译码阶段，在取指令完成后，立马进入指令译码阶段，在指令译码阶段，指令译码器按照预定的指令格式，对取回的指令进行拆分和解释，识别区分出不同的指令类别以及各种获取操作数的方法。
  - 执行指令阶段，译码完成后，就需要执行这一条指令了，此阶段的任务是完成指令所规定的各种操作，具体实现指令的功能。
  - 访问取数阶段，根据指令的需要，有可能需要从内存中提取数据，此阶段的任务是：根据指令地址码，得到操作数在主存中的地址，并从主存中读取该操作数用于运算。
  - 结果写回阶段，作为最后一个阶段，结果写回（Write Back，WB）阶段把执行指令阶段的运行结果数据“写回”到某种存储形式：结果数据经常被写到 CPU 的内部寄存器中，以便被后续的指令快速地存取；
* CPU向主存请求加载程序计数器指定的地址的指令，将其存放到指令寄存器中，加载后将程序计数器的值加2（假如指令长度为2个字节）
* 与其他设备的通信一般通过控制器来实现，控制器可能在主板上，也可能以电路板形式插到主板.现在随着通用串行总线（USB）成为通用的标准，很多外设都可以直接用USB控制器作为通信接口。每个控制器都连接在总线上，通过总线进行通信
* 直接存储器存取（DMA）是一种提升外设通信性能的措施，CPU并非总是需要使用总线，在总线空闲的时间里控制器能够充分利用起来。因为控制器都与总线相连接，而控制器又有执行指令的能力，所以可以将CPU的一些工作分给控制器来完成。比如在磁盘中检索数据时，CPU可以将告知控制器，然后由控制器找到数据并放到主存上，期间CPU可以去执行其他任务。这样能节省CPU资源。不过DMA会使总线通信更加复杂，而且会导致总线竞争问题。总线瓶颈源自冯诺依曼体系结构
* CPU 架构 CPU architecture:不同 CPU 设计实现.不同 CPU 架构有不同的指令集，彼此不通用，导致运行在上面的软件也不兼容，必须重新编译
  - x86:性能好，但是耗电多、电压高，主要用于桌面电脑和服务器，生产厂商为 Intel 公司和 AMD 公司
  - ARM:耗电小、电压低，但是单核性能不如 x86，主要用于移动设备。商业模式是授权制。英国的 ARM 公司出售指令集的授权，购买授权的公司可以基于公版的设计，开发自己的 ARM 芯片。高通、三星、华为、苹果等公司的芯片，都属于这个模式
* 超线程是intel于2002年发布的一种技术，全名为Hyper-Threading，简写为HT技术，超线程技术最初只是应用于至强系列处理器中，之后陆续应用在奔腾系列中并将技术主流化，业界对于HT的评价不一，但是官方并未放弃超线程技术
  - HT技术可使处理器中的1颗物理核，如同2颗物理核那样发挥作用，从而提高了系统的整体性能，但是肯定也不会真的像2颗物理核那样，要不然就违背物理规律了，只是说借助于某些技术将1颗物理核的性能发挥地更好而已
  - `开启HT: 逻辑核心数=总CPU数*单CPU中物理核心数*2`
* 多处理器架构
  - 对称多处理器结构 SMP Symmetric Multi-Processor:指多个CPU对称平等，共享相同的物理内存/IO等资源，因此SMP结构属于一致存储器访问结构 UMA
    + 共享模式下所有CPU平等地使用资源，模式简单，在CPU数量不多时效率很不错，但是优点也可能变为拦路虎。
    + 试想一种场景如果在SMP模式下为了提高服务器的处理能力，水平扩展了CPU数量，这些CPU通过相同的总线访问内存。随着CPU数量的增加，相同内存地址访问冲突将明显增加，间接造成了CPU资源浪费，相关实验证明，SMP服务器最好的情况是2-4个CPU
  - 非一致存储访问结构 NUMA Non-Uniform Memory Access:
    + 和SMP架构的显著区别在于是否是一致对等访问内存
    + 有多个 CPU 模块，每个 CPU 模块由多个 CPU组成，每个CPU模块具有独立的本地内存Local-Memory、 I/O等资源，可以将CPU模块称为Node
    + Node之间可以通过互联模块进行数据交互，因此每个 CPU 模块仍然可以访问整个系统的内存，但是此时的内存有本地和外部之分了，访问速度自然也就不一样
    + 访问CPU模块的本地内存将远远快于访问其他CPU模块内存，在明确这种架构带来的内存访问差异后，我们在实际开发应用程序时需要尽量减少不同 CPU 模块之间的信息交互
    + 缺陷，由于访问远地内存的延时远远超过本地内存，当 CPU 数量增加时，系统性能无法线性增加，换句话说增加1倍的CPU数量并不能获得1倍的性能提升，因此仍然存在扩展限制区
  - 海量并行处理结构 MPP Massive Parallel Processing:由多个 SMP 服务器通过一定的节点互联网络进行连接，完成相同的任务，可以看作是SMP的水平扩展
    + 多个 SMP 服务器是一种完全无共享Share Nothing)结构，因而扩展能力最好，典型的就是刀片服务器
* 缓存基本上来说就是把后面的数据加载到离自己近的地方，对于CPU来说,一块一块的加载的，对于这样的一块一块的数据单位，术语叫“Cache Line”，一般来说，一个主流的CPU的Cache Line 是 64 Bytes.64Bytes也就是16个32位的整型，这就是CPU从内存中捞数据上来的最小数据单位
* 缓存需要把内存里的数据放到放进来，英文叫 CPU Associativity。Cache的数据放置的策略决定了内存中的数据块会拷贝到CPU Cache中的哪个位置上，因为Cache的大小远远小于内存，所以，需要有一种地址关联的算法，能够让内存中的数据可以被映射到Cache中来。这个有点像内存地址从逻辑地址向物理地址映射的方法，但不完全一样
  - 任何一个内存地址的数据可以被缓存在任何一个Cache Line里，这种方法是最灵活的，但是，如果要知道一个内存是否存在于Cache中,就需要进行O(n)复杂度的Cache遍历，这是很没有效率的
  - 为了降低缓存搜索算法，需要使用像Hash Table这样的数据结构，最简单的hash table就是做“求模运算”,比如：L1 Cache有512个Cache Line，公式：`（内存地址 mod 512）* 64` 就可以直接找到所在的Cache地址的偏移了。但是，这样的方式需要程序对内存地址的访问要非常地平均，不然冲突就会非常严重。这成了一种非常理想的情况了
  - 为了避免上述两种方案的问题，于是就要容忍一定的hash冲突，也就出现了 N-Way 关联。也就是把连续的N个Cache Line绑成一组，然后，先把找到相关的组，然后再在这个组内找到相关的Cache Line。这叫 Set Associativity
* CPU缓存:新CPU会有三级内存（L1，L2，L3）,L1/L2大小基本上也就是KB级别的，L3会是MB级别的
  - L1缓分成两种，一种是指令缓存，一种是数据缓存。L2缓存和L3缓存不分指令和数据。
  - L1和L2缓存在每一个CPU核中，L3则是所有CPU核心共享的内存。
  - L1、L2、L3的越离CPU近就越小，速度也越快，越离CPU远，速度也越慢。
  - L1 存取速度：4 个CPU时钟周期
  - L2 存取速度： 11 个CPU时钟周期
  - L3 存取速度：39 个CPU时钟周期
  - RAM内存存取速度：107 个CPU时钟周期
  - L3，多核共享
  - 三层考虑：
    + 物理速度，如果要更大的容量就需要更多的晶体管，除了芯片的体积会变大，更重要的是大量的晶体管会导致速度下降，因为访问速度和要访问的晶体管所在的位置成反比，也就是当信号路径变长时，通信速度会变慢。这部分是物理问题
    + 多核技术中，数据的状态需要在多个CPU中进行同步，并且，可以看到，cache和RAM的速度差距太大，所以，多级不同尺寸的缓存有利于提高整体的性能

```
# Java 获取CPU核心数
Runtime.getRuntime().availableProcessors()//获取逻辑核心数，如6核心12线程，那么返回的是12

# Linux 获取CPU核心数
# 总核数 = 物理CPU个数 X 每颗物理CPU的核数
# 总逻辑CPU数 = 物理CPU个数 X 每颗物理CPU的核数 X 超线程数

# 查看物理CPU个数
cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l

# 查看每个物理CPU中core的个数(即核数)
cat /proc/cpuinfo| grep "cpu cores"| uniq

# 查看逻辑CPU的个数
cat /proc/cpuinfo| grep "processor"| wc -l
```

### 局部性原理

* CPU 与内存之间往往集成了挺多层级的缓存，这些缓存越接近CPU，速度越快，所以如果能提前把内存中的数据加载到如下图中的 L1, L2, L3 缓存中，那么下一次 CPU 取数的话直接从这些缓存里取即可，能让CPU执行速度加快
* 当某个元素被用到的时候，那么这个元素地址附近的的元素会被提前加载到 L1,L2,L3 缓存中,让内存一次性把目标区域附近的数据一起给cpu，存在这块区域，后面在需要用到的时候就先去这里找，找不到再去找内存要
* 无论是内存还是磁盘，操作系统都是按页的大小进行读取的（页大小通常为 4 kb），磁盘每次读取都会预读，会提前将连续的数据读入内存中，这样就避免了多次 IO
* 乱序执行：在等待的时间里把后续指令需要的数据（或者不依赖前者的操作）提前处理到缓存中来
  - 分支预测：遇到分支跳转时，按照之前的经验，如果某个分支经常被执行，那后续再去这个分支的概率一定很大，那这样咱们预测后面会去到这个分支，就提前把这个分支后面指令能做的工作先做了

### 并发

* 多核心：可以同时做多件事，互不打扰
* 执行线程数大于核心数，需要通过操作系统的调度。操作系统给每个线程分配CPU时间片资源，然后不停的切换，从而实现“并行”执行的效果
* 切换会伴随着寄存器数据更新，内存页表更新等操作 。虽然一次切换的代价和I/O操作比起来微不足道，但如果线程过多，线程切换的过于频繁，甚至在单位时间内切换的耗时已经大于程序执行的时间，就会导致CPU资源过多的浪费在上下文切换上，而不是在执行程序，得不偿失
* I/O操作，可能是读写文件，网络收发报文等，这些 I/O 操作在进行时时需要等待反馈的。比如网络读写时，需要等待报文发送或者接收到，在这个等待过程中，线程是等待状态，CPU没有工作。此时操作系统就会调度CPU去执行其他线程的指令，这样就完美利用了CPU这段空闲期，提高了CPU的利用率。
  - 当线程中有 I/O 等操作不占用CPU资源时，操作系统可以调度CPU可以同时执行更多的线程。
* 一个极端的线程（不停执行“计算”型操作时），就可以把单个核心的利用率跑满，多核心CPU最多只能同时执行等于核心数的“极端”线程数
* 如果每个线程都这么“极端”，且同时执行的线程数超过核心数，会导致不必要的切换，造成负载过高，只会让执行更慢
* I/O 等暂停类操作时，CPU处于空闲状态，操作系统调度CPU执行其他线程，可以提高CPU利用率，同时执行更多的线程
* I/O 事件的频率频率越高，或者等待/暂停时间越长，CPU的空闲时间也就更长，利用率越低，操作系统可以调度CPU执行更多的线程

## 内存 Memory

* 程序与 CPU 进行沟通的桥梁,程序只能在内存中运行
* 一个个电容所代表的0和1 ，由于这些电容不能持久地保持电荷，得定期地去刷新，如果不及时刷新，那些0和1的数据就会丢失
* 最小的一个格子就是一个bit ，只能存储0和1。8个bit 称为一个字节(Byte) 0～255 4个byte= 1 word
* 次序：大端（从左到右） 小端（从右到左）
* 编译器：允许用变量的方式来表达程序，可以把这些变量转换成地址
* 信息=位+上下文
* 指针
* Linux内存管理中通过MMU的硬件实现虚拟地址到物理地址的转换，但是每次都这样转换势必造成性能的损耗，所以采用了缓存组件TLB来缓存最近使用的虚拟地址到物理地址的映射
* 类型
  - 随机存储器（RAM）： 内存中最重要的一种，表示既可以从中读取数据，也可以写入数据。当机器关闭时，内存中的信息会丢失
  - 只读存储器（ROM）：ROM 一般只能用于数据的读取，不能写入数据，但是当机器停电时，这些数据不会丢失
  - 高速缓存（Cache）：Cache 也是我们经常见到的，它分为一级缓存（L1 Cache）、二级缓存（L2 Cache）、三级缓存（L3 Cache）这些数据，它位于内存和 CPU 之间，是一个读写速度比内存更快的存储器。当 CPU 向内存写入数据时，这些数据也会被写入高速缓存中。当 CPU 需要读取数据时，会直接从高速缓存中直接读取，当然，如需要的数据在 Cache 中没有，CPU 会再去读取内存中的数据
* 虚拟内存：指把磁盘的一部分作为假想内存来使用。这与磁盘缓存是假想的磁盘（实际上是内存）相对，虚拟内存是假想的内存（实际上是磁盘
  - 应用程序认为它拥有连续可用的内存（一个完整的地址空间），但是实际上，它通常被分割成多个物理碎片，还有部分存储在外部磁盘管理器上，必要时进行数据交换
  - 通过借助虚拟内存，在内存不足时仍然可以运行程序
  - 虚拟内存与内存交换方式
    + Windows 采用的是分页式。该方式是指在不考虑程序构造的情况下，把运行的程序按照一定大小的页进行分割，并以页为单位进行置换。在分页式中，我们把磁盘的内容读到内存中称为 Page In，把内存的内容写入磁盘称为 Page Out。Windows 计算机的页大小为 4KB ，也就是说，需要把应用程序按照 4KB 的页来进行切分，以页（page）为单位放到磁盘中，然后进行置换

## 磁盘 disk

* 计算机上外部存储设备，可以持久存储大量数据。 
  - CPU 无法直接访问硬盘中的数据，当计算机启动时操作系统会将硬盘中的数据加载到内存中以便 CPU 访问
  - 如果 CPU 要访问数据不在内存中，需要花费几千倍甚至几十万倍的时间来读取数据
  - CPU 访问硬盘数据过程比较复杂，先通过 I/O 操作将磁盘中的数据读入内存，再访问内存的数据
* 机械硬盘 Hard Disk Drive HDD
  - 电磁存储，通过电磁信号转变来控制读写，磁头机械臂移动
  - 在读取和写入数据的过程中，硬盘机械臂连接的磁头通过移动磁头到对应的磁道，然后再旋转磁头到对应的扇区。最后进行移动磁头进行读写数据。
  - 磁盘具有比较复杂的机械结构，所以磁盘的读取和写入都要花费很多时间，数据库的读写性能也基本都依赖于磁盘的性能
  - 由盘片，磁头，盘片转轴及控制电机，磁头控制器，数据转换器，接口，缓存等几个部分组成
    + 一个盘片可能会有两个盘面，机械硬盘中所有的盘片都装在一个旋转轴上，每张盘片之间是平行的，在每个盘片的存储面上有一个磁头，磁头与盘片之间的距离比头发丝的直径还小，所有的磁头联在一个磁头控制器上，由磁头控制器负责各个磁头的运动
    + 每个盘面对应一个磁头，所有磁头连在一个磁臂上，磁头共进退，磁头可沿盘片的半径方向运动，加上盘片每分钟几千转的高速旋转，磁头就可以定位在盘片的指定位置上进行数据的读写操作
    + 柱面：所有盘面中相对位置相同磁道
    + 数据通过磁头由电磁流来改变极性方式被电磁流写到磁盘上，也可以通过相反方式读取。硬盘为精密设备，进入硬盘的空气必须过滤
  - 一次硬盘数据读写主要包括三大部分耗时：寻道时间、旋转时间、传输时间。而在这其中寻道时间主要占大头，主要是因为磁头的移动主要是马达通过驱动磁臂近而移动磁头，这个运动属于机械运动，所以速度相对较慢。
    + 寻道时间：8ms~12ms
    + 旋转时间：7200 转/min：半周 4ms
    + 传输时间：50M/s，约 0.3ms
  - 随机 I/O：随机查询一条数据，可能会触发磁盘的随机 I/O：将数据从磁盘读取到内存中所需要的成本是非常大的，普通磁盘（非 SSD）加载数据需要经过队列、寻道、旋转以及传输的这些过程，大概要花费 10ms 左右的时间
    + 可以使用 10ms 这个数量级对随机 I/O 占用的时间进行估算，这里想要说的是随机 I/O 对于数据库的查询性能影响会非常大，而顺序读取磁盘中的数据时速度可以达到 40MB/s
  - 顺序 IO 主要减少了磁头的移动频率，也就是减少了寻道时间。所以它的性能要比随机 IO 要快很多。
  - HDD 在价格、容量、使用寿命上占有绝对优势
* 固态硬盘（Solid State Drive、SSD）
  - 半导体存储，用固态电子存储芯片阵列、由控制单元和存储单元组成，内部由闪存颗粒组成。速度较
  - 在接口的规范和定义、功能及使用方法上与普通硬盘的完全相同
  - 在乱序写时，性能表现比机械硬盘会好很多，特别是多线程同时进行写操作时，性能也会比单线程顺序写强
  - 在防震抗摔、传输速率、功耗、重量、噪音上有明显优势，SSD 传输速率性能是HDD 的2倍
* 物理结构：磁盘存储数据的形式
  - 可变长方式将物理结构划分成长度可变的空间
  - 扇区方式：将磁盘结构划分为固定长度的空间
    + 把磁盘表面分成若干个同心圆的空间就是 磁道
    + 把磁道按照固定大小的存储空间划分而成的就是 扇区
* 页缓存：操作系统用来作为磁盘的一种缓存，减少磁盘的I/O操作
  - 写入磁盘：其实是写入页缓存中，使得对磁盘的写入变成对内存的写入。写入的页变成脏页，然后操作系统会在合适的时候将脏页写入磁盘中
    + 后写：写入的页缓存，这样存着可以将一些小的写入操作合并成大的写入，然后再刷盘
  - 读取：如果页缓存命中则直接返回，如果页缓存 miss 则产生缺页中断，从磁盘加载数据至页缓存中，然后返回数据
    + 读的时候会预读，根据局部性原理当读取的时候会把相邻的磁盘块读入页缓存中
* 顺序读写：磁头几乎不用换道，或者换道的时间很短
  - 顺序写盘的速度比随机写内存还要快
  - 当然这样的写入存在数据丢失的风险，例如机器突然断电，那些还未刷盘的脏页就丢失了。不过可以调用 fsync 强制刷盘，但是这样对于性能的损耗较大
  - 建议通过多副本机制来保证消息的可靠，而不是同步刷盘
* 磁盘缓存：把从磁盘中读出的数据存储到内存的方式，这样一来，当接下来需要读取相同的内容时，就不会再通过实际的磁盘，而是通过磁盘缓存来读取。某一种技术或者框架的出现势必要解决某种问题的，那么磁盘缓存就大大改善了磁盘访问的速度
* 文件存储：文件就是字节数据的集合
* 压缩算法 compaction algorithm
  - 无损压缩：能够无失真地从压缩后的数据重构，准确地还原原始数据。可用于对数据的准确性要求严格的场合，如可执行文件和普通文件的压缩、磁盘的压缩，也可用于多媒体数据的压缩。该方法的压缩比较小。如差分编码、RLE、Huffman 编码、LZW 编码、算术编码。
  - 有损压缩：有失真，不能完全准确地恢复原始数据，重构的数据只是原始数据的一个近似。可用于对数据的准确性要求不高的场合，如多媒体数据的压缩。该方法的压缩比较大。例如预测编码、音感编码、分形压缩、小波压缩、JPEG/MPEG
  - 视频编码中会同时用到帧内与帧间的编码方法
    + 帧内编码是指在一帧图像内独立完成的编码方法，同静态图像的编码，如 JPEG
    + 帧间编码则需要参照前后帧才能进行编解码，并在编码过程中考虑对帧之间的时间冗余的压缩，如 MPEG
  - RLE Run Length Encoding 行程长度编码：字符 * 重复次数 AAAAAABBCDDEEEEEF 的 17 个字符成功被压缩成了 A6B2C1D2E5F1 的 12 个字符
  - 莫尔斯编码
    + 把文本中出现最高频率的字符用短编码来表示
  - 哈夫曼算法:为压缩对象文件分别构造最佳的编码体系，并以该编码体系为基础来进行压缩
    + 出现频率高的字符用尽量少的位数编码来表示这一原则进行整理。按照出现频率从高到低的顺序整理后
    + 通过借助哈夫曼树的构造编码体系,构造哈夫曼树

### 页


## I/O 操作

* 编程 I/O（Programmed I/O）：CPU 会负责全部的工作，如果想要在屏幕上输出 Hello World，CPU 每次都会向 I/O 设备中写入一个新字符，写入后会轮询设备的状态等待它完成工作后写入新的字符。这种方式虽然简单，但是它会占用全部的 CPU 资源，在某些复杂的系统中会造成计算资源的严重浪费
* 中断驱动 I/O（Interrupt-driven I/O）：执行 I/O 操作的一种更高效方式，在编程 I/O 中，CPU 会主动获取设备的状态并等待设备闲置，但是如果使用了中断驱动 I/O，设备会在闲置时主动发起中断暂停当前进程并保存上下文，而操作系统会执行 I/O 设备的中断处理程序：
  - 如果当前不包含待打印的字符，停止中断处理程序并恢复暂停的进程；
  - 如果当前包含待打印的字符，将下一个字符拷贝到设备中并恢复暂停的进程；
  - 使用中断驱动 I/O 可以在设备繁忙时，让 CPU 能够处理其它任务，尽可能地提高 CPU 的利用率，不再浪费珍贵的计算资源。与编程 I/O 相比，中断驱动 I/O 将一部分工作交给了 I/O 设备，所以能够提高资源的利用率。
* 直接内存访问（Direct Memory Access)：利用 DMA 控制器来执行 I/O 操作，中断驱动 I/O 需要为每个字符触发操作系统中断，这会消耗一定的 CPU 时间。当我们使用 DMA 控制器时，CPU 会一次将缓冲区中的数据全部读到 DMA 控制器中，DMA 控制器会负责将数据按字符写入 I/O 设备
  - DMA 控制器可以解放 CPU 并减少中断次数，但是它的执行速度与 CPU 相比却很慢，如果 DMA 控制器不能快速驱动 I/O 设备，CPU 可能就会等待 DMA 控制器触发中断，在这种情况下，中断驱动 I/O 或者编程 I/O 可以提供更快的访问速度
* 在默认情况下，会使用 DMA 控制器来执行 I/O 任务，不过编程 I/O 和中断驱动 I/O 也不是不能接受的选项。当 CPU 经常需要等待 DMA 控制器执行 I/O 任务时，使用中断驱动 I/O 甚至轮询的编程 I/O 都可以得到更高的吞吐量，然而无论使用哪种方式，I/O 都是程序中比较耗时的复杂操作

## Cache

* 工作过程:cpu 与 cache 交换字，cache 与内存交换块
* 写策略
  - 写穿策略（write through）：同时写缓存和内存，好像穿过缓存一样。若不命中，先写到主存中，并选择性地同时分配到缓存中（写分配/非写分配）
  - 写回策略（write back）：写到缓存后不管了，只有当缓存的内容替换回主存时再管，需有脏位。好像隔段时间后再写回到主存中一样
* 映射方式
  - 全相联：cache 行号 = random（内存块号）
  - 直接相联：cache 行号 = 内存块号 % cache 行数
  - 组相联：两者结合。8 行 1 路组相联就是全相联，8 行 8 路组相联就是直接相联
* 替换算法
  - 先进先出法-FIFO
  - 最近最不经常使用法-LFU
  - 近期最少使用法-LRU
  - 随机替换法

## 延迟数

* 从磁盘以 30 MB/s 的速度顺序读取
* 以 100 MB/s 从 1 Gbps 的以太网顺序读取
* 从 SSD 以 1 GB/s 的速度读取
* 以 4 GB/s 的速度从主存读取
* 每秒能绕地球 6-7 圈
* 数据中心内每秒有 2,000 次往返

```
Latency Comparison Numbers
--------------------------
L1 cache reference                           0.5 ns
Branch mispredict                            5   ns
L2 cache reference                           7   ns                      14x L1 cache
Mutex lock/unlock                          100   ns
Main memory reference                      100   ns                      20x L2 cache, 200x L1 cache
Compress 1K bytes with Zippy            10,000   ns       10 us
Send 1 KB bytes over 1 Gbps network     10,000   ns       10 us
Read 4 KB randomly from SSD*           150,000   ns      150 us          ~1GB/sec SSD
Read 1 MB sequentially from memory     250,000   ns      250 us
Round trip within same datacenter      500,000   ns      500 us
Read 1 MB sequentially from SSD*     1,000,000   ns    1,000 us    1 ms  ~1GB/sec SSD, 4X memory
Disk seek                           10,000,000   ns   10,000 us   10 ms  20x datacenter roundtrip
Read 1 MB sequentially from 1 Gbps  10,000,000   ns   10,000 us   10 ms  40x memory, 10X SSD
Read 1 MB sequentially from disk    30,000,000   ns   30,000 us   30 ms 120x memory, 30X SSD
Send packet CA->Netherlands->CA    150,000,000   ns  150,000 us  150 ms

Notes
-----
1 ns = 10^-9 seconds
1 us = 10^-6 seconds = 1,000 ns
1 ms = 10^-3 seconds = 1,000 us = 1,000,000 ns
```

## CS Computer Science

* C语言基础
  - [CSE 251 Programming in C](https://www.cse.msu.edu/~cse251/index.html)
  - The Absolute Beginner's Guide to C
  - 课程站点上的所有14个Steps实验+3个Projects
* [Computer Systems: A Programmer's Perspective CSAPP 深入理解计算机系统](http://csapp.cs.cmu.edu/3e/home.html) 3/E (CS:APP3e) Randal E. Bryant and David R. O'Hallaron, Carnegie Mellon University
  - [Berkeley CS 61C](http://inst.eecs.berkeley.edu/~cs61c/sp15/)
  - [cmu 15-213/18-213: Introduction to Computer Systems (ICS)](http://www.cs.cmu.edu/~213/)
  - [CSE351: The Hardware/Software Interface](http://courses.cs.washington.edu/courses/cse351/)
    + [](https://www.bilibili.com/video/BV1Zt411s7Gg)
    + [](https://www.bilibili.com/video/BV1iW411d7hd?p=1)
  - [CSAPP书籍配套的所有Labs](http://csapp.cs.cmu.edu/3e/labs.html)
  - [视频](https://www.bilibili.com/video/av31289365)
* 数据结构
  - [Berkeley CS61B Data Structures](https://sp19.datastructur.es/)
    + [ [2019 SP/2020 FA] UCB CS 61B Data Structures](https://www.bilibili.com/video/BV1EJ411n72e)
	* [Berkeley CS61B](http://datastructur.es/sp17/)
  - Head First Java + 数据结构书自选
  - CS 61B站点上的所有Labs/Homeworks/Projects
* 操作系统
  - [MIT 6.828 Operating System Engineering](https://pdos.csail.mit.edu/6.828/2018/index.html)
  - [HMC CS 134 2019 Operating System](https://www.bilibili.com/video/av47977122)
  - 操作系统导论(Operating Systems: Three Easy Pieces)
  - MIT 6.828站点上的所有7个Labs
* 计算机网络
  - [CS 144 Introduction to Computer Networking](https://cs144.github.io/)
  - 计算机网络：自顶向下方法
  - CS 144 站点上的所有8个Labs
* 编译原理
  - [Crafting Interpreters](https://www.craftinginterpreters.com/contents.html) [Write an Interpreter in Go](https://interpreterbook.com/)
  - [CS143 斯坦福编译原理](https://www.bilibili.com/video/BV1cE411f78c)
  - 参考Crafting Interpreters，使用Java或者golang语言(或其它熟悉的语言)，实现Lox小型编程语言。
  - 参考Write an Interpreter in Go ，或 [Write A Compiler in Go](https://compilerbook.com/)，使用Java语言实现Monkey小型语言。
* 数据库系统
  - [CMU 15-445/645 Database Systems](https://15445.courses.cs.cmu.edu/fall2020/)
    + [](https://www.bilibili.com/video/BV1Cp4y1C7dv)
  - 数据库系统概念
  - 参考[vanilladb](https://github.com/vanilladb/vanillacore)项目，使用golang语言实现clone版的vanilladb（原项目是Java实现的）
* 计划
  - [自学计算机科学](https://github.com/keithnull/TeachYourselfCS-CN/blob/master/TeachYourselfCS-CN.md)
  - [自学计算机科学]( https://github.com/ossu/computer-science)

## 图书

* 《计算机是怎样跑起来的》
* 编码·隐匿在计算机硬件背后的语言
* [计算机程序的构造和解释 Structure and Interpertation of Computer Programming SICP](https://www.bilibili.com/video/av8515129)
  - [Learning-SICP](https://github.com/DeathKing/Learning-SICP):MIT视频公开课《计算机程序的构造和解释》中文化项目及课程学习资料搜集。 <https://learningsicp.github.io>
  - [book](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html)
  - [video lecture](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/video-lectures/)
  - [Brian Harvey’s Berkeley CS 61A](https://archive.org/details/ucberkeley-webcast-PL3E89002AA9B9879E?sort=titleSorter) <https://inst.eecs.berkeley.edu/~cs61a/fa19/>
  - [CS 61A: Structure and Interpretation of Computer Programs](https://cs61a.org/)
  - [Composing Programs](http://www.composingprograms.com/)
  * [SICP-answers](https://github.com/huangz1990/SICP-answers):SICP 解题集 <http://sicp.readthedocs.org/>
  * 
* [Mathematics for Computer Science](https://courses.csail.mit.edu/6.042/spring17/mcs.pdf)
  - Tom Leighton’s MIT 6.042J
* 《计算机程序的概念、技术和模型 Concepts, Techniques, and Models of Computer Programming，CTMCP》
* [The Elements of Computing Systems](https://www.nand2tetris.org/)
* [计算的本质：深入剖析程序和计算机](https://www.amazon.cn/gp/product/B00PG0MM3C)
* [Bottom Up Computer Science](https://github.com/ianw/bottomupcs) <http://www.bottomupcs.com>
* The Encyclopedia of Human-Computer Interaction
* [计算机系统概论](https://www.amazon.cn/gp/product/B0011F9OQE)
* [Introduction to Computer Organization with x86-64 Assembly Language & GNU/Linux](http://bob.cs.sonoma.edu/IntroCompOrg-x64/book.html)
* [Introduction to Computing Explorations in Language, Logic, and Machines](https://www.cs.virginia.edu/~evans/ctbook/)
* [Electronic References](https://csgordon.github.io/books.html)
* 程序设计实践 The practise of programming

## 项目

* [comp-m2](https://github.com/gto76/comp-m2):Comp Mark II – Simple 4-bit virtual computer
* [Chip-8 Technical Reference v1.0](http://devernay.free.fr/hacks/chip8/C8TECH10.HTM)
* [Build an 8-bit CPU from scratch](https://eater.net/)

## 课程

* [Computation Structures](https://computationstructures.org/index.html)
* [哈佛大学计算机核心课程](https://www.bilibili.com/video/av19302731)
* [The Missing Semester of Your CS Education](https://github.com/missing-semester/missing-semester)<https://missing.csail.mit.edu/>
* [Teach Yourself Computer Science](https://teachyourselfcs.com/)
* [computer-science](https://github.com/ossu/computer-science) 🎓 Path to a free self-taught education in Computer Science!
* [Composing Programs](http://www.composingprograms.com/): a free online introduction to programming and computer science.
* [CS-Notes](https://github.com/CyC2018/CS-Notes):📚 Computer Science Learning Notes
* [SJTU-Courses](https://github.com/CoolPhilChen/SJTU-Courses/):上海交通大学课程资料分享
  - [sjtu-se-courseware](https://github.com/sjtu-se-courseware/sjtu-se-courseware):上海交大软件学院课件
* [REKCARC-TSC-UHT](https://github.com/PKUanonym/REKCARC-TSC-UHT):清华大学计算机系课程攻略 Guidance for courses in Department of Computer Science and Technology, Tsinghua University <https://rekcarc-tsc-uht.readthedocs.io/>
* [USTC-CS-Courses-Resource](https://github.com/mbinary/USTC-CS-Courses-Resource):❤️中国科学技术大学计算机学院课程资源 <https://mbinary.xyz/ustc-cs/>
  - ftp.ustclug.org； /ebook/USTC-CS-Courses-Resource； ftp@ftp
  - afp://ftp.ustclug.org/； /ebook/USTC-CS-Courses-Resource； Connect As Guest
* [PKUCourse](https://github.com/tongtzeho/PKUCourse):北大计算机课程大作业
* [HIT-Computer-Courses](https://github.com/wxwmd/HIT-Computer-Courses):哈工大计算机课程资料，包含计算机系统等多个科目
* [CS50's Introduction to Computer Science](https://www.edx.org/course/cs50s-introduction-computer-science-harvardx-cs50x)
  - [This is CS50x](https://cs50.harvard.edu/x/2021/notes/0/)
* [crash-course-computer-science-chinese](https://github.com/1c7/crash-course-computer-science-chinese):💻 计算机速成课 <https://www.bilibili.com/video/av21376839/>
* [Yorgey's cis194](https://www.seas.upenn.edu/~cis194/spring13/lectures.html)
* [卡梅隆大学CS课件](http://www.cs.cmu.edu/~aada/courses/15251f16/www/schedule.html)
* [cs-video-courses](https://github.com/Developer-Y/cs-video-courses):List of Computer Science courses with video lectures.
* [LIFT-CS: Laboratory for Innovation for the Future of Teaching Computer Science](https://lift.cs.princeton.edu/)
* [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/)
* [This is The Entire Computer Science Curriculum in 1000 YouTube Videos](https://web.archive.org/web/20210210143025/https://laconicml.com/computer-science-curriculum-youtube-videos/)

## 参考

* Apple Developer Site — 学习开发 IOS、Mac OS、Safari 环境下的 app
* Google Code — 学习开发安卓 app
* Code.org — 编程一小时活动的大本营
* CodeHS
* Aquent Gymnasium
* [computer-science-in-javascript](https://github.com/humanwhocodes/computer-science-in-javascript)Collection of classic computer science paradigms, algorithms, and approaches written in JavaScript. <http://www.nczonline.net/>
* [Treehouse](https://teamtreehouse.com/):学习编程等互联网技能
* [Playground](https://www.apple.com/swift/playgrounds/):ipad 上学习 swift 的游戏
* [scratch](https://scratch.mit.edu/)
* [Introduction: A Guide To The Tech Tree](https://github.com/github/archive-program/blob/master/TheTechTree.md)
* [CPU 缓存](https://coolshell.cn/articles/20793.html)
* [CPU 和 GPU - 异构计算的演进与发展](https://draveness.me//heterogeneous-computing)

[程序员不得不了解的硬核知识大全](https://gitbook.cn/books/5e40f2c79b420438e62ec2de/index.html)
