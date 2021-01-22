# Java

* 由Sun Microsystems公司于1995年5月推出的Java面向对象程序设计语言和Java平台的总称。由James Gosling和同事们共同研发，并在1995年正式推出
* 风格十分接近C++语言。继承了C++语言面向对象技术的核心，Java舍弃了C++语言中容易引起错误的指针，改以引用取代，同时移除原C++与原来运算符重载，也移除多重继承特性，改用接口取代，增加垃圾回收器功能。
* 在Java SE 1.5版本中引入了泛型编程、类型安全的枚举、不定长参数和自动装/拆箱特性。Sun 对Java语言的解释是："Java编程语言是个简单、面向对象、分布式、解释性、健壮、安全与系统无关、可移植、高性能、多线程和动态的语言"。
* Java不同于一般的编译语言或直译语言
  - 将源代码编译成字节码，依赖各种不同平台上的虚拟机来解释执行字节码，从而实现了"一次编写，到处运行"的跨平台特性。在早期JVM中，一定程度上降低了Java程序的运行效率。但在J2SE1.4.2发布后，Java的运行速度有了大幅提升。执行Java应用程序必须安装 Java Runtime Environment，JRE，JRE内部有一个Java虚拟机（Java Virtual Machine，JVM）以及一些标准的类库（Class Library）。通过JVM才能在电脑系统执行Java应用程序（Java Application）
  - 实现跨平台性的方法是大多数编译器在进行Java语言程序的编码时候会生成一个用字节码写成的"半成品"，这个"半成品"会在Java虚拟机（解释层）的帮助下运行，虚拟机会把它转换成当前所处硬件平台的原始代码
  - Java虚拟机会打开标准库，进行数据（图片、线程和网络）的访问工作
  - 注意，尽管已经存在一个进行代码翻译的解释层，有些时候Java的字节码代码还是会被JIT编译器进行二次编译。 C++语言被用户诟病的原因之一是大多数C++编译器不支持垃圾收集机制。通常使用C++编程的时候，程序员于程序中初始化对象时，会在主机内存堆栈上分配一块内存与地址，当不需要此对象时，进行析构或者删除的时候再释放分配的内存地址。如果对象是在堆栈上分配的，而程序员又忘记进行删除，那么就会造成内存泄漏（Memory Leak）。长此以往，程序运行的时候可能会生成很多不清除的垃圾，浪费了不必要的内存空间。而且如果同一内存地址被删除两次的话，程序会变得不稳定，甚至崩溃。因此有经验的C++程序员都会在删除之后将指针重置为NULL，然后在删除之前先判断指针是否为NULL。 C++中也可以使用"智能指针"（Smart Pointer）或者使用C++托管扩展编译器的方法来实现自动化内存释放，智能指针可以在标准类库中找到，而C++托管扩展被微软的Visual C++ 7.0及以上版本所支持。智能指针的优点是不需引入缓慢的垃圾收集机制，而且可以不考虑线程安全的问题，但是缺点是如果不善使用智能指针的话，性能有可能不如垃圾收集机制，而且不断地分配和释放内存可能造成内存碎片，需要手动对堆进行压缩。除此之外，由于智能指针是一个基于模板的功能，所以没有经验的程序员在需要使用多态特性进行自动清理时也可能束手无策。 Java语言则不同，上述的情况被自动垃圾收集功能自动处理。对象的创建和放置都是在内存堆栈上面进行的。当一个对象没有任何引用的时候，Java的自动垃圾收集机制就发挥作用，自动删除这个对象所占用的空间，释放内存以避免内存泄漏。
* 甲骨文与该平台的另外两大贡献者IBM 和 Red Hat 共同做出了这个决定:选择 Eclipse 基金会作为 Java EE 的新东家

## 版本

* [Java SE](https://www.oracle.com/technetwork/java/javase)：Standard Edition 包含标准JVM和标准库
  - [OpenJDK](http://openjdk.java.net):免费的开源实现,GPL License发布，很多Linux发行版中都会包含这个Open JDK
  - Oracle JDK
    + JavaSE(J2SE)(Java2 Platform Standard Edition，java平台标准版）:从JDK 5.0开始，改名为Java SE
      - Java SE 5.0 (1.5.0)
      - Java SE 8.0 (1.8.0):从2019年1月 后续的update 开始就要收费 8u191, 8u192这样的东西，191,192就是update 的编号
      - Java SE 9
      - Java SE 10
    + 组件
      * java:其实就是JVM，运行Java程序，就是启动JVM，然后让JVM执行指定的编译后的代码
      * javac:编译器，把Java源码文件（以.java后缀结尾）编译为Java字节码文件（以.class后缀结尾）
      * jar:打包工具，把一组.class文件打包成一个.jar文件，便于发布
      * javadoc:文档生成器，从Java源码中自动提取注释并生成文档
      * jdb:debugger，用于开发阶段的运行调试
      * appletviewer：小程序浏览器，一种执行HTML文件上的Java小程序的Java浏览器。
      * Javah：产生可以调用Java过程的C过程，或建立能被Java程序调用的C过程的头文件。
      * Javap：Java反汇编器，显示编译类文件中的可访问功能和数据，同时显示字节代码含义。
      * Jconsole: Java进行系统调试和监控的工具
  - Oracle与OpenJDK
    + Oracle JDK版本将每三年发布一次，而OpenJDK版本每三个月发布一次。
    + Oracle JDK将更多地关注稳定性，它重视更多的企业级用户，而OpenJDK经常发布以支持其他性能，这可能会导致不稳定。
    + Oracle JDK支持长期发布的更改，而Open JDK仅支持计划和完成下一个发行版。
    + Oracle JDK根据二进制代码许可协议获得许可，而OpenJDK根据GPL v2许可获得许可。使用Oracle平台时会产生一些许可影响。如Oracle 宣布的那样，在没有商业许可的情况下，在2019年1月之后发布的Oracle Java SE 8的公开更新将无法用于商业，商业或生产用途。但是，OpenJDK是完全开源的，可以自由使用。
    + Oracle JDK的构建过程基于OpenJDK，因此OpenJDK与Oracle JDK之间没有技术差异。
    + 顶级公司正在使用Oracle JDK，例如Android Studio，Minecraft和IntelliJ IDEA开发工具，其中Open JDK不太受欢迎。
    + Oracle JDK具有Flight Recorder，Java Mission Control和Application Class-Data Sharing功能，Open JDK具有Font Renderer功能，这是OpenJDK与Oracle JDK之间的显着差异。
    + Oracle JDK具有良好的GC选项和更好的渲染器，而OpenJDK具有更少的GC选项，并且由于其包含自己的渲染器的分布，因此具有较慢的图形渲染器选项。
    + 在响应性和JVM性能方面，Oracle JDK与OpenJDK相比提供了更好的性能。
    + 与OpenJDK相比，Oracle JDK的开源社区较少，OpenJDK社区用户的表现优于Oracle JDK发布的功能，以提高性能。
    + 如果使用Oracle JDK会产生许可影响，而OpenJDK没有这样的问题，并且可以以任何方式使用，以满足完全开源和免费使用。
    + Oracle JDK在运行JDK时不会产生任何问题，而OpenJDK在为某些用户运行JDK时会产生一些问题。
    + 根据使用方的使用和许可协议，现有应用程序可以从Oracle JDK迁移到Open JDK，反之亦然。
    + Oracle JDK将从其10.0.X版本将收费，用户必须付费或必须依赖OpenJDK才能使用其免费版本。
    + Oracle JDK不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本。
    + Oracle JDK以前的1.0版以前的版本是由Sun开发的，后来被Oracle收购并为其他版本维护，而OpenJDK最初只基于Java SDK或JDK版本7。
    + Oracle JDK发布时大多数功能都是开源的，其中一些功能免于开源，并且根据Sun的许可授权，而OpenJDK发布了所有功能，如开源和免费。
    + Oracle JDK完全由Oracle公司开发，而Open JDK项目由IBM，Apple，SAP AG，Redhat等顶级公司加入和合作
* Java EE：Enterprise Edition Java SE的基础上加上了大量的API和库，以便方便开发Web应用、数据库、消息服务等 从2018年2月26日开始，J2EE改名为Jakarta EE
* Oracle Java SE Advanced, Java  SE Advanced Desktop, Java SE Suite:为企业级用户提供的高级工具和功能，可以监控、部署、管理企业级的Java程序
* Java ME：Micro Edition 针对嵌入式设备的“瘦身版”，Java SE的标准库无法在Java ME上使用，Java ME的虚拟机也是“瘦身版”

### 安装

* [下载JDK(Java Development Kit)](https://www.oracle.com/java/technologies/javase-downloads.html)
* 目录
  - CLASS_PATH JVM用到的一个环境变量，用来指示JVM如何搜索class,保证class文件能够在任意目录下运行.启动JVM时设置classpath才是推荐的做法,java命令传入-classpath或-cp参数
  - PATH 保证javac可以在任意目录下运行
  - 强烈不推荐在系统环境变量中设置classpath，那样会污染整个系统环境。在启动JVM时设置classpath才是推荐的做法。实际上就是给java命令传入-classpath或-cp参数
* Mac
  - 默认安装目录 `/Library/Java/JavaVirtualMachines/`
* bin目录下可执行文件：
  - java：JVM，运行Java程序，就是启动JVM，然后让JVM执行指定的编译后的代码
  - javac：编译器，用于把Java源码文件（以.java后缀结尾）编译为Java字节码文件（以.class后缀结尾）
  - jar：用于把一组.class文件打包成一个.jar文件，便于发布
  - javadoc：用于从Java源码中自动提取注释并生成文档
  - jdb：Java调试器，用于开发阶段的运行调试

```sh
# windows
JAVA_HOME C:\Program Files (x86)\Java\jdk1.8.0_91        # 要根据自己的实际路径配置
CLASSPATH .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar\;         # 记得前面有个"."
Path %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin\; # win10 path 分条添加

# ubuntu
# using the version packaged with Debian：OpenJDK 8
sudo apt-get update
sudo apt install openjdk-11-jdk
apt-get install default-jdk

# Installing the Oracle JDK
sudo apt-get install software-properties-common
sudo add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main"
sudo apt-get update
sudo apt-get install oracle-java8-installer
javac -version

sudo add-apt-repository ppa:linuxuprising/java
sudo apt install oracle-java14-installer
sudo apt-get install oracle-java14-set-default

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
# export JRE_HOME==${JAVA_HOME}/jre
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
# export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH:$PATH

## JAVA_HOME Environment Variable配置 etc/environment # 添加 JAVA_HOME="/usr/lib/jvm/java-8-oracle"
source /etc/environment
echo $JAVA_HOME

# mac ~/.bash_profile
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_144.jdk/Contents/Home
export PATH=${PATH}:$JAVA_HOME/bin
# export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export CLASS_PATH=.:"$JAVA_HOME/lib"

# 卸载
sudo rm -rf /Library/Java/JavaVirtualMachines/jdk1.8.0_40.jdk

# 或者
JAVA_HOME=$(/usr/libexec/java_home -v 1.8)
export JAVA_HOME
source .bash_profile | source .zshrc

## centos
sudo yum install java-1.8.0-openjdk
sudo yum install java-1.8.0-openjdk-devel

sudo sh -c 'for bin in /usr/lib/jvm/java-11-openjdk-amd64/bin/*; do update-alternatives --install /usr/bin/$(basename $bin) $(basename $bin) $bin 100; done'
sudo sh -c 'for bin in /usr/lib/jvm/java-11-openjdk-amd64/bin/*; do update-alternatives --set $(basename $bin) $bin; done'

# 多版本管理
sudo update-alternatives --config java | javac # 会获得程序路径

java -version

java -classpath|cp .;C:\work\project1\bin;C:\shared abc.xyz.Hello # 搜索Hello.class
```

### 执行

* 编译成Java字节码需要JDK(Java Development Kit)，因为JDK除了包含JRE，还提供了编译器、调试器等开发工具
  - JRE(Java Runtime Environment) 运行Java字节码的虚拟机JVM
* 编译型源程序->可执行程序->操作系统执行
* Java 源程序：源程序（.java）->字节码程序（.class）->**解释器执行**->操作系统执行,无法直接运行Java源码文件，原因是它需要依赖其他的库
  - 源文件:Javac 后面跟着的是java文件的文件名，例如 HelloWorld.java。 该命令用于将 java 源文件编译为 class 字节码文件
    + 一个源文件中只能有一个public类
    + 一个源文件可以有多个非public类
    + 源文件的名称应该和public类的类名保持一致。例如：源文件中public类的类名是Employee，那么源文件应该命名为Employee.java。
    + 如果一个类定义在某个包中，那么package语句应该在源文件的首行。
    + 如果源文件包含import语句，那么应该放在package语句和类定义之间。如果没有package语句，那么import语句应该在源文件中最前面。
    + import语句和package语句对源文件中定义的所有类都有效。在同一源文件中，不能给不同的类不同的包声明。
  - Java 后面跟着的是java文件中的类名

```java
//  HelloWorld.java
public class HelloWorld {
    /* 第一个Java程序
     * 它将打印字符串 Hello World
     */
    public static void main(String []args) {
        System.out.println("Hello World"); // 打印 Hello World
    }
}

javac HelloWorld.java // 编译 HelloWorld.class文件
java HelloWorld // 运行
```

## 源码构建工具 ant -> maven -> gradle

* [ant](./ant.md) 功能虽然也很强大，但是过于灵活，规范性不足，对目录结构及build.xml没有默认约定，10个程序员做同样的项目，可能最终出来的10个项目，目录结构和build.xml都不相同，而且没有统一的依赖项管理。
* [maven](./maven.md)的出现，解决了规范的问题，也顺带解决了依赖项统一管理的问题，但是规范性又太强了，基本上可以认为是一种强规范，用久了之后，感觉灵活性显略不足，而且pom.xml采用xml结构，项目大了，xml就有些冗长。
* [gradle](./gradle.md)则是综合了ant与maven的优点，吸收了ant中task的思想，然后把maven的目录规范及仓库思想也融合进来了，但是允许用户自由修改默认的规范（比如：源代码目录可以自己指定），另外配置文件采用groovy语言来书写（格式初看上去有点类似json，比较精减），注意：groovy是一门真正的【可编程】语言，而不是象css、html之类的标记性「符号」，所以从这个意义上讲，配置文件build.gradle本身就是一份源代码，这份源代码，最终交由gradle来处理执行，完成代码的构建工作。gradle的发展速度之快，是ant 与 maven所不能比拟的，看下gradle官网的文档就能感受到了，一个新兴的工具文档如此之齐全，可见大家对它的认可程度。

## JVM

* 垃圾收集器
* 类加载机制
* Class文件结构
* 参数调优
* 字节码文件
* 锁升级
* JMM
* JVM并发
* JIT
* 记录好日志
* 对程序做好性能监控
* 根据日志和性能监控数据修改程序
* 使用专业工具通过不同的JVM参数进行压测并获得最佳配置

## JDK

一套依据jvm规范实现的一套API

* 集合
* 多线程
* NIO
* 反射
* 文件操作
* Lambda语法

## 基础

* 类名：首字母应该大写。如果类名由若干单词组成，每个单词首字母应该大写，例如 MyFirstJavaClass
* 方法名：以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写
* 源文件名：必须和类名相同。当保存文件的时候，应该使用类名作为文件名保存，文件名的后缀为.java,如果文件名和类名不相同则会导致编译错误
* 包名：包名应该尽量保证小写，例如 my.first.package
* 主方法入口：所有 Java 程序由 `public static void main(String []args)` 方法开始执行
* 注释：单行注释与多行注释
* 标志符：类名、变量名以及方法名
  - 标识符都应该以字母（A-Z或者a-z）,美元符（$）、或者下划线（_）开始
  - 首字符之后可以是字母（A-Z或者a-z）,美元符（$）、下划线（_）或数字的任何字符组合
  - 关键字不能用作标识符
  - 大小写敏感

## 常量

* 在程序运行时是不能被修改
* 使用 final 关键字来修饰常量
* 大写字母表示

```java
final double PI = 3.1415927;

"two\nlines"
"\"This is in quotes\""
char a = '\u0001';
String a = "\u0001";

\ddd  // 八进制字符 (ddd)
\uxxxx  // 16进制Unicode字符 (xxxx)
```

## 变量

* 创建时，在内存中申请空间。变量为地址别名，值为存储内容
* 内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据
* 可以重新赋值，还可以赋值给其他变量 `=`是赋值语句
* 成员变量（非静态变量）：声明在类中，方法体之外的变量。创建对象时实例化。可以被类中方法、构造方法和特定类的语句块访问
  - 一个对象被实例化之后，每个实例变量的值就跟着确定
  - 对象创建时创建，对象被销毁时销毁
  - 可以声明在使用前或者使用后
  - 访问修饰符可以修饰实例变量
  - 对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见
  - 具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定
  - 可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName
* 类变量（静态变量）：声明在类中，方法体之外，必须声明为static类型
  - 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝
  - 除了被声明为常量外很少使用。常量是指声明为public/private，final和static类型的变量,初始化后不可改变
  - 储存在静态存储区,在第一次被访问时创建，在程序结束时销毁
  - 与实例变量具有相似的可见性。为了对类的使用者可见，大多数静态变量声明为public类型
  - 默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明时候、构造方法中、静态语句块中初始化
  - 访问：`ClassName.VariableName`
  - 被声明为public static final类型时，名称建议使用大写字母
* 局部变量：在方法、构造方法或者语句块中定义的变量。声明和初始化都是在方法中，方法结束后变量就会自动销毁
  - 在方法、构造方法、或者语句块被执行的时候创建，执行完成后，将会被销毁
  - 访问修饰符不能用于局部变量
  - 只在声明它的方法、构造方法或者语句块中可见
  - 在栈上分配
  - 没有默认值，所以被声明后必须经过初始化，才可以使用

## 数据类型

* 基本数据类型：CPU可以直接进行运算,字面量可以赋给任何内置类型变量
  - 整数类型：可以用十进制、16进制以及8进制方式来表示
    - byte（字节）
      + 8位、有符号，以二进制补码表示整数
      + 范围：128（-2^7）127（2^7-1）
      + 默认值 0
      + 占用空间只有 int 类型的四分之一
    - short（短整型）
      * 16 位、有符号的以二进制补码表示整数
      * 范围：-32768（-2^15） 32767（2^15 - 1）
      * 默认值 0
    + int（整型）Integer
      * 32位、有符号的以二进制补码表示整数
      * 范围：-2,147,483,648（-2^31） 2,147,483,647（2^31 - 1）
      * 整型变量默认 int 类型
      * 默认值 0
    + long（长整型）Long
      * 64 位、有符号的以二进制补码表示整数
      * 范围： -9,223,372,036,854,775,808（-2^63） 9,223,372,036,854,775,807（2^63 -1）
      * 主要使用在需要比较大整数的系统上
      * 默认值 0L
  - 浮点型
    + float（单精度浮点）Float
      * 单精度、32位、符合IEEE 754标准的浮点数
      * 在储存大型浮点数组时候可节省内存空间 3.4x1038
      * 默认值 0.0f
      * 不能用来表示精确的值，如货币
    + double（双精度浮点）Double
      * 数据类型是双精度、64 位、符合IEEE 754标准的浮点数
      * 浮点数默认类型为double 1.79x10308
      * 同样不能表示精确的值，如货币
      * 默认值是 0.0d
  - boolean
    + 一位信息,总是关系运算的计算结果,JVM内部会把boolean表示为4字节整数
    + 两个取值：true 和 false
    + 默认值是 false
  - char
    + 一个单一 16 位 Unicode 字符
    + 范围 \u0000（即为0）~ \uffff（即为65,535）
    + 可以储存任何字符
    + 使用单引号'，且仅有一个字符
* 类型转换
  - 自动类型转换
    * 整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算.
    * 优先级：byte,short,char—> int —> long—> float —> double
    + 不能对boolean类型进行类型转换。
    + 不能把对象类型转换成不相关类的对象。
    + 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。
    + 转换过程中可能导致溢出或损失精度
    + 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入
    + 必须满足转换前的数据类型的位数要低于转换后的数据类型，例如: short数据类型的位数为16位，就可以自动转换位数为32的int类型，同样float数据类型的位数为32，可以自动转换为64位的double类型。
  - 强制转换:条件是转换的数据类型必须兼容 `(type)value`
  - 隐含强制类型转换
    + 整数的默认类型是 int
    + 浮点型不存在这种情况，因为在定义 float 类型时必须在数字后面跟上 F 或者 f
  - 引用数据类型
    + 非常类似于C/C++的指针。引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型。变量一旦声明后，类型就不能被改变了
    + 对象、数组都是引用数据类型
    + 所有引用类型的默认值都是null
    + 一个引用变量可以用来引用任何与之兼容的类型

```java
type identifier [ = value][, identifier [= value] ...] ;

int d = 3, e = 4, f = 5; // 声明三个整数并赋予初值
double d1 = 123.4;
boolean one = true;
char letter = 'A';
char a = '\u0001'; // 可以包含任何Unicode字符
String s = "runoob";  // 声明并初始化字符串 s

Byte.SIZE
Byte.MIN_VALUE
Byte.MAX_VALUE
Integer.SIZE
Integer.MIN_VALUE
Integer.MAX_VALUE
Character.SIZE

int decimal = 100;
int octal = 0144;
int hexa =  0x64;

byte a = 68;
char a = 'A'

int i =128;
byte b = (byte)i; // 值 128 时候就会导致溢出
(int)23.7 == 23;
(int)-45.89f == -45

int i1 = 123;
byte b = (byte)i1;

int a[] = new int[10]; //定义了一个长度是10的int类型数组
```

## 枚举

## HashMap

* TreeMap<K,V>
  - Key值是要求实现java.lang.Comparable，所以迭代的时候TreeMap默认是按照Key值升序排序的
  - 实现是基于红黑树结构,没有调优选项，因为该树总处于平衡状态
    + TreeMap()：构建一个空的映像树
    + TreeMap(Map m): 构建一个映像树，并且添加映像m中所有元素
    + TreeMap(Comparator c): 构建一个映像树，并且使用特定的比较器对关键字进行排序
    + TreeMap(SortedMap s): 构建一个映像树，添加映像树s中所有映射，并且使用与有序映像s相同的比较器排序
  - 适用于按自然顺序或自定义顺序遍历键（key）
  - 通过自定义的比较器来实现降序：实现Comparator接口，重写compare方法，有两个参数，这两个参数通过调用compareTo进行比较，而compareTo默认规则是：
    + 如果参数字符串等于此字符串，则返回 0 值；
    + 如果此字符串小于字符串参数，则返回一个小于 0 的值；
    + 如果此字符串大于字符串参数，则返回一个大于 0 的值
    + 在返回时多添加了个负号，就将比较的结果以相反的形式返回
* HashMap<K,V>
  - Key值实现散列hashCode()，分布是散列的、均匀的，不支持排序
  - 数据结构主要是桶(数组)，链表或红黑树
  - 基于哈希表实现。使用HashMap要求添加的键类明确定义了hashCode()和equals()[可以重写hashCode()和equals()]，为了优化HashMap空间的使用，可以调优初始容量和负载因子
    + HashMap(): 构建一个空的哈希映像
    + HashMap(Map m): 构建一个哈希映像，并且添加映像m的所有映射
    + HashMap(int initialCapacity): 构建一个拥有特定容量的空的哈希映像
    + HashMap(int initialCapacity, float loadFactor): 构建一个拥有特定容量和加载因子的空的哈希映像
  - 适用于在Map中插入、删除和定位元素
* 线程安全
  - HashMap继承AbstractMap抽象类。 AbstractMap抽象类： 覆盖了equals()和hashCode()方法以确保两个相等映射返回相同的哈希码。如果两个映射大小相等、包含同样的键且每个键在这两个映射中对应的值都相同，则这两个映射相等。映射的哈希码是映射元素哈希码的总和，其中每个元素是Map.Entry接口的一个实现。因此，不论映射内部顺序如何，两个相等映射会报告相同的哈希码。
  - TreeMap继承自SortedMap接口。SortedMap接口： 它用来保持键的有序顺序。SortedMap接口为映像的视图(子集)，包括两个端点提供了访问方法。除了排序是作用于映射的键以外，处理SortedMap和处理SortedSet一样。添加到SortedMap实现类的元素必须实现Comparable接口，否则您必须给它的构造函数提供一个Comparator接口的实现。TreeMap类是它的唯一一个实现。

```java
public class MapTest {

    public static void main(String[] args) {
        //初始化自定义比较器
        MyComparator comparator = new MyComparator();
        //初始化一个map集合
        Map<String,String> map = new TreeMap<String,String>(comparator);
        //存入数据
        map.put("a", "a");
        map.put("b", "b");
        map.put("f", "f");
        map.put("d", "d");
        map.put("c", "c");
        map.put("g", "g");
        //遍历输出
        Iterator iterator = map.keySet().iterator();
        while(iterator.hasNext()){
            String key = (String)iterator.next();
            System.out.println(map.get(key));
        }
    }

    static class MyComparator implements Comparator{

        @Override
        public int compare(Object o1, Object o2) {
            // TODO Auto-generated method stub
            String param1 = (String)o1;
            String param2 = (String)o2;
            return -param1.compareTo(param2);
        }

    }

}
```

## DelayQueue 延时任务

* 定时任务 vs 延时任务
  - 定时任务有固定的触发时间（比如每天的凌晨2点执行），延迟任务的执行时间不固定，严格依赖于业务事件的触发时间（比如：自动确认收货是在卖家发货那个时刻往后延15天）
  - 定时任务有执行周期，而延迟任务在某事件触发后一段时间内执行，一般是一次性的，没有执行周期
  - 定时任务一般执行的是批处理操作多个任务，而延迟任务一般是单个任务
* JDK 延迟队列
  - 无界阻塞队列，支持延时获取元素，队列中的元素必须实现 Delayed 接口，并重写 getDelay(TimeUnit) 和 compareTo(Delayed) 方法
    + 由于采用无界阻塞队列，占用本地内存，如果任务太多的话，很容易产生内存溢出（OOM）的风险
    + 发生系统重启等情况会导致内存数据丢失，需要考虑将数据重新预热到缓存的操作，有额外实现成本
  - 基于调度的线程池ScheduledExecutorService
    + schedule。单次延迟任务。
    + scheduleAtFixedRate。基于固定时间间隔进行循环延迟任务。如果上一次任务还没有结束，会等它结束后，才执行下一次任务，取间隔时间和任务执行时间的最大值。
    + scheduleWithFixedDelay。取决于每次任务执行的时间长短，是基于不固定时间间隔进行循环延迟任务，每次执行时间为上一次任务结束起向后推一个时间间隔，即每次执行时间为：initialDelay, initialDelay+executeTime+delay, initialDelay+2executeTime+2delay
* 数据库轮询
  - 创建一个超时记录表，当业务执行时会插入一条记录到mysql表，并指定目标执行时间
  - 启动一个定时任务，一般会采用 Quartz 框架来实现， 无限循环扫描该表记录，如果发现目标执行时间小于当前时间，会提取记录执行并修改状态。为什么要先修改状态呢？主要是考虑多线程并发问题，毕竟执行超时任务（如：自动确认收货）也要花费时间，待超时任务执行结束后，再修改状态标记为“已完成”。
  - 缺点：采用主动发现机制，执行时间严重依赖扫描频率，如果定时任务配置的时间周期太长，那么任务真正执行时间可能会有较大延迟。反之，如果扫描周期时间太短，扫描频率过快，数据库的压力会比较大，还存在较大的系统资源浪费
* Redis 有序集合
  - Zset支持按score对value值排序，这里的score可以采用超时记录的目标执行时间。也就是说集合列表中的记录是按执行时间排好序，只需要取小于当前时间的即可。
* pulsa 消息
* ActiveMQ作为一个开箱即用的中间件，提供了扩展配置属性支持延迟消息
* Netty
  - 时间轮是一种高效来利用线程资源来进行批量化调度的一种调度模型。把大批量的调度任务全部都绑定到同一个的调度器上面，使用这一个调度器来进行所有任务的管理（manager），触发（trigger）以及运行（runnable）。能够高效的管理各种延时任务，周期任务，通知任务等等。
  - 时间轮调度器的时间精度可能不是很高，对于精度要求特别高的调度任务可能不太适合。因为时间轮算法的精度取决于，时间段“指针”单元的最小粒度大小

## 运算符

* 算术 + - * / % ++ --
* 关系  == != > < >= <=
* 位 作用在所有的位上，并且按位运算
  - & 与
  - | 或
  - ^：如果相对应位值相同，则结果为0，否则为1
  - ~：按位取反运算符翻转操作数的每一位，即0变成1，1变成0
  - <<  按位左移运算符。左操作数按位左移右操作数指定的位数
  - />>  按位右移运算符。左操作数按位右移右操作数指定的位数
  - />>>   按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充。
* 逻辑 && || ！
  - 当使用与逻辑运算符时，在两个操作数都为true时，结果才为true，但是当得到第一个操作为false时，其结果就必定是false，这时候就不会再判断第二个操作了
  - 逻辑或时，有一个为true,就通过
* 赋值 = != += -= /= (%)= <<= >>= &= ^= |=
* 条件（?:）
* instanceof :用于操作对象实例，检查该对象是否是一个特定类型（类类型或接口类型）
* 优先级：属性》一元〉乘法》加减〉移位》关系〉是否相等》位与〉位异或》位或〉逻辑与》逻辑或〉条件》赋值〉逗号

```
( Object reference variable ) instanceof  (class/interface type)
String name = "James";
boolean result = name instanceof String;

// 优先级
() [] .(点操作符)
+ + - ！〜 // 一元
* /％ // 乘性
+ -
>> >>>  <<
>> = << =
==  !=
＆
^
|
&&
||
？：  // 从右到左
= + = - = * = / =％= >> = << =＆= ^ = | = // 从右到左
，
```

## 控制语句

* 条件
  - if
  - switch
    + 变量类型： byte、short、int 或者 char。从 Java SE 7 开始，支持字符串 String 类型
    + 拥有多个 case 语句。每个 case 后面跟一个要比较的值和冒号。
    + case 语句中的值的数据类型必须与变量的数据类型相同，而且只能是常量或者字面常量。
    + 当变量的值与 case 语句的值相等时，那么 case 语句之后的语句开始执行，直到 break 语句出现才会跳出 switch 语句。
    + case 语句不必须要包含 break 语句。如果没有 break 语句出现，程序会继续执行下一条 case 语句，直到出现 break 语句。
    + 可以包含一个 default 分支，该分支一般是 switch 语句的最后一个分支（可以在任何位置，但建议在最后一个）。
    + default 在没有 case 语句的值和变量值相等的时候执行。default 分支不需要 break 语句。
  - 嵌套
* 循环
  - while
  - do...while
  - for
* break 跳出整个语句块。跳出最里层的循环，并且继续执行该循环下面的语句
* continue 适用于任何循环控制结构中。作用是让程序立刻跳转到下一次循环的迭代。
* return

### Number and Math

* Java 语言为每一个内置数据类型提供了对应的包装类
  - 由编译器特别支持的包装称为装箱，所以当内置数据类型被当作对象使用的时候，编译器会把内置类型装箱为包装类。
  - 相似的，编译器也可以把一个对象拆箱为内置类型。Number 类属于 java.lang 包。
* 所有的包装类（Integer、Long、Byte、Double、Float、Short）都是抽象类 Number 的子类
* Math 包含了用于执行基本数学运算的属性和方法
  - xxxValue() 方法用于将 Number 对象转换为 xxx 数据类型的值
  - random() 方法用于返回一个随机数，随机数范围为 0.0 =< Math.random < 1.0。
  - compareTo() 方法用于将 Number 对象与方法的参数进行比较。可用于比较 Byte, Long, Integer等。该方法用于两个相同数据类型的比较，两个不同类型的数据不能用此方法来比较
  - equals() 方法用于判断 Number 对象与方法的参数进是否相等
  - valueOf() 方法用于返回给定参数的原生 Number 对象值，参数可以是原生数据类型, String等。该方法可以接收两个参数一个是字符串，一个是基数
  - toString() 方法用于返回以一个字符串表示的 Number 对象值。
  - parseInt() 方法用于将字符串参数作为有符号的十进制整数进行解析。如果方法有两个参数， 使用第二个参数指定的基数，将字符串参数解析为有符号的整数。
  - abs() 返回参数的绝对值
  - ceil() 返回大于等于( >= )给定参数的的最小整数
  - floor() 返回小于等于（<=）给定参数的最大整数
  - round():表示四舍五入，算法为 Math.floor(x+0.5)，即将原来的数字加上 0.5 后再向下取整，所以，Math.round(11.5) 的结果为12，Math.round(-11.5) 的结果为-11
  - rint() 方法返回最接近参数的整数值
  - min() 方法用于返回两个参数中的最小值
  - max() 返回两个参数中的最大值
  - exp() 返回自然数底数e的参数次方
  - log() 方法用于返回参数的自然数底数的对数值
  - double pow(double base, double exponent) 方法用于返回第一个参数的第二个参数次方。
  - sqrt() 求参数的算术平方根
  - sin() 方法用于返回指定double类型参数的正弦值
  - cos() 方法用于返回指定double类型参数的余弦值
  - tan() 方法用于返回指定double类型参数的正切值
  - asin() 求指定double类型参数的反正弦值
  - acos() 求指定double类型参数的反余弦值
  - atan() 求指定double类型参数的反正切值
  - atan2() 方法用于将矩形坐标 (x, y) 转换成极坐标 (r, theta)，返回所得角 theta。该方法通过计算 y/x 的反正切值来计算相角 theta，范围为从 -pi 到 pi。
  - toDegrees() 将参数转化为角度
  - toRadians() 将角度转换为弧度

### Character

用于对单个字符进行操作。 在对象中包装一个基本类型 char 的值.常会遇到需要使用对象，而不是内置数据类型的情况。为了解决这个问题，Java语言为内置数据类型char提供了包装类Character类

* 在某些情况下，Java编译器会自动创建一个Character对象
* 将一个char类型的参数传递给需要一个Character类型参数的方法时，那么编译器会自动地将char类型参数转换为Character对象。 这种特征称为装箱，反过来称为拆箱。
* 打印语句遇到一个转义序列时，编译器可以正确地对其进行解释
* 方法
  - isLetter() 是否是一个字母
  - isDigit() 是否是一个数字字符
  - isWhitespace() 是否是一个空白字符
  - isUpperCase() 是否是大写字母
  - isLowerCase() 是否是小写字母
  - toUpperCase() 指定字母的大写形式
  - toLowerCase() 指定字母的小写形式
  - toString() 返回字符的字符串形式，字符串的长度仅为1

```
char ch = 'a';
// Unicode 字符表示形式
char uniChar = '\u039A';
// 字符数组
char[] charArray ={ 'a', 'b', 'c', 'd', 'e' };

Character ch = new Character('a');

// 原始字符 'a' 装箱到 Character 对象 ch 中
Character ch = 'a';
// 原始字符 'x' 用 test 方法装箱 返回拆箱的值到 'c'
char c = test('x');

\t  // 在文中该处插入一个tab键
\b  // 在文中该处插入一个后退键
\n  // 在文中该处换行
\r  // 在文中该处插入回车
\f  // 在文中该处插入换页符
\'  // 在文中该处插入单引号
\"  // 在文中该处插入双引号
\\  // 在文中该处插入反斜杠

Character.isLetter('c') // true
Character.isLetter('5') // false
Character.isDigit('5') // true
Character.isWhitespace(' ') // true
Character.isWhitespace('\n') // true
Character.isWhitespace('\t') // true
Character.isUpperCase('C') // true
Character.isLowerCase('c') // true
Character.toUpperCase('a') // A
Character.toLowerCase('A') // a
Character.toString('a') // a
Character.toString('A') // A
```

### String类

* 字符串属于对象，Java 提供了 String 类来创建和操作字符串
* String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了
* 方法
  - char charAt(int index)返回指定索引处的 char 值。
  - int compareTo(Object o)把这个字符串和另一个对象比较。
    + 字符串与对象进行比较。
  - int compareTo(String anotherString)按字典顺序比较两个字符串。
    + 先比较对应字符的大小(ASCII码顺序),如果第一个字符和参数的第一个字符不等,结束比较,返回他们之间的差值,如果第一个字符和参数的第一个字符相等,则以第二个字符和参数的第二个字符做比较,以此类推,直至比较的字符或被比较的字符不一样
    + 如果参数字符串等于此字符串，则返回值 0；
    + 如果此字符串小于字符串参数，则返回一个小于 0 的值；
    + 如果此字符串大于字符串参数，则返回一个大于 0 的值。
  - int compareToIgnoreCase(String str)按字典顺序比较两个字符串，不考虑大小写。
  - String concat(String str)将指定字符串连接到此字符串的结尾。
  - boolean contentEquals(StringBuffer sb)当且仅当字符串与指定的StringBuffer有相同顺序的字符时候返回真。
  - static String copyValueOf(char[] data)返回指定数组中表示该字符序列的 String。
  - static String copyValueOf(char[] data, int offset, int count)返回指定数组中表示该字符序列的 String。
  - boolean endsWith(String suffix)测试此字符串是否以指定的后缀结束。
  - boolean equals(Object anObject)将此字符串与指定的对象比较。
  - boolean equalsIgnoreCase(String anotherString)将此 String 与另一个 String 比较，不考虑大小写。
  - byte[] getBytes()使用平台的默认字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。
  - byte[] getBytes(String charsetName)使用指定的字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。
  - void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)将字符从此字符串复制到目标字符数组。
  - int hashCode()返回此字符串的哈希码。
  - int indexOf(int ch)返回指定字符在此字符串中第一次出现处的索引。
  - int indexOf(int ch, int fromIndex)返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。
  - int indexOf(String str)返回指定子字符串在此字符串中第一次出现处的索引。
  - int indexOf(String str, int fromIndex)返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。
  - String intern()返回字符串对象的规范化表示形式。
  - int lastIndexOf(int ch)返回指定字符在此字符串中最后一次出现处的索引。
  - int lastIndexOf(int ch, int fromIndex)返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索。
  - int lastIndexOf(String str)返回指定子字符串在此字符串中最右边出现处的索引。
  - int lastIndexOf(String str, int fromIndex)返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。
  - int length()返回此字符串的长度。
  - boolean matches(String regex)告知此字符串是否匹配给定的正则表达式。
  - boolean regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)测试两个字符串区域是否相等。
  - boolean regionMatches(int toffset, String other, int ooffset, int len)测试两个字符串区域是否相等。
  - String replace(char oldChar, char newChar)返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。
  - String replaceAll(String regex, String replacement)使用给定的 replacement 替换此字符串所有匹配给定的正则表达式的子字符串。
  - String replaceFirst(String regex, String replacement)使用给定的 replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。
  - String[] split(String regex)根据给定正则表达式的匹配拆分此字符串。
  - String[] split(String regex, int limit)根据匹配给定的正则表达式来拆分此字符串。
  - boolean startsWith(String prefix)测试此字符串是否以指定的前缀开始。
  - boolean startsWith(String prefix, int toffset)测试此字符串从指定索引开始的子字符串是否以指定前缀开始。
  - CharSequence subSequence(int beginIndex, int endIndex)返回一个新的字符序列，它是此序列的一个子序列。
  - String substring(int beginIndex)返回一个新的字符串，它是此字符串的一个子字符串。
  - String substring(int beginIndex, int endIndex)返回一个新字符串，它是此字符串的一个子字符串。
  - char[] toCharArray()将此字符串转换为一个新的字符数组。
  - String toLowerCase()使用默认语言环境的规则将此 String 中的所有字符都转换为小写。
  - String toLowerCase(Locale locale)使用给定 Locale 的规则将此 String 中的所有字符都转换为小写。
  - String toString()返回此对象本身（它已经是一个字符串！）。
  - String toUpperCase()使用默认语言环境的规则将此 String 中的所有字符都转换为大写。
  - String toUpperCase(Locale locale)使用给定 Locale 的规则将此 String 中的所有字符都转换为大写。
  - String trim()返回字符串的副本，忽略前导空白和尾部空白。
  - static String valueOf(primitive data type x)返回给定data type类型x参数的字符串表示形式。

```java
// 初始化字符串
String greeting = "Hello World!";
char[] helloArray = { 'r', 'u', 'n', 'o', 'o', 'b'};
String helloString = new String(helloArray);

greeting.length();
string1.concat(string2);
"Hello," + " World" + "!"

String fs;
fs = String.format("浮点型变量的值为 " +
                   "%f, 整型变量的值为 " +
                   " %d, 字符串变量的值为 " +
                   " %s", floatVar, intVar, stringVar);

String s = "www.runoob.com";
s.charAt(8); // o
String str1 = "Strings";
String str2 = "Strings";
String str3 = "Strings123";
str1.compareTo( str2 ); // 0
str2.compareTo( str3 ); // -3
str3.compareTo( str1 ); // 3
```

## Object-oriented programming OOP

* 包 package
  - Import语句就是用来提供一个合理的路径，使得编译器可以找到某个类
* 类 class
  - 描述一类对象的行为和状态的模板, a blueprint using which you can create as many objects as you like.
  - 静态属性：声明在类中，方法体之外
    + 声明为static类型
  - 静态方法
  - 普通属性 fields：定义在类中，方法体外变量
    + 创建对象时实例化
    + 可以被类中方法、构造方法和特定类的语句块访问
  - 普通方法块
  - 构造方法 Constructor
    + 每个类都有构造方法。如果没有显式定义构造方法，JVM 自动生成一个构造方法
    + 创建对象时，至少要调用一个构造方法
    + 构造方法名称必须与类同名
    + 不加任何参数的构造方法为默认构造方法
  - Parameterized constructor
  - 局部变量：在方法、构造方法或者语句块中定义
    + 声明和初始化都是在方法中
    + 方法结束后，变量就会自动销毁
* 对象 Object：对象是类的一个实例，有状态和行为,用关键字new来创建一个新的对象
  - 声明：声明一个对象，包括对象名称和对象类型。
  - 实例化：使用关键字new来创建一个对象。
  - 初始化：使用new创建对象时，会调用构造方法初始化对象。
  - states
  - behaviors
  - Message passing:One object interacts with another object by invoking methods on that object. It is also referred to as Method
* Abstraction:a process where you show only “relevant” data and “hide” unnecessary details of an object from the user.
* Encapsulation:binding object state(fields) and behaviour(methods) together
  - Make the instance variables private so that they cannot be accessed directly from outside the class. You can only set and get values of these variables through the methods of the class
  - Have getter and setter methods in the class to set and get the values of the fields
* 继承 Inheritance
  - a process of defining a new class based on an existing class by extending its common data members and methods.
  - Inheritance allows us to reuse of code, it improves reusability in your java application.
  - The parent class is called the base class or super class. The child class that extends the base class is called the derived class or sub class or child class.
  - 可以重用已存在类的所有非 private 属性和方法
  - 被继承的类称为超类（super class），派生类称为子类（subclass）
  - 父类中声明为 public 的方法在子类中也必须为 public
  - 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。
  - 父类中声明为 private 的方法，不能够被继承
* Polymorphism
  - perform a single action in different ways
  - Static Polymorphism:resolved during compiler time
    + Method overloading
      * have more than one methods with same name in a class that differs in signature
      * can be considered as static polymorphism example
  - Dynamic Polymorphism:Dynamic Method Dispatch
    + a process in which a call to an overridden method is resolved at runtime rather, thats why it is called runtime polymorphism.
* 重载：重载方法都有独一无二参数列表
  - 条件
    + 方法名称必须相同
    + 参数列表必须不同（个数不同、类型不同、参数类型排列顺序不同等）
    + 返回类型可以相同也可以不相同，仅仅返回类型不同不足以成为方法的重载
    + 发生在编译时的，因为编译器可以根据参数的类型来选择使用哪个方法
  - 构造函数重载
  - 方法重载
* 重写：重写描述是对子类和父类之间的。重载指的是同一类中的
  - 重写方法必须要和父类保持一致，包括返回值类型,方法名,参数列表 也都一样
  - 重写方法可以使用 @Override 注解来标识
  - 子类中重写方法的访问权限不能低于父类中方法的访问权限
* 抽象类 Abstract Class
  - Abstract method
    + A method that is declared but not defined. Only method signature no body.
    + Declared using the abstract keyword
    + These cannot be abstract
      * Constructors
      * Static methods
      * Private methods
      * Methods that are declared “final”
  - An abstract class outlines the methods but not necessarily implements all the methods.
  - 如果一个类包含抽象方法，那么该类一定要声明为抽象类
  - 一种没有任何实现方法，方法体实现由子类提供
  - 抽象方法不能被声明成 final 和 static。
  - 任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类
  - 如果一个类包含若干个抽象方法，那么该类必须声明为抽象类
  - 可以不包含抽象方法
  - 抽象方法的声明以分号结尾，例如：public abstract sample();
* 接口 interface
  - a blueprint of a class
  - 对象间相互通信协议
  - 只定义派生要用到方法，具体实现完全取决于派生类
  - 使用默认访问修饰符声明的变量和方法，对同一个包内的类是可见的
  - 变量都隐式声明为 public static final
  - 方法默认情况下访问权限为 public
  - 不能被实例化，不能有任何构造方法
  - 一个类中有抽象方法，那么这个类一定是抽象类,使用关键字 abstract 修饰的方法一定是抽象方法，具有抽象方法的类一定是抽象类
* Generalization and Specialization
* 访问控制修饰符
  - private:在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
    + 声明为 private 的方法、变量和构造方法只能被所属类访问
    + 声明为私有访问类型的变量只能通过类中公共的 getter 方法被外部类访问
    + 主要用来隐藏类的实现细节和保护类的数据
  - public:对所有类可见。使用对象：类、接口、变量、方法
    + 如果几个相互访问的 public 类分布在不同的包中，则需要导入相应 public 类所在的包。
    + 由于类的继承性，类所有的公有方法和变量都能被其子类继承。
  - protected:对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
    + 子类与基类在同一包中：被声明为 protected 的变量、方法和构造器能被同一个包中的任何其他类访问；
    + 子类与基类不在同一包中：那么在子类中，子类实例可以访问其从基类继承而来的 protected 方法，而不能访问基类实例的protected方法。
* 非访问控制修饰符
  - static:修饰类方法和类变量
    + 静态变量：关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝
    + 静态方法不能使用类的非静态变量。
  - final:用来修饰类、方法和变量
    - 修饰的类不能够被继承
    - 修饰的方法可以被子类继承，但是不能被子类修改,防止该方法的内容被修改
    - 修饰的变量为常量，是不可修改的,必须显式指定初始值 常和 static 修饰符一起使用来创建类常量。
  - abstract:用来创建抽象类和抽象方法
    + 抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充
    + 一个类不能同时被 abstract 和 final 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类
  - synchronized:同一时间只能被一个线程访问,可以应用于四个访问修饰符
  - ransient:序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。
    - 该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。
  - volatile
    - 在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。
    - 当成员变量发生变化时，会强制线程将变化值回写到共享内存。
    - 在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。
    - 一个 volatile 对象引用可能是 null

```java
// 命令编译器载入 java_installation/java/io路径下的所有类
import java.io.*;

abstract class Caravan{
   private double price;
   private String model;
   private String year;
   public abstract void goFast(); //抽象方法
   public abstract void changeColor();
}

public synchronized void showDetails(){
.......
}

public transient int limit = 55;   // 不会持久化

// 在一个线程调用 run() 方法（在 Runnable 开启的线程），在另一个线程调用 stop() 方法。 如果 第一行 中缓冲区的 active 值被使用，那么在 第二行 的 active 值为 false 时循环不会停止。但是以上代码中我们使用了 volatile 修饰 active，所以该循环会停止。
public class MyRunnable implements Runnable
{
    private volatile boolean active;
    public void run()
    {
        active = true;
        while (active) // 第一行
        {
            // 代码
        }
    }
    public void stop()
    {
        active = false; // 第二行
    }
}

public class Puppy{
   int puppyAge;
   public Puppy(String name){
      // 这个构造器仅有一个参数：name
      System.out.println("小狗的名字是 : " + name );
   }

   public void setAge( int age ){
       puppyAge = age;
   }

   public int getAge( ){
       System.out.println("小狗的年龄为 : " + puppyAge );
       return puppyAge;
   }

   public static void main(String []args){
      /* 创建对象 */
      Puppy myPuppy = new Puppy( "tommy" );
      /* 通过方法来设定age */
      myPuppy.setAge( 2 );
      /* 调用另一个方法获取age */
      myPuppy.getAge( );
      /*你也可以像下面这样访问成员变量 */
      System.out.println("变量值 : " + myPuppy.puppyAge );
   }
}

// IS-A & HAS-A Relationships
public class Vehicle{ }
public class Car extends Vehicle{
   private License myCarLicense;
}
```

## 容器

* Iterable 接口:允许对象成为 for-each 循环的目标
* Collection 是一个顶层接口，用来定义集合的约定
  - List
  - Set 对add、equals、hashCode  方法提供了额外的标准
    + SortedSet 接口直接继承于 Set 接口，使用 Comparable 对元素进行自然排序或者使用 Comparator 在创建时对元素提供定制的排序规则。set 的迭代器将按升序元素顺序遍历集合。
  - Queue 用来在处理之前保持元素的访问次序。除了 Collection 基础的操作之外，队列提供了额外的插入，读取，检查操作。
* Map 一个支持 key-value 存储的对象，不能包含重复的 key，每个键最多映射一个值。这个接口代替了Dictionary 类，Dictionary 是一个抽象类而不是接口。
* ArrayList 实现了 List 接口的可扩容数组(动态数组)，内部基于数组实现  `public class ArrayList<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, java.io.Serializable {...}`
  - 可以实现所有可选择的列表操作，允许所有的元素，包括空值。ArrayList 还提供了内部存储 list 的方法，它能够完全替代 Vector，只有一点例外，ArrayList 不是线程安全的容器。
  - 有一个容量的概念，这个数组的容量就是 List 用来存储元素的容量
  - 不是线程安全的容器，如果多个线程中至少有两个线程修改了 ArrayList 的结构的话就会导致线程安全问题，作为替代条件可以使用线程安全的 List，应使用 Collections.synchronizedList 。
  - 具有 fail-fast 快速失败机制，能够对 ArrayList 作出失败检测。当在迭代集合的过程中该集合在结构上发生改变的时候，就有可能会发生 fail-fast，即抛出 ConcurrentModificationException异常
* Vector
  - 同 ArrayList 一样，都是基于数组实现的
  - Vector 是一个线程安全的容器，它对内部的每个方法都简单粗暴的上锁，避免多线程引起的安全性问题，但是通常这种同步方式需要的开销比较大，因此，访问元素的效率要远远低于 ArrayList。
  - ArrayList 扩容后的数组长度会增加 50%，而 Vector 的扩容长度后数组会增加一倍。
* LinkedList 双向链表，允许存储任何元素(包括 null )
  - 所有的操作都可以表现为双向性的，索引到链表的操作将遍历从头到尾，视哪个距离近为遍历顺序。
  - 注意这个实现也不是线程安全的，如果多个线程并发访问链表，并且至少其中的一个线程修改了链表的结构，那么这个链表必须进行外部加锁。或者使用
* Stack
  - 继承了 Vector 类，提供了通常用的 push 和 pop 操作，以及在栈顶的 peek 方法，测试 stack 是否为空的 empty 方法，和一个寻找与栈顶距离的 search 方法
  - 一个更完善，可靠性更强的 LIFO 栈操作由 Deque 接口和他的实现提供
* HashSet 是 Set 接口的实现类，由哈希表支持(实际上 HashSet 是 HashMap 的一个实例)。它不能保证集合的迭代顺序。这个类允许 null 元素
  - 这个实现不是线程安全的。如果多线程并发访问 HashSet，并且至少一个线程修改了set，必须进行外部加锁。或者使用 Collections.synchronizedSet() 方法重写。
  - 支持 fail-fast 机制
* TreeSet 一个基于 TreeMap 的 NavigableSet 实现。这些元素使用他们的自然排序或者在创建时提供的Comparator 进行排序，具体取决于使用的构造函数。
  - 此实现为基本操作 add,remove 和 contains 提供了 log(n) 的时间成本。
  - 注意这个实现不是线程安全的。如果多线程并发访问 TreeSet，并且至少一个线程修改了 set，必须进行外部加锁。或者使用
* LinkedHashSet 继承于 Set接口的 Hash 表和 LinkedList 的实现。这个实现不同于 HashSet 的是它维护着一个贯穿所有条目的双向链表。此链表定义了元素插入集合的顺序。注意：如果元素重新插入，则插入顺序不会受到影响。
  - LinkedHashSet 有两个影响其构成的参数：初始容量和加载因子。它们的定义与 HashSet 完全相同。但请注意：对于 LinkedHashSet，选择过高的初始容量值的开销要比 HashSet 小，因为 LinkedHashSet 的迭代次数不受容量影响。
  - 注意 LinkedHashSet 也不是线程安全的，如果多线程同时访问 LinkedHashSet，必须加锁，或者通过使用
  - 该类也支持fail-fast机制
* PriorityQueue:AbstractQueue 的实现类，优先级队列的元素根据自然排序或者通过在构造函数时期提供Comparator 来排序，具体根据构造器判断。PriorityQueue 不允许 null 元素。
  - 队列的头在某种意义上是指定顺序的最后一个元素。队列查找操作 poll,remove,peek 和 element 访问队列头部元素。
    -优先级队列是无限制的，但具有内部 capacity，用于控制用于在队列中存储元素的数组大小。
    -该类以及迭代器实现了 Collection、Iterator 接口的所有可选方法。这个迭代器提供了 iterator() 方法不能保证以任何特定顺序遍历优先级队列的元素。如果你需要有序遍历，考虑使用 Arrays.sort(pq.toArray())。
    -注意这个实现不是线程安全的，多线程不应该并发访问 PriorityQueue 实例如果有某个线程修改了队列的话，使用线程安全的类 PriorityBlockingQueu
* HashMap 利用哈希表原理来存储元素的集合，并且允许空的 key-value 键值对。HashMap 是非线程安全的，也就是说在多线程的环境下，可能会存在问题，而 Hashtable 是线程安全的容器。HashMap 也支持 fail-fast 机制。HashMap 的实例有两个参数影响其性能：初始容量 和加载因子。可以使用 Collections.synchronizedMap(new HashMap(...)) 来构造一个线程安全的 HashMap。

* TreeMap 类

  - 一个基于 NavigableMap 实现的红黑树。这个 map 根据 key 自然排序存储，或者通过 Comparator 进行定制排序。
  - TreeMap 为 containsKey,get,put 和remove方法提供了 log(n) 的时间开销。
  - 注意这个实现不是线程安全的。如果多线程并发访问 TreeMap，并且至少一个线程修改了 map，必须进行外部加锁。这通常通过在自然封装集合的某个对象上进行同步来实现，或者使用 SortedMap m = Collections.synchronizedSortedMap(new TreeMap(...))。
  - 这个实现持有fail-fast机制。

* LinkedHashMap 类

  - LinkedHashMap 是 Map 接口的哈希表和链表的实现。这个实现与 HashMap 不同之处在于它维护了一个贯穿其所有条目的双向链表。这个链表定义了遍历顺序，通常是插入 map 中的顺序。
  - 它提供一个特殊的 LinkedHashMap(int,float,boolean) 构造器来创建 LinkedHashMap，其遍历顺序是其最后一次访问的顺序。
  - 可以重写 removeEldestEntry(Map.Entry) 方法，以便在将新映射添加到 map 时强制删除过期映射的策略。
  - 这个类提供了所有可选择的 map 操作，并且允许 null 元素。由于维护链表的额外开销，性能可能会低于HashMap，有一条除外：遍历 LinkedHashMap 中的 collection-views 需要与 map.size 成正比，无论其容量如何。HashMap 的迭代看起来开销更大，因为还要求时间与其容量成正比。
  - LinkedHashMap 有两个因素影响了它的构成：初始容量和加载因子。
  - 注意这个实现不是线程安全的。如果多线程并发访问LinkedHashMap，并且至少一个线程修改了map，必须进行外部加锁。这通常通过在自然封装集合的某个对象上进行同步来实现 Map m = Collections.synchronizedMap(new LinkedHashMap(...))。
  - 个实现持有fail-fast机制。

* Hashtable 类

  - Hashtable 类实现了一个哈希表，能够将键映射到值。任何非空对象都可以用作键或值。
  - 此实现类支持 fail-fast 机制
  - 与新的集合实现不同，Hashtable 是线程安全的。如果不需要线程安全的容器，推荐使用 HashMap，如果需要多线程高并发，推荐使用 ConcurrentHashMap。

* IdentityHashMap 类

  - IdentityHashMap 是比较小众的 Map 实现了。
  - 这个类不是一个通用的 Map 实现！虽然这个类实现了 Map 接口，但它故意违反了 Map 的约定，该约定要求在比较对象时使用 equals 方法，此类仅适用于需要引用相等语义的极少数情况。
  - 同 HashMap，IdentityHashMap 也是无序的，并且该类不是线程安全的，如果要使之线程安全，可以调用Collections.synchronizedMap(new IdentityHashMap(...))方法来实现。
  - 支持fail-fast机制

* WeakHashMap 类

  - WeakHashMap 类基于哈希表的 Map 基础实现，带有弱键。WeakHashMap 中的 entry 当不再使用时还会自动移除。更准确的说，给定key的映射的存在将不会阻止 key 被垃圾收集器丢弃。
  - 基于 map 接口，是一种弱键相连，WeakHashMap 里面的键会自动回收
  - 支持 null 值和 null 键。
  - fast-fail 机制
  - 不允许重复

* WeakHashMap 经常用作缓存

![Alt text](../_static/container.png "Optional title")

## 内部类

* 一种非常有用的特性，定义在类内部的类，持有外部类的引用，但却对其他外部类不可见

## 异常 Exception

* 位于 java.lang 包下，它是一种顶级接口，继承于 Throwable 类，Exception 类及其子类都是 Throwable 的组成条件，是程序出现的合理情况
* Throwable 类是 Java 语言中所有错误(errors)和异常(exceptions)的父类。只有继承于 Throwable 的类或者其子类才能够被抛出，还有一种方式是带有 Java 中的 @throw 注解的类也可以抛出
* 通过 throws 声明函数抛出异常，通过 try-catch-finally 语句来捕获异常
* RuntimeException
  - ArrayIndexOutOfBoundsException  数组越界异常
  - NullPointerException  空指针异常
  - IllegalArgumentException  非法参数异常
  - NegativeArraySizeException  数组长度为负异常
  - IllegalStateException 非法状态异常
  - ClassCastException  类型转换异常
* UncheckedException
  - NoSuchFieldException  表示该类没有指定名称抛出来的异常
  - NoSuchMethodException 表示该类没有指定方法抛出来的异常
  - IllegalAccessException  不允许访问某个类的异常
  - ClassNotFoundException  类没有找到抛出异常
* Error 程序无法处理的错误，表示运行应用程序中较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时 JVM（Java 虚拟机）出现的问题
* 规范
  - 在Finally块中清理资源或者使用try-with-resource语句
  - 尽可能的使用最具体的异常来声明方法，这样才能使得代码更容易理解
  - 在Javadoc中加入throws声明，并且描述抛出异常的场景
  - 抛出异常的时候包含描述信息
  - 首先捕获最具体的异常
  - 不要捕获Throwable:Throwable是所有异常和错误的父类,如果catch了throwable，那么不仅仅会捕获所有exception，还会捕获error
  - 不要忽略异常:写了一个catch块，少要记录异常的信息
  - 不要记录并抛出异常：仅仅当想要处理异常时才去捕获，否则只需要在方法签名中声明让调用者去处理
  - 包装异常时不要抛弃原始的异常：一定要把原始的异常设置为cause(Exception有构造方法可以传入cause)
  - 不要捕获类似 Exception 之类的异常，而应该捕获类似特定的异常，比如 InterruptedException，方便排查问题，而且也能够让其他人接手你的代码时，会减少骂你的次数
  - 不要在函数式编程中使用 checkedException
* NoClassDefFoundError 和 ClassNotFoundException 区别
  - 类的加载过程中， JVM 或者 ClassLoader 无法找到对应的类时，都可能会引起这两种异常/错误，由于不同的 ClassLoader 会从不同的地方加载类，有时是错误的 CLASSPATH 类路径导致的这类错误，有时是某个库的 jar 包缺失引发这类错误
  - NoClassDefFoundError 表示这个类在编译时期存在，但是在运行时却找不到此类，有时静态初始化块也会导致 NoClassDefFoundError 错误
  - ClassNotFoundException 和 NoClassDefFoundError 都是由 CLASSPATH 中缺少类引起的，通常是由于缺少 JAR 文件而引起的，但是如果 JVM 认为应用运行时找不到相应的引用，就会抛出 NoClassDefFoundError 错误；当你在代码中显示的加载类比如 Class.forName() 调用时却没有找到相应的类，就会抛出 java.lang.ClassNotFoundException
    + NoClassDefFoundError 是 JVM 引起的错误，是 unchecked，未经检查的。因此不会使用 try-catch 或者 finally 语句块；另外，ClassNotFoundException 是受检异常，因此需要 try-catch 语句块或者 try-finally 语句块包围，否则会导致编译错误
    + 用 Class.forName()、ClassLoader.findClass() 和 ClassLoader.loadClass() 等方法时可能会引起 java.lang.ClassNotFoundException

```java
public class UserNotFoundException extends Exception { // 自定义一个异常
  public UserNotFoundException() {
    super();
  }

  public UserNotFoundException(String message) {
    super(message);
  }

  public UserNotFoundException(String message, Throwable e) {
    super(message, e);
  }
}

public class UserService {
  private UserRepository userRepo;
  public UserService(UseRepository userRepo) {
    this.userRepo = userRepo;
  }

  public User getUserById(long userId) throws UserNotFoundException {
    User user = userRepo.findUserById(userId);
    if (user == null) { // throw用来抛出异常
      throw new UserNotFoundException();//代码从此处返回
    }
    return user;
  }
}

public class UserController {
  private UserService userService;
  public UserController(UserService userService) {
    this.userService = userService;
  }

  public User getUserById(long userId) {
    User user = null;
    try { //捕获异常
      user = userService.getUserById(userId);
    } catch (UserNotFoundException e) {
      System.out.println("User not found: " + userId);
    } finally { //不管异常会不会发生，finally包裹的语句块总会被执行
      System.out.println("I am always printed.");
    }
    return user;
  }
}

static void cacheException() throws Exception{
  for (int i = 0; i < 5; i++) {
    System.out.println("enter: i=" + i);
    try {
      System.out.println("execute: i=" + i);
      continue;
    } finally {
      System.out.println("leave: i=" + i);
    }
  }
}
```

## 泛型 generics

* 提供了编译时类型安全检测机制，允许开发者在编译时检测到非法的类型
* 一种参数化的集合，它限制了你添加进集合的类型。泛型的本质就是一种参数化类型。多态也可以看作是泛型的机制。一个类继承了父类，那么就能通过它的父类找到对应的子类，但是不能通过其他类来找到具体要找的这个类。泛型的设计之处就是希望对象或方法具有最广泛的表达能力
* 本质是参数化类型
* 通配符
  - ？表示不确定的 java 类型
  - T (type) 表示具体的一个java类型
  - K V (key value) 分别代表java键值中的Key Value
  - E (element) 代表Element

## 类加载

* ClassLoader 是类路径装载器，在Java 中，类路径装载器一共有三种两类一种是虚拟机自带的 ClassLoader，分为三种
  - 启动类加载器(Bootstrap) ，负责加载 $JAVAHOME/jre/lib/rt.jar
  - 扩展类加载器(Extension)，负责加载 $JAVAHOME/jre/lib/ext/*.jar
  - 应用程序类加载器(AppClassLoader)，加载当前应用的 classpath 的所有类
* 用户自定义类加载器：Java.lang.ClassLoader 的子类，用户可以定制类的加载方式

## 并发编程

* 线程安全
* 线程池
  - [线程池参数动态化配置](https://mp.weixin.qq.com/s/EhBt44Rj0c5E-UVf742aGw)
* [AQS](https://mp.weixin.qq.com/s/ae60O68UofpuO0Cq5OEnNA)
* 锁
* 悲观锁/乐观锁
* 非/公平锁
* Concurrent工具包
* 无锁队列
* ABA问题
* 伪共享
* 死锁

## SSM

* IOC

* AOP

* Mybatis

* 日志组件

* 设计模式

* DDD

* UML

* 基础知识：

  - Java反射：Field、Type
  - Java代理：proxy、cglib
  - Java线程：Thread、Runnable、ExecutorService、Callable、Future、ThreadPoolExecutor
  - Java数据结构：HashMap ArrayList LinkedList HashSet BlockingQueue ConcurrentHashMap TreeMap
  - JVM：运行时数据区、堆设置、收集器设置、回收日志分析
  - Lambda表达式：stream、filter、collect、map、forEach、
  - 并发与锁：synchronized、ReentrantLock、ReadWriteLock、Atomic；
  - 通讯协议：HTTP、TCP/IP、NIO、BIO、WebSocket
  - 数据结构：表、栈、队列、二叉树、AVL树、BTree、黑红数、散列、图。
  - 常用算法：冒泡排序，选择排序，插入排序、堆排序，归并排序、快速排序；二分查找；布隆过滤器；
  - 设计模式：工厂模式、观察者模式、单例模式、代理模式、命令模式、策略模式
  - Web容器：tomcat、jboss、jetty
  - HTTP服务：httpd、nginx、openResty、kong
  - 工具包：common、poi、gson、guava
  - 构建工具：maven、gradle
  - 通讯框架：netty、mina
  - 序列化：hessian、protostuff、json
  - 服务发现：zookeeper、etcd、eureka、consul
  - 数据库：mysql、mongoDB、redis、mycat、berkeleyDB
  - 连接池：dbcp、c3o0、druid、jdbc、http
  - 大数据：spark、storm、hadoop、hdfs
  - 容器：docker、k8s
  - 监控：zabbix、prometheus

* 数据库：

  - Mysql：主备、读写分、横向纵向拆分、调优、语法、索引、优化
  - Redis：主备、读写分离、持久化、命中和过期
  - MogoDB：集合、文档、文件、索引、聚合函数、分片

* 消息队列：

  - 概念：topic、message、queue、producer、consumer、broker
  - 消息类型：顺序消息、定时消息、延迟消息、事务消息
  - 消息回溯、消息堆积、消息拉取、消息签收

* 高并发：

  - 服务拆分：微服务化、分布式事务、数据库水平垂直拆分
  - 服务治理：zookeeper、rpc
  - 消息队列：异步处理、最终一致性
  - 缓存技术：JVM缓存、redis缓存、nginx缓存、CDN缓存、浏览器缓存。缓存击穿、缓存雪崩、缓存淘汰
  - 并发编程
    + 学习JDK源码
    + 看JVM源码
    + 看CPU架构
    + 在技术点逐渐深度研究的过程中，广度也得到了完善
  - 参考
    + <http://ifeve.com/talk-concurrency/>
    + [Java并发](https://mp.weixin.qq.com/s?__biz=MjM5MzA1Mzc3Nw==&mid=2247484908&idx=1&sn=fe9004cd8369cabf448c9f43466bad0f)

* 高可用：

  - 负载均衡：算法、动静分离、切换、检测
  - 超时重试：超时时间、重试机制和策略
  - 限流：算法、容器、nginx、防止抖动
  - 隔离：线程隔离、进程隔离、机房隔离、读写隔离、动静隔离，采用hystrix、servlet3做隔离熔断
  - 降级：自动降级、人工降级，控制中心，采用hystrix手段
  - 监控：进程监控、线程监控、机器监控，报警

* 问题解决
  1.如何解决单点故障；(lvs、F5、A10、Zookeep、MQ)
  2.如何保证数据安全性；(热备、冷备、异地多活)
  3.如何解决检索难题；(数据库代理中间件：mysql-proxy、Cobar、MaxScale等;)
  4.如何解决统计分析问题；(离线、近实时)

* [volatile](https://mp.weixin.qq.com/s/x78EZQ0E0fgKSwGdK5vtwg)

jvm原理，spring+springmvc原理及源码，linux，mysql事务隔离与锁机制，mongodb，http/tcp，多线程，分布式架构（dubbo，dubbox，spring cloud），弹性计算架构，微服务架构（springboot+zookeeper+docker+jenkins），java性能优化，以及相关的项目管理等等。

## Java Agent

* Java代理是为应用程序提供检测功能的软件组件。在代理的上下文中 ，检测提供了重新定义在运行时加载的类内容的功能。
* [Jacoco](https://www.eclemma.org/jacoco/) 代理是 Java 代理之一，可以在 JVM 加载类文件时标记类代码，并在调用任何代码后及时计算覆盖范围。可以转储覆盖数据并上传到SonarQube以使其可视化，获取最新的Jacoco代理
* 使用
  - 需要使用以下两个文件：
    + lib / jacocoagent.jar –> Java代理用以标记代码
    + lib / jacococli.jar –> CLI转储覆盖率数据并生成报告
  - 宿主应用程序启动参数设置
    + `java -javaagent:/lib/jacocoagent.jar=includes=*,output=tcpserver,port=6300,address=localhost,append=true -jar MyBackendService.jar`
    + 通过 Docker 运行后端服务:在 docker 镜像中构建jacocoagent
* 转储覆盖率数据: `java -jar /lib/jacococli.jar dump --address localhost --port 6300 --destfile ./coverage.exec`
* 生成可视化报告: `java -jar /lib/jacococli.jar report ./coverage.exec --classfiles ./build/classes --html htmlReportFolder --xml xmlReportFileName.xml`
* 报告上传到SonarQube `./mvnw sonar:sonar -Dsonar.coverage.jacoco.xmlReportPaths=./xmlReportFileName.xml -Dsonar.java.binaries=./build/classes -Dsonar.sources=./src/main/java -Dsonar.inclusions="**/*Api.java,**/*Controller.java"`

## Lombok

通过相关注解就可以不用再编写冗长的 getter 或者 equals 等方法

* 注解解析方式
  - 运行时解析，比如 Spring 配置的 AOP 切面这些注解都是在程序运行的时候通过反射来获取的注解值，但是只有在程序运行时才能获取到这些注解值，导致运行时代码效率很低，并且如果想在编译阶段利用这些注解来进行检查，比如对用户的不合理代码作出错误报告，反射的方法就行不通了。
  - 编译时解析，Lombok 工具就是运行在编译时解析的
* JSR 269 插入式注解处理器（Pluggable Annotation Processing API），它是实现了 JSR 269 的机制
* 优点
  - 通过注解自动生成样板代码，提高开发效率
  - 代码简洁，只关注相关属性
  - 新增属性后，无需刻意修改相关方法
* 缺点：
  - 降低了源代码的可读性和完整性
  - 加大对问题排查的难度（可能问题定位到不存在的行，无从下手）
  - 强 x 队友，因为需要 IDE 的相关插件的支持

## 客户端

* JavaFX
* swing
* Spring

JavaEE/JDBC/Weblogic

## project

* [symphony](https://github.com/b3log/symphony):🎶 一款用 Java 实现的现代化社区（论坛/BBS/社交网络/博客）平台。<https://hacpai.com> <https://sym.b3log.org>
* [shopping-management-system](https://github.com/zhanglei-workspace/shopping-management-system)
* [zheng](https://github.com/shuzheng/zheng):基于Spring+SpringMVC+Mybatis分布式敏捷开发系统架构，提供整套公共微服务服务模块：集中权限管理（单点登录）、内容管理、支付中心、用户管理（支持第三方登录）、微信平台、存储系统、配置中心、日志分析、任务和通知等，支持服务治理、监控和追踪，努力为中小型企业打造全方位J2EE企业级开发解决方案。 <http://47.93.195.63/zheng-upms-server>
* [halo](https://github.com/ruibaby/halo):Halo可能是最好的Java博客系统😉 <https://docs.halo.run>

## 面试

* [JavaGuide](https://github.com/Snailclimb/JavaGuide):【Java学习+面试指南】 一份涵盖大部分Java程序员所需要掌握的核心知识。 <https://github.com/Snailclimb/JavaGuide>
* [可能是一份最适合你的后端面试指南](https://juejin.im/post/5ba591386fb9a05cd31eb85f)
* [advanced-java](https://github.com/doocs/advanced-java):😮 互联网 Java 工程师进阶知识完全扫盲：涵盖高并发、分布式、高可用、微服务等领域知识
* [Java-Tutorial](https://github.com/h2pl/Java-Tutorial):【Java工程师面试复习指南】本仓库涵盖大部分Java程序员所需要掌握的核心知识，整合了互联网上的很多优质Java技术文章，力求打造为最完整最实用的Java开发者学习指南，如果对你有帮助，给个star告诉我吧，谢谢！
* [toBeTopJavaer](https://github.com/hollischuang/toBeTopJavaer):To Be Top Javaer - Java 工程师成神之路 www.hollischuang.com

## 图书

* [Thinking In Java Java 编程思想](https://www.codeguru.com/java/tij/tij_c.shtml)
  - [on Java8](https://lingcoder.github.io/OnJava8/#/)
  - [thinking-in-java-zh](https://github.com/apachecn/thinking-in-java-zh):📖 Java 编程思想
* Java核心技术·卷 I（原书第10版）
* Java核心技术·卷 II（原书第10版）
* Effective Java
* Head First Java
* [Introduction to Programming Using Java](http://math.hws.edu/javanotes/)
* 《[Java8 实战](https://www.amazon.cn/gp/product/B01ER75QC8)》
* Java并发编程实战 Java concurrency in practice
* 《Java并发编程的艺术》
* 《[Java性能权威指南](https://www.amazon.cn/gp/product/B01DLB7Z66)》
* 《[Java程序员修炼之道](https://www.amazon.cn/gp/product/B00E0D2OX4)》
* 深入理解Java虚拟机（第3版）
* 《大型网站系统与 Java 中间件实践》

## 教程

* [Java教程](https://www.liaoxuefeng.com/wiki/1252599548343744)
* [docs4dev](https://www.docs4dev.com)

## 工具

* IDE
  - [Eclipse](https://www.eclipse.org/)
  - [插件库](https://plugins.jetbrains.com/idea)
  - [Cloud Toolkit](https://www.aliyun.com/product/cloudtoolkit): 一款 IDE 插件，可以帮助开发者更高效地开发、测试、诊断并部署应用
* 测试
  - [arthas](https://github.com/alibaba/arthas):Alibaba Java Diagnostic Tool Arthas/Alibaba Java诊断利器 Arthas <https://alibaba.github.io/arthas/>
  - [mockito](https://github.com/mockito/mockito):Most popular Mocking framework for unit tests written in Java <http://mockito.org>
* datetime
  - [joda-time](https://github.com/JodaOrg/joda-time):Joda-Time is the widely used replacement for the Java date and time classes prior to Java SE 8. <http://www.joda.org/joda-time/>
* 框架
  - [blade](https://github.com/lets-blade/blade):🚀 Lightning fast and elegant mvc framework for Java8 <https://lets-blade.com>
  - Spring：IOC、AOP、事务处理
  - SpringMVC：DispatcherServlet、HandlerMapping、HandlerAdapter、Controller、Intercepter、View
  - SpringBoot：集成web、hibernate、mybatis、redis、docker下使用
  - SpringCloud：Netfix、Config、Bus、Eureka、Consul、Stream、Task、Gateway
  - Hibernate：Configuration、SessionFactory、乐观锁、二级缓存、高并发、多数据源
  - Mybatis：Configuration、SqlSession、Executor 、TypeHandler、动态sql、二级缓存
  - Netty：nio、拆念包、future、pipeline
  - [guava](https://github.com/google/guava):Google core libraries for Java 限流算法、布隆过滤器、JVM缓存
  - Hystrix：隔离、熔断、降级
  - RPC框架：dubbo、motan、thrift、grpc
    + [grpc-java](https://github.com/grpc/grpc-java)The Java gRPC implementation. HTTP/2 based RPC <https://grpc.io>
  - 搜索引擎：Lucene、Elasticsearch、Solr
* 规范
  - Alibaba Java Code Guidelines 阿里巴巴Java开发手册
  - [p3c](https://github.com/alibaba/p3c):Alibaba Java Coding Guidelines pmd implements and IDE plugin <https://github.com/alibaba/p3c/wiki>
* Admin
  - [eladmin](https://github.com/elunez/eladmin):项目基于 Spring Boot 2.1.0 、 Jpa、 Spring Security、redis、Vue的前后端分离的后台管理系统，项目采用分模块开发方式， 权限控制采用 RBAC，支持数据字典与数据权限管理，支持一键生成前后端代码，支持动态路由 <https://auauz.net>
* 优化
  - [hutool](https://github.com/looly/hutool):A set of tools that keep Java sweet. <http://www.hutool.cn>
* [httpcomponents-core](https://github.com/apache/httpcomponents-core)
* [Apache Camel](https://github.com/apache/camel) is a powerful open source integration framework based on known Enterprise Integration Patterns with powerful Bean Integration.
* [vjtools](https://github.com/vipshop/vjtools):The vip.com's java coding standard, libraries and tools
* [opengrok](https://github.com/oracle/opengrok):OpenGrok is a fast and usable source code search and cross reference engine, written in Java <http://oracle.github.io/opengrok/>
* [http-request](https://github.com/kevinsawicki/http-request):Java HTTP Request Library
* [AutoLoadCache](https://github.com/qiujiayu/AutoLoadCache):AutoLoadCache 是基于AOP+Annotation等技术实现的高效的缓存管理解决方案，实现缓存与业务逻辑的解耦，并增加异步刷新及“拿来主义机制”，以适应高并发环境下的使用。
* [vert.x](https://github.com/eclipse-vertx/vert.x):Vert.x is a tool-kit for building reactive applications on the JVM <http://vertx.io>
* [Sentinel](https://github.com/alibaba/Sentinel):A lightweight powerful flow control component enabling reliability and monitoring for microservices. (轻量级的流量控制、熔断降级 Java 库)
* [SDKMAN](https://sdkman.io):The Software Development Kit Manager,a tool for managing parallel versions of multiple Software Development Kits on most Unix-like systems
  - `curl -s "https://get.sdkman.io" | bash`
  - `source "$HOME/.sdkman/bin/sdkman-init.sh"`
* Log
  - [主流日志工具库](https://mp.weixin.qq.com/s/iuWJxBghqhF09JqYfejBWw)
* [api-document](https://github.com/liuanxin/api-document):java spring-mvc document collect
* [jenv](https://github.com/jenv/jenv):Manage your Java environment <http://www.jenv.be>
* [akka](https://github.com/akka/akka):Build highly concurrent, distributed, and resilient message-driven applications on the JVM <https://akka.io/>

## 参考

* [Java World](http://www.javaworld.com/)
* [awesome-java](https://github.com/akullpp/awesome-java) A curated list of awesome frameworks, libraries and software for the Java programming language.
* [Java SE 技术文档](http://docs.oracle.com/javase/)
* [technology-talk](https://github.com/aalansehaiyang/technology-talk)：汇总java生态圈常用技术框架、开源中间件，系统架构、项目管理、经典架构案例、数据库、常用三方库、线上运维等知识
* [java-design-patterns](https://github.com/iluwatar/java-design-patterns):Design patterns implemented in Java <http://java-design-patterns.com>
* [Java Algorithm And Data Structure Interview Questions and Programs](http://www.codespaghetti.com/java-algorithms-questions/)
* [JCSprout](https://github.com/crossoverJie/JCSprout):👨‍🎓 Java Core Sprout : basic, concurrent, algorithm
* [精简之道](https://mp.weixin.qq.com/s/Icn5_RZzFHB9WsKip2ZZ6g)
