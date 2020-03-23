# Data Structures

如何把现实问题转化为计算机语言的表示：设计出数据结构， 在施加以算法就行了，


### Array

### 栈

### 队列

### 链表(Singly-linked List)

### 双向链表(Doubly-Linked List)

### 堆(heap)

### 栈(stack)

### 哈希表（hash table）

### 树

* 特点
    - 每个节点有零个或多个子节点；
    - 没有父节点的节点称为根节点；
    - 每一个非根节点有且只有一个父节点；
    - 除了根节点外，每个子节点可以分为多个不相交的子树
* 术语
    - 节点的度：一个节点含有的子树的个数称为该节点的度；
    - 树的度：一棵树中，最大的节点的度称为树的度；
    - 叶节点或终端节点：度为零的节点；
    - 非终端节点或分支节点：度不为零的节点；
    - 父亲节点或父节点：若一个节点含有子节点，则这个节点称为其子节点的父节点；
    - 孩子节点或子节点：一个节点含有的子树的根节点称为该节点的子节点；
    - 兄弟节点：具有相同父节点的节点互称为兄弟节点；
    - 节点的层次：从根开始定义起，根为第1层，根的子节点为第2层，以此类推；
    - 深度：对于任意节点n,n的深度为从根到n的唯一路径长，根的深度为0；
    - 高度：对于任意节点n,n的高度为从n到一片树叶的最长路径长，所有树叶的高度为0；
    - 堂兄弟节点：父节点在同一层的节点互为堂兄弟；
    - 节点的祖先：从根到该节点所经分支上的所有节点；
    - 子孙：以某节点为根的子树中任一节点都称为该节点的子孙。
    - 森林：由m（m>=0）棵互不相交的树的集合称为森林；

### 二叉查找树(Binary search tree)

* 规定
    - 非叶子节点只能允许最多两个子节点存在，左子树和右子树
    - 左边的子节点小当前节点的值，右边的子节点大于当前节点的值
* 平衡树(AVL tree)：大多数情况下二叉查找树的平均查找速度比顺序查找要快。想二叉查找数的查询性能最高，需要这棵二叉查找树是平衡的
    - 任何节点的两个子树的高度差不能大于1
    - 平衡二叉树的查找性能是比较高的（性能最好的是最优二叉树），查询性能越好，维护的成本就越大
        + 实际应用场景中可能需要旋转多次
    - 查询性能和树的层级（h高度）成反比，h值越小查询越快、为了保证树的结构左右两端数据大致平衡降低二叉树的查询难度一般会采用一种算法机制实现节点数据结构的平衡，实现了这种算法的有比如AVL、Treap、红黑树，使用平衡二叉树能保证数据的左右两边的节点层级相差不会大于1.，通过这样避免树形结构由于删除增加变成线性链表影响查询效率，保证数据平衡的情况下查找数据的速度近于二分法查找；
* 特点
    - 非空二叉树的第 n 层上至多有 2^(n-1)个元素。
    - 深度为 h 的二叉树至多有 2^h-1 个结点。
    - 满二叉树：所有终端都在同一层次，且非终端结点的度数为 2。若其深度为 h，则其所包含的结点数必为 2^h-1。
    - 完全二叉树：除了最大的层次即成为一颗满二叉树且层次最大那层所有的结点均向左靠齐，即集中在左面的位置上，不能有空位置。设一个结点为 i 则其父节点为 i/2，2i 为左子节点，2i+1 为右子节点。
* 遍历
    - 前序遍历(垂直)：根结点->左子树->右子树
    - 中序遍历（由下向上）:一个有序序列。由于树的高度，区间查询需要中序遍历，都会导致查询效率很慢
        + 中序遍历左子树；
        + 访问根结点；
        + 中序遍历右子树。
    - 后序遍历（先水平后垂直）:左子树->右子树->根结点
* 广度优先:即是层次遍历，按一层一层地遍历

```
graph TD 3-->1 3-->5 1-->2 5-->4 5-->6

前序遍历结果： 3 1 2 5 4 6
中序遍历结果： 1 2 3 4 5 6
后序遍历结果： 2 1 4 6 5 3
```

### B树(B-tree)

* 一种树状数据结构，能够用来存储排序后的数据
* 能够让查找数据、循序存取、插入数据及删除的动作，都在对数时间内完成
* 概括来说是一个一般化的二叉查找树，可以拥有多于2个子节点。与自平衡二叉查找树不同，B-树为系统最优化大块数据的读和写操作
* B-tree算法减少定位记录时所经历的中间过程，从而加快存取速度。这种数据结构常被应用在数据库和文件系统的实作上

### B+树

* B树的变体，也是一种多路搜索树,其定义基本与B-树相同，B+ Tree与B Tree的区别如下：
    - 非叶子结点的子树指针与关键字个数相同；B+节点关键字搜索采用闭合区间（B-树是开区间）
    - B+非叶节点不保存数据相关信息，只保存关键字和子节点的引用；
    - B+关键字对应的数据保存在叶子节点中
    - B+叶子节点是顺序排列的，并且相邻节点具有顺序引用的关系
* 优点
* 扫库、表能力更强
* 的磁盘读写能力更强
* 排序能力更强
* 的查询效率更加稳定

### 平衡二叉树（Balanced Binary Tree）又被称为AVL树（有别于AVL算法）

* 一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树
* 数据处的（高）深度决定着他的IO操作次数，IO操作耗时大
* 每一个磁盘块（节点/页）保存的数据量太小了
* 没有很好的利用操作磁盘IO的数据交换特性
* 也没有利用好磁盘IO的预读能力（空间局部性原理），从而带来频繁的IO操作

### 红黑树（red-balck tree）

* 特征
    - 根节点为黑色
    - 一个节点为红色，子节点必定为黑色
    - 从任意一点触发到达每一个叶子节点的黑色节点个数相同
    - 每一个节点不是红色就是黑色
    - 每一个叶子节点都是黑色 
* 插入： 
    - 如果父节点为黑色，直接插入不处理 
    - 如果父节点为红色，叔叔节点为红色，则父节点和叔叔节点变为黑色，祖先节点变为红色，将节点操作转换为祖先节点 
    - 如果当前节点为父亲节点的右节点，则以父亲结点为中心左旋操作 
    - 如果当前节点为父亲节点的左节点，则父亲节点变为黑色，祖先节点变为红色，以祖先节点为中心右旋操作 
* 删除： 
    - 先按照排序二叉树的方法，删除当前节点，如果需要转移即转移到下一个节点 
    - 当前节点，必定为这样的情况：没有左子树。 
    - 删除为红色节点，不需要处理，直接按照删除二叉树节点一样 
    - 如果兄弟节点为黑色，兄弟节点的两个子节点为黑色，则将兄弟节点变为红色，将着色转移到父亲节点 
    - 如果兄弟节点为红色，将兄弟节点设为黑色，父亲结点设为红色节点，对父亲结点进行左旋操作 
    - 如果兄弟节点为黑色，左孩子为红色，右孩子为黑色，对兄弟节点进行右旋操作 
    - 如果兄弟节点为黑色，右孩子为红色，则将父亲节点的颜色赋值给兄弟节点，将父亲节点设置为黑色，将兄弟节点的右孩子设为黑色，对父亲节点进行左旋 

### 图

## 应用

*   学了顺序表和链表，你就知道，在查询操作更多的程序中，你应该用顺序表；
*   而修改操作更多的程序中，你要使用链表；
*   而单向链表不方便怎么办，每次都从头到尾好麻烦啊你这时就会想到双向链表 or 循环链表。
*   学了栈之后，你就知道，很多涉及后入先出的问题，例如函数递归就是个栈模型、Android 的屏幕跳转就用到栈，很多类似的东西，你就会第一时间想到：我会用这东西来去写算法实现这个功能。学了队列之后，你就知道，对于先入先出要排队的问题，你就要用到队列，例如多个网络下载任务，我该怎么去调度它们去获得网络资源呢？再例如操作系统的进程（or 线程）调度，我该怎么去分配资源（像 CPU）给多个任务呢？肯定不能全部一起拥有的，资源只有一个，那就要排队！那么怎么排队呢？用普通的队列？但是对于那些优先级高的线程怎么办？
*   这时，你就会想到了优先队列，优先队列怎么实现？用堆，然后你就有疑问了，堆是啥玩意？自己查吧，敲累了。总之好好学数据结构就对了。我觉得数据结构就相当于：我塞牙了，那么就要用到牙签这“数据结构”，当然你用指甲也行，只不过“性能”没那么好；我要拧螺母，肯定用扳手这个“数据结构”，当然你用钳子也行，只不过也没那么好用。学习数据结构，就是为了了解以后在 IT 行业里搬砖需要用到什么工具，这些工具有什么利弊，应用于什么场景。以后用的过程中，你会发现这些基础的“工具”也存在着一些缺陷，你不满足于此工具，此时，你就开始自己在这些数据结构的基础上加以改造，这就叫做自定义数据结构。而且，你以后还会造出很多其他应用于实际场景的数据结构。。你用这些数据结构去造轮子，不知不觉，你成了又一个轮子哥。
*   一个负载稍高一点的 Python 网站，你不懂数据结构，你都不知道 List 和 Dictionary 的性能曲线大概会怎么变，需要深度优化的时候怎么下手。

数据结构的作用，就是为了提高硬件利用率。比如操作系统需要查找用户应用程序"office"在硬盘的哪个位置，盲目的搜索一遍硬盘肯定是低效的，这时候搞个 b+树作为索引，搜索 office 这个单词就很快，然后就能很快的定位 office 这个应用程序的文件信息，再找到文件信息中对应的磁盘位置了。数据结构的东西找本《算法导论》，《数据结构与算法分析》之类的看吧。

的确很少有写业务代码的时候会直接用上二叉树。但是真的没有吗？XML/DOM 是什么？是不是一棵树？为什么 DOM 可以和 XML 一一对应？因为 XML 序列化就是树的遍历的结果。能和 XML 对应，也就能跟 JSON 对应，因为两者都可以对应到树（只是表示逻辑上有些区别）。一个业务系统里有任务（Task），任务有相应的执行计划（Plan），计划可以用子任务组成，子任务可以是基础任务，也可以通过 Plan 拆分成更多的子任务。这是什么？这不就是树吗？那么怎么存储？JSON 不就很好吗。怎么从 JSON 加载、再保存会 JSON？树的遍历。怎么计算任务总共需要多少个基础任务？树的遍历。怎么计算计划总共需要多少时间？树的遍历。一个社交系统里，用户可以加好友，好友还有别的好友，这是什么？无向图。如果是知乎这样的关注系统呢？有向图。一个用户点了个赞，扩散到另一个用户至少要经过几次转发？最短路径。我要画一个小圈子里的人之间的关系图，怎么做？最小生成树。我要整理信息路径，看这批用户里哪些生产内容，哪些阅读内容，按什么次序传播，怎么做？拓扑排序。

说明数据结构首先就是“数据的结构”，在内存上的存储方式，就是物理的存储结构，在程序使用人员的思想上它是逻辑的，比如：你们在 C/C++中学习到链表，那么链表是什么一个概念，你们使用指针制向下一个结点的首地址，让他们串联起来，形成一个接一个的结点，就像显示生活中的火车一样。而这只是对于程序员的概念，但是在内存中存储的方式是怎样的那？对于你程序员来说这是“透明”的，其内部分配空间在那里，都是随机的，而内存中也没有一个又一根的线将他们串联起来，所以，这是一个物理与逻辑的概念，对于我们程序员只需要知道这些就可以了，而我们主要要研究的是“逻辑结构”。我可以给你一个我自己总结的一个概念：所有的算法必须基于数据结构生存。也就是说，我们对于任何算法的编写，必须依赖一个已经存在的数据结构来对它进行操作，数据结构成为算法的操作对象，这也是为什么算法和数据结构两门分类不分家的概念，算法在没有数据结构的情况下，没有任何存在的意义；而数据结构没有算法就等于是一个尸体而没有灵魂。估计这个对于算法的初学者可能有点晕，我们在具体的说一些东西吧：我们在数据结构中最简单的是什么：我个人把书籍中线性表更加细化一层（这里是为了便于理解在这样说的）：单个元素，比如：int i;这个 i 就是一个数据结构，它是一个什么样的数据结构，就是一个类型为 int 的变量，我们可以对它进行加法/减法/乘法/除法/自加等等一系列操作，当然对于单个元素我们对它的数据结构和算法的研究没有什么意义，因为它本来就是原子的，某些具体运算上可能算法存在比较小的差异；而提升一个层次：就是我们的线性表（一般包含有：顺序表/链表）那么我们研究这样两种数据结构主要就是要研究它的什么东西那？一般我们主要研究他们以结构为单位（就是结点）的增加/删除/修改/检索（查询）四个操作（为什么有这样的操作，我在下面说到），我们一般把“增加/删除/修改”都把它称为更新，对于一个结点，若要进行更新一类的操作比如：删除，对于顺序表来说是使用下标访问方式，那么我们在删除了一个元素后需要将这个元素后的所有元素后的所有元素全部向前移动，这个时间是对于越长的顺序表，时间越长的，而对于链表，没有顺序的概念，其删除元素只需要将前一个结点的指针指向被删除点的下一个结点，将空间使用 free()函数进行释放，还原给操作系统。当执行检索操作的时候，由于顺序表直接使用下标进行随机访问，而链表需要从头开始访问一一匹配才可以得到使用的元素，这个时间也是和链表的结点个数成正比的。所以我们每一种数据结构对于不同的算法会产生不同的效果，各自没有绝对的好，也没有绝对的不好，他们都有自己的应用价值和方式；这样我们就可以在实际的项目开发中，对于内部的算法时间和空间以及项目所能提供的硬件能力进行综合评估，以让自己的算法能够更加好。（在这里只提到了基于数据结构的一个方面就是：速度，其实算法的要素还应该包括：稳定性、健壮性、正确性、有穷性、可理解性、有输入和输出等等）为什么要以结点方式进行这些乱七八糟的操作那？首先明确一个概念就是：对于过程化程序设计语言所提供的都是一些基础第一信息，比如一些关键字/保留字/运算符/分界符。而我们需要用程序解决现实生活中的问题，比如我们要程序记录某公司人员的情况变化，那么人员这个数据类型，在程序设计语言中是没有的，那么我们需要对人员的内部信息定义（不可能完全，只是我们需要那些就定义那些），比如：年龄/性别/姓名/出生日期/民族/工作单位/职称/职务/工资状态等，那么就可以用一些 C/C++语言描述了，如年龄我们就可以进行如下定义:
int age;/_age 变量，表示人员公司人员的年龄_/
同理进行其他的定义，我们用结构体或类把他们封装成自定义数据类型或类的形式，这样用他们定义的就是一个人的对象的了，它内部包含了很多的模板数据了。我就我个人的经历估计的代码量应该 10000 以内的（我个人的经理：只是建议，从你的第一行代码开始算，不论程序正确与否，不论那一门语言，作为一个标准程序员需要十万行的代码的功底（这个是我在大学二年级感觉有一定时候的大致数据，不一定适合其他人），而十万行代码功底一般需要四门基础远支撑，若老师没有教，可以自学一些语言）。

坚持刷 leetcode，因为找工作有用

AVL 树: 最早的平衡二叉树之一。应用相对其他数据结构比较少。windows 对进程地址空间的管理用到了 AVL 树。红黑树: 平衡二叉树，广泛用在 C++的 STL 中。如 map 和 set 都是用红黑树实现的。
epoll 在内核中的实现，用红黑树管理事件块
nginx 中，用红黑树管理 timer 等著名的 linux 进程调度,用红黑树管理进程控制块
B/B+树: 用在磁盘文件组织 数据索引和数据库索引。
Trie 树(字典树): 用在统计和排序大量字符串，如自动机。

AVL 是一种高度平衡的二叉树，所以通常的结果是，维护这种高度平衡所付出的代价比从中获得的效率收益还大，故而实际的应用不多，更多的地方是用追求局部而不是非常严格整体平衡的红黑树。当然，如果场景中对插入删除不频繁，只是对查找特别有要求，AVL 还是优于红黑的。

有一种数据结构是树（Tree），树里面有一种树叫二叉搜索树（Binary Search Tree），平均复杂度是 O(logN)，具有不错的查询性能。但是在这里，我们忽略了一个关键的问题，复杂度模型是基于每次相同的操作成本来考虑的，数据库的实现比较复杂，数据保存在磁盘上，而为了提高性能，每次又可以把部分数据读入内存来计算，因为我们知道——磁盘访问的成本大概是内存访问成本的十万倍左右，所以简单的搜索树，难以满足复杂的应用场景。

磁盘读取数据，考的是机械运动，每次读取数据花费的时间可以分成：寻道时间、旋转延迟、传输时间三个部分。寻道时间指的是磁臂移动到指定磁盘所需要的时间，主流的磁盘一般在 5ms 以下；旋转延迟指的是我们经常说的磁盘转速，比如一个磁盘 7200 转，表示的就是每分钟磁盘能转 7200 次，转换成秒也就是 120 次每秒，旋转延迟就是 1/120/2=4.17ms；传输时间指的是从磁盘读取出数据或将数据写入磁盘的时间，一般都在零点几毫秒，相对于前两个，可以忽略不计。那么访问一次磁盘的时间，即一次磁盘 I/O 的时间约等于 5+4.17=9.17ms，9ms 左右，听起来还是不错的哈，但要知道一台 500-MIPS 的机器每秒可以执行 5 亿条指令，因为指令依靠的是电的性质，换句话说，执行一次 I/O 的时间可以执行 40 万条指令，数据库动辄百万级甚至千万级的数据，每次 9ms 的时间，显然是一个灾难。

http://blog.csdn.net/mysteryhaohao/article/details/51719871

https://guptavikas.wordpress.com/2012/12/17/b-tree-index-in-mysql/

## 树

树状图是一种数据结构，它是由 n（n>=1）个有限节点组成一个具有层次关系的集合。

*   每个节点（node）有零个或多个子节点
*   没有父节点的节点称为根节点（root）
*   每一个非根节点有且只有一个父节点
*   除了根节点外，每个子节点可以分为多个不相交的子树（subtree）

概念

*   节点的度：一个节点含有的子树的个数称为该节点的度
*   叶节点或终端节点：度为 0 的节点称为叶节点
*   非终端节点或分支节点：度不为 0 的节点
*   双亲节点或父节点：若一个节点含有子节点，则这个节点称为其子节点的父节点
*   孩子节点或子节点：一个节点含有的子树的根节点称为该节点的子节点
*   兄弟节点：具有相同父节点的节点互称为兄弟节点
*   树的度：一棵树中，最大的节点的度称为树的度
*   节点的层次：从根开始定义起，根为第 1 层，根的子节点为第 2 层，以此类推
*   树的高度或深度：树中节点的最大层次
*   堂兄弟节点：双亲在同一层的节点互为堂兄弟
*   节点的祖先：从根到该节点所经分支上的所有节点
*   子孙：以某节点为根的子树中任一节点都称为该节点的子孙
*   森林：由 m（m>=0）棵互不相交的树的集合称为森林

分类

无序树：树中任意节点的子结点之间没有顺序关系,也称为自由树有序树：树中任意节点的子结点之间有顺序关系二叉树：每个节点最多含有两个子树的树称为二叉树完全二叉树满二叉树霍夫曼树：带权路径最短的二叉树称为哈夫曼树或最优二叉树

遍历表达方法

先序遍历为 ABDECF
中序遍历为 DBEAFC
后序遍历为 DEBFCA

### 哈夫曼树（Huffman Tree）

给定 n 个含有权值作为 n 个叶子结点，构造一棵二叉树，若带权路径长度达到最小，称这样的二叉树为最优二叉树，也称为哈夫曼树(Huffman Tree)。

*   哈夫曼树是带权路径长度最短的树，权值较大的结点离根较近。

## 参考

* [grantjenks/python-sortedcontainers](https://github.com/grantjenks/python-sortedcontainers):Python Sorted Container Types: Sorted List, Sorted Dict, and Sorted Set
* [Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)
* [elarity/data-structure-php](https://github.com/elarity/data-structure-php):对于数据结构和算法类的东西
* [学好这13种数据结构，应对各种编程语言（C++版）](https://mp.weixin.qq.com/s/JxQjKWBe-Dg9aCyq-USPwA)