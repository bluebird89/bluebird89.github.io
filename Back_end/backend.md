# 后端|服务器端

* 三高（高并发，高可用，高性能）
* 安全
* 存储
* 业务

## 职能

* web项目开发
* 底层API封装与开发:为前端操作提供服务
* 线上系统的优化
* 线上服务器的运维，常见问题的诊断与解决。
* 存储：文件 信息 信息之间的关系（数据库）

## 技能

* 掌握好语言基础
* 语言生态
  - apache+php 常用的PHP和apache模块
  - 框架：LN(A)MP架构
* 算法与数据结构
* 计算机网络
* 数据库
  - Mysql 优化、能创建高效的索引
  - nosql
* 消息中间件
* Linux与应用部署，Shell脚本
* 缓存
  * Memcache
  * Redis
* 服务化
* 项目扩展
  - restful
  - solr
* 模版引擎

## 业务

* 设计、实现相关业务服务
* 底层框架代码以及线上系统优化

## 进阶

* 了解大容量、高性能的分布式系统开发原理
* 在开放平台，分布式存储，分布式Cache

## 趋势

* 异步模式：Go Dubbo.异步非阻塞的 Nginx，而不是同步阻塞的 Apache。就是因为 Nginx 这样的异步程序，它的适应性更好、并发能力更强。现在在后端业务开发编程方面，技术力量强的团队已经开始将技术栈从同步模式切换为异步了。
  - 同步阻塞模式存在较多缺陷，并发能力弱、适应性差、慢速请求导致服务不可用。如：后台接口中调用第三方 API 的场景，同步模式效果极差。过去那些使用 Java、PHP、C++、Python、Ruby 语言开发的同步阻塞模式框架，用的人越来越少。
* Node.js:很少见到企业将 Node.js 作为公司后端方面的主要编程语言.
  - 异步回调的技术方案，以及在它之上所做的一些优化方案，包括 Promise、Future、Yield/Generator、Async/Await 等，改变了程序开发的风格和习惯。使用这些技术方案是无法兼容已有程序的
* 协程模式，兼顾了同步阻塞的可维护性和异步非阻塞的高并发能力。将会成为未来后端开发领域的主流技术方案。
  - 协程模式只需要对已有项目代码进行少量调整就可以运行起来，甚至可以完全兼容老项目。只需要框架层进行兼容即可。
  - GO 是最耀眼的那一个。协程、通道、静态语言、性能、富编译、标准库丰富、生态完整、Google 等
  - PHP + Swoole 的技术栈，更适合快速开发、快速迭代、业务驱动的场景。毕竟动态语言比静态语言还是要更加灵活、开发效率更高。而 Go 更适合编写系统级软件、核心业务。

## 系统性能

* 分类
  - Load Testing - 负载测试
  - Stress Testing - 压力测试
  - Soak Testing - 耐久测试
  - Spike Testing - 瞬压测试
* 指标
  - 技术指标
    + OK / KO
    + QPS / RPS / TPS
    + Response Time(min/max/mean/std/90%…)
    + Concurrent Users / Concurrent Requests
  - 业务指标
    + 平均同时在线用户数
    + 同时在线用户数
* 步骤
  - 确定性能需求（可选）
  - 准备测试环境和测试数据
  - 选择性能测试工具/平台，
  - 制定性能测试模型，编写性能测试代码
  - 运行性能测试
  - 分析测试报告
  - 性能调优 | 修复问题
* 测试核心
  - 网关(防火墙/VPN等)
  - 应用系统
  - 数据库
* 目标：核心三点都分别性能最优，并且全链路长时超高压能正常运行

## 系统性能工程

* 内容
  - 架构易扩展
  - 测试较简单
  - 分析很困难
    + 性能测试结果 （ Throughput vs Latency 等）
    + 操作系统监控（ CPU, Memory, IO, Network 等）
    + 应用系统（ Profiler, Code Review 等）
    + 网关和数据库 （ Logs, CPU, Memory, IO 等）
  - 优化可灵活
    + 硬件基础设施优化
    + 操作系统优化
    + 应用系统优化
    + 数据库优化
    + 系统架构优化
  - 规划要按需
    + 选取测试指标
    + 建立测试模型
    + 变化测试指标
    + 分析测试报告、拟合测试数据

## 负载均衡 Load Balancer

* 一组计算机节点（或者一组进程）提供相同（同质的）服务，服务请求应该均匀分摊到这些节点上
* 当系统面临大量用户访问，负载过高的时候，通常会使用增加服务器数量来进行横向扩展，使用集群和负载均衡提高整个系统的处理能力
* 把用户访问的流量通过「负载均衡器」根据某种转发策略，均匀的分发到后端多台服务器上，后端服务器可以独立响应和处理请求，从而实现分散负载的效果，负载均衡的关键在于将用户流量进行均衡减压的
* 让所有节点以最小代价、最好状态对外提供服务，这样系统吞吐量最大，性能更高，对于用户而言请求的时间也更小
* 优点
  - 增强了系统可靠性
  - 提高了系统服务能力
  - 增强了应用可用性，最大化降低了单个节点过载、甚至crash概率
* 负载均衡是一种推模型，一定会选出一个服务节点，然后把请求推送过来
* 消息队列是拉模型：空闲服务节点主动去拉取请求进行处理，各个节点负载自然也是均衡的
  - 服务节点不会被大量请求冲垮，同时增加服务节点更加容易
  - 缺点：请求不是事实处理的

### 结构

每一个上游都均匀访问每一个下游，就能实现“将请求/数据【均匀】分摊到多个操作单元上执行

* 客户端层：典型调用方是浏览器browser或者手机应用APP，根据服务节点信息自行选择，然后将请求直接发送到选中服务节点
  - 知道服务器列表，要么是静态配置，要么有简单接口查询
  - backend server详细负载信息，就不适用通过客户端来查询
  - 算法要么是比较简单的，比如轮训（加权轮训）、随机（加权随机）、哈希这几种算法，只要每个客户端足够随机，按照大数定理，服务节点的负载也是均衡的
  - 较为复杂算法，比如根据backend的实际负载需要去额外的负载均衡服务（external load balancing service）查询到这些信息，在grpc中，就是使用这种办法
    + load balancer与grpc server通信，获得grpc server的负载等具体详细
    + grpc client从load balancer获取这些信息，最终grpc client直连到被选择的grpc server
* 反向代理层：系统入口，反向代理
  - 水平扩展通过“DNS轮询”实现的：dns-server对于一个域名配置了多个解析ip，每次DNS解析请求来访问dns-server，会轮询返回这些ip
  - 当nginx成为瓶颈的时候，只要增加服务器数量，新增nginx服务部署，增加一个外网ip，就能扩展反向代理层的性能，做到理论上的无限高并发
  - 请求轮询：和DNS轮询类似，请求依次路由到各个web-server；
  - 最少连接路由：哪个web-server的连接少，路由到哪个web-server；
  - ip哈希：按照访问用户的ip哈希值来路由web-server，只要用户的ip分布是均匀的，请求理论上也是均匀的，ip哈希均衡方法可以做到，同一个用户的请求固定落到同一台web-server上，此策略适合有状态服务，例如session；
* 站点应用层：实现核心应用逻辑，返回html或者json
  - 水平扩展通过“nginx”实现的。通过修改nginx.conf，设置多个web后端
  - 当web后端成为瓶颈的时候，增加服务器数量，新增web服务部署，在nginx配置中配置上新的web后端，就能扩展站点层的性能，做到理论上的无限高并发
* 服务层：如果实现了服务化，就有这一层
  - 水平扩展通过“服务连接池”实现的。站点层通过RPC-client调用下游的服务层RPC-server时，RPC-client中的连接池会建立与下游服务多个连接，当服务成为瓶颈的时候，只要增加服务器数量，新增服务部署，在RPC-client处建立新的下游服务连接，就能扩展服务层性能，做到理论上的无限高并发
  - 如果需要优雅进行服务层自动扩容，需要配置中心里服务自动发现功能的支持
* 缓存层：缓存加速访问存储
* 数据库层：数据库固化数据存储
* 在数据量很大情况下，数据层（缓存，数据库）涉及数据水平扩展，将原本存储在一台服务器上的数据（缓存，数据库）水平拆分到不同服务器上去，以达到扩充系统性能的目的，要考虑“数据的均衡”与“请求的均衡”两个点
  - 按照范围水平拆分：每一个数据服务，存储一定范围的数据，user0库，存储uid范围1-1kw，user1库，存储uid范围1kw-2kw
    + 规则简单，service只需判断一下uid范围就能路由到对应的存储服务；
    + 数据均衡性较好；
    + 比较容易扩展，可以随时加一个uid[2kw,3kw]的数据服务
    + 不足：请求的负载不一定均衡，一般来说，新注册的用户会比老用户更活跃，大range的服务请求压力会更大
  - 按照哈希水平拆分:每一个数据库，存储某个key值hash后的部分数据，user0库，存储偶数uid数据,user1库，存储奇数uid数据
    + 规则简单，service只需对uid进行hash能路由到对应的存储服务
    + 数据均衡性较好
    + 请求均匀性较好
    + 不容易扩展，扩展一个数据服务，hash方法改变时候，可能需要进行数据迁移
  - 水平拆分来扩充系统性能vs主从同步读写分离
    + 水平拆分扩展数据库性能：
      * 每个服务器上存储的数据量是总量的1/n，所以单机的性能也会有提升
      * n个服务器上的数据没有交集，那个服务器上数据的并集是数据的全集
      * 数据水平拆分到了n个服务器上，理论上读性能扩充了n倍，写性能也扩充了n倍（其实远不止n倍，因为单机的数据量变为了原来的1/n）
    + 通过主从同步读写分离扩展数据库性能：
      * 每个服务器上存储的数据量是和总量相同
      * n个服务器上的数据都一样，都是全集
      * 理论上读性能扩充了n倍，写仍然是单点，写性能不变
* 服务节点集群之前放一个集中式代理（proxy），由代理负责请求分发
  - 7层Nginx:response经过Proxy
  - 四层F5、LVS:response不经过proxy，如LVS
  - 在于方便控制，而且能容易实现一些更精密，更复杂的算法
  - 缺点
    - 负载均衡器本身可能成为性能瓶颈
    - 可能引入额外的延迟，请求一定先发到达负载均衡器，然后到达真正的服务节点。
  * load balancer proxy不能成为单点故障（single point of failure），因此一般会设计为高可用的主从结构
  * response也是走load balancer proxy的话，那么整个服务过程对客户端而言就是完全透明的，也防止了客户端去尝试连接后台服务器，提供了一层安全保障！

![grpc原理图](../_static/grpc.png "grpc原理图")
![proxy原理图](../_static/proxy.png "proxy原理图")

### 方案

* HTTP重定向：权衡转移请求开销和处理实际请求开销，前者相对于后者越小，那么重定向的意义就越大
  - 缺陷
    + 吞吐率限制：主站点服务器的吞吐率平均分配到了被转移的服务器现假设使用RR（Round Robin）调度策略，子服务器的最大吞吐率为1000reqs/s，那么主服务器的吞吐率要达到3000reqs/s，主服务器的吞吐与子服务器吞吐匹配
    + 重定向访问深度不同
* 基于DNS负载均衡：可以实现在地域上流量均衡,DNS服务器便充当负载均衡调度器。大型网站一般使用DNS作为第一级负载均衡 DNS节省了所谓的主站点，DNS服务器已经充当了主站点的职能。常见的策略是对多个A记录进行RR(轮询)
  - 在DNS服务器配置多个A记录，不同的DNS请求会解析到不同的IP地址 让DNS服务器根据不同地理位置的用户返回不同的IP
  - 相当于实现了按照「就近原则」将请求分流了，既减轻了单个集群的负载压力，也提升了用户的访问速度。
  - 配置简单，实现成本非常低，无需额外的开发和维护工作
  - 缺点：
    + 大多是基于地域或者干脆直接做IP轮询，没有更高级的路由策略，所以这也是DNS方案的局限所在，比如 无法将HTTP请求的上下文引入到调度策略中
    + DNS生效时间略长，当配置修改后，生效不及时。这个是由于DNS的特性导致的，DNS一般会有多级缓存，所以当修改了DNS配置之后，由于缓存的原因，会导致IP变更不及时，从而影响负载均衡的效果
* 基于硬件负载均衡：用于大型服务器集群中的负载需求，F5 Network Big-IP。完全通过硬件来抗压力，性能是非常的好。用在大型互联网公司的流量入口最前端
* 基于软件负载均衡：基于机器层面的流量均衡
  - 四层负载均衡｜Linux Virtual Server LVS:基于第四层传输层来做流量分发方案，通过报文中目标地址和端口，支持 TCP/UDP 负载均衡
    + LVS在Linux内核态获取到IP报文后，根据特定负载均衡算法将IP报文转发到整个集群的某台服务器中去
    + 服务器集群系统有三个部分组成：
      * 最前端负载均衡层，用 Load Balancer 表示
      * 中间服务器集群层，用 Server Array 表示
      * 最底端数据共享存储层，用 Shared Storage 表示
    + 特点
      + 基于 4 层的网络协议的，抗负载能力强，对于服务器的硬件要求除了网卡外，其他没有太多要求
      + 配置性比较低，这是一个缺点也是一个优点，因为没有可太多配置的东西，大大减少了人为出错的几率
      + 应用范围比较广，不仅仅对 web 服务做负载均衡，还可以对其他应用（mysql）做负载均衡
      + LVS 架构中存在一个虚拟 IP 的概念，需要向 IDC 多申请一个 IP 来做虚拟 IP
    + 转发主要通过修改 IP 地址（NAT 模式，分为源地址修改 SNAT 和目标地址修改 DNAT）、修改目标 MAC（DR 模式）来实现
      * NAT（Network Address Translation）是一种外网和内网地址映射的技术
        - 当包到达 LVS 时，LVS 做目标地址转换（DNAT），将目标 IP 改为 RS 的 IP。RS 接收到包以后，仿佛是客户端直接发给它的一样。RS 处理完，返回响应时，源 IP 是 RS IP，目标 IP 是客户端的 IP。这时 RS 的包通过网关（LVS）中转，LVS 会做源地址转换（SNAT），将包的源地址改为 VIP，这样，这个包对客户端看起来就仿佛是 LVS 直接返回给它的
        - NAT服务器（前端服务器）必须作为实际服务器（后端服务器）的网关，否则数据包被转发后将一去不返
        - 从Linux2.4内核开始，其内置的Neftilter模块在内核中维护着一些数据包过滤表，这些表包含了用于控制数据包过滤的规则
        - Linux提供了iptables来对过滤表进行插入、修改和删除等操作。更加令人振奋的是，Linux2.6.x内核中内置了IPVS模块，它的工作性质类型于Netfilter模块，不过它更专注于实现IP负载均衡
        - `modprobe -l  | grep ipvs` 管理工具是ipvsadm
          + `ipvsadm -A -t 111.11.11.11:80 -s rr`: 添加一台虚拟服务器，-t 后面是服务器的外网ip和端口，-s rr是指采用简单轮询的RR调度策略
          + `ipvsadm -a -t 111.11.11.11:80 -r 10.10.120.210:8000 -m`  -r后面是实际服务器的内网ip和端口，-m表示采用NAT方式来转发数据包
        - 作为调度器的NAT服务器可以将吞吐率提升到一个新的高度，几乎是反向代理服务器的两倍以上，这大多归功于在内核中进行请求转发的较低开销。
        - 瓶颈:NAT服务器的网络带宽，包括内部网络和外部网络- 网络地址转换(NAT)负载均衡工作在传输层，对数据包中的IP地址和端口进行修改，从而达到转发的目的
      * DR 模式：直接路由，需要 LVS 和 RS 集群绑定同一个 VIP（RS 通过将 VIP 绑定在 loopback 实现），但与 NAT 的不同点在于：请求由 LVS 接受，由真实提供服务的服务器（RealServer，RS）直接返回给用户，返回的时候不经过 LVS
        - 工作在数据链路层（第二层）,通过修改数据包的目标MAC地址（没有修改目标IP），将数据包转发到实际服务器上，不同的是，实际服务器的响应数据包将直接发送给客户羰，而不经过调度器。
        - 一个请求过来时，LVS 只需要将网络帧的 MAC 地址修改为某一台 RS 的 MAC，该包就会被转发到相应的 RS 处理，注意此时的源 IP 和目标 IP 都没变，LVS 只是做了一下移花接木。RS 收到 LVS 转发来的包时，链路层发现 MAC 是自己的，到上面的网络层，发现 IP 也是自己的，于是这个包被合法地接受，RS 感知不到前面有 LVS 的存在。而当 RS 返回响应时，只要直接向源 IP（即用户的 IP）返回即可，不再经过 LVS
        - 数据分发过程中不修改 IP 地址，只修改 mac 地址，由于实际处理请求的真实物理 IP 地址和数据请求目的 IP 地址一致，所以不需要通过负载均衡服务器进行地址转换，可将响应数据包直接返回给用户浏览器，避免负载均衡服务器网卡带宽成为瓶颈。因此，DR 模式具有较好的性能，也是目前大型网站使用最广泛的一种负载均衡手段。
        - 相较于LVS-NAT的最大优势在于LVS-DR不受调度器宽带的限制
      * LVS-TUN｜基于IP隧道的请求转发机制：将调度器收到的IP数据包封装在一个新IP数据包中，转交给实际服务器，然后实际服务器的响应数据包可以直接到达用户端
        - 与LVS-DR不同的是，实际服务器可以和调度器不在同一个WANt网段，调度器通过IP隧道技术来转发请求到实际服务器，所以实际服务器也必须拥有合法的IP地址。
      * LVS-DR和LVS-TUN都适合响应和请求不对称的Web服务器，如何从它们中做出选择，取决于你的网络部署需要，因为LVS-TUN可以将实际服务器根据需要部署在不同的地域，并且根据就近访问的原则来转移请求，所以有类似这种需求的，就应该选择LVS-TUN
    + 优点
      * 抗负载能力强、是工作在传输层上仅作分发之用，没有流量的产生，这个特点也决定了它在负载均衡软件里的性能最强的，对内存和 cpu 资源消耗比较低
      * 配置性比较低，这是一个缺点也是一个优点，因为没有可太多配置的东西，所以并不需要太多接触，大大减少了人为出错的几率
      * 工作稳定，因为其本身抗负载能力很强，自身有完整的双机热备方案，如 LVS + Keepalived
      * 无流量，LVS 只分发请求，而流量并不从它本身出去，这点保证了均衡器 IO 的性能不会受到大流量的影响
      * 应用范围比较广，因为 LVS 工作在传输层，几乎可以对所有应用做负载均衡，包括 http、数据库、在线聊天室等等
    + 缺点
      * LVS性能依赖Linux内核的网络性能，但Linux内核的网络路径过长导致了大量开销，使得LVS单机性能较低
      * 软件本身不支持正则表达式处理，不能做动静分离；而现在许多网站在这方面都有较强的需求，这个是 Nginx、HAProxy + Keepalived 的优势所在
      * 如果是网站应用比较庞大的话，LVS/DR + Keepalived 实施起来就比较复杂了，相对而言，Nginx / HAProxy + Keepalived 就简单多了
    + LVS vs Nginx
      * LVS 比 Nginx 具有更强的抗负载能力，性能高，对内存和 CPU 资源消耗较低
      * LVS 工作在网络层，具体流量由操作系统内核进行处理，Nginx 工作在应用层，可针对 HTTP 应用实施一些分流策略
      * LVS 安装配置较复杂，网络依赖性大，稳定性高。Nginx 安装配置较简单，网络依赖性小
      * LVS 不支持正则匹配处理，无法实现动静分离效果
      * LVS 适用的协议范围广。Nginx 仅支持 HTTP、HTTPS、Email 协议，适用范围小
  - 反向代理负载均衡｜七层负载均衡 :基于第七层应用层来做流量分发
    + 工作在HTTP层面，核心工作是转发HTTP
    + 任何对于实际服务器HTTP请求都必须经过调度器
    + 调度器必须等待实际服务器HTTP响应，并将它反馈给用户
    + 特性：
      * 调度策略丰富
      * 对反向代理服务器的并发处理能力要求高，因为它工作在HTTP层面
      * 反向代理服务器进行转发操作本身需要一定开销的，比如创建线程、与后端服务器建立TCP连接、接收后端服务器返回的处理结果、分析HTTP头部信息、用户空间和内核空间的频繁切换等，虽然这部分时间并不长，但是当后端服务器处理请求的时间非常短时，转发的开销就显得尤为突出。例如请求静态文件，更适合使用前面介绍的基于DNS的负载均衡方式
      * 反向代理服务器可以监控后端服务器，比如系统负载、响应时间、是否可用、TCP连接数、流量等，从而根据这些数据调整负载均衡的策略
      * 反射代理服务器可以让用户在一次会话周期内的所有请求始终转发到一台特定的后端服务器上（粘滞会话），这样的好处一是保持session的本地访问，二是防止后端服务器的动态内存缓存的资源浪费
    + Nginx：七层负载均衡 ，也称为“内容交换”，也就是主要通过报文中真正有意义的应用层内容
      * 传统：相对于传统基于进程或线程模型（Apache就采用这种模型）在处理并发连接时会为每一个连接建立一个单独的进程或线程，且在网络或者输入/输出操作时阻塞，将导致内存和 CPU 的大量消耗，因为新起一个单独的进程或线程需要准备新的运行时环境，包括堆和栈内存的分配，以及新的执行上下文，当然，这些也会导致多余的 CPU 开销。最终，会由于过多的上下文切换而导致服务器性能变差。
      * Nginx 的架构设计是采用模块化的、基于事件驱动、异步、单线程且非阻塞
  - HAProxy
    + 特点
      + HAProxy 是工作在网络 7 层之上
      + 支持 Session 的保持，Cookie 的引导等
      + 支持 url 检测后端的服务器出问题的检测会有很好的帮助
      + 支持的负载均衡算法：动态加权轮循(Dynamic Round Robin)，加权源地址哈希(Weighted Source Hash)，加权 URL 哈希和加权参数哈希(Weighted Parameter Hash)
      + 单纯从效率上来讲 HAProxy 更会比 Nginx 有更出色的负载均衡速度
      + HAProxy 可以对 Mysql 进行负载均衡，对后端的 DB 节点进行检测和负载均衡
    + 优点能够补充 Nginx 的一些缺点，比如支持 Session 的保持，Cookie 的引导；同时支持通过获取指定的 url 来检测后端服务器的状态
    + 本身就只是一款负载均衡软件；单纯从效率上来讲 HAProxy 会比 Nginx 有更出色的负载均衡速度，在并发处理上也是优于 Nginx 的
    + 支持 TCP 协议的负载均衡转发，可以对 MySQL 读进行负载均衡，对后端的 MySQL 节点进行检测和负载均衡，大家可以用 LVS+Keepalived 对 MySQL 主从做负载均衡
    + 均衡策略非常多：Round-robin（轮循）、Weight-round-robin（带权轮循）、source（原地址保持）、RI（请求URL）、rdp-cookie（根据cookie）
  - 日 PV 小于1000万，用 Nginx 就完全可以了；如果机器不少，可以用 DNS 轮询，LVS 所耗费的机器还是比较多的；大型网站或重要的服务，且服务器比较多时，可以考虑用 LVS
  - 合理流行架构方案：Web 前端采用 Nginx/HAProxy+Keepalived 作负载均衡器；后端采用 MySQL数据库一主多从和读写分离，采用 LVS+Keepalived 的架构
* Google于2016年3月最新公布的负载均衡Maglev
  - Maglev是谷歌为自己的数据中心研发的解决方案，并于2008开始用于生产环境。在第十三届网络系统设计与实现USENIX研讨会（NSDI '16）上， 来自谷歌、加州大学洛杉矶分校、SpaceX公司的工程师们分享了这一商用服务器负载均衡器Maglev的详细信息
  - Maglev安装后不需要预热5秒内就能应付每秒100万次请求令人惊叹不已。在谷歌的性能基准测试中，Maglev实例运行在一个8核CPU下，网络吞吐率上限为12M PPS(数据包每秒)，如果Maglev使用Linux内核网络堆栈则速度会小于4M PPS
* 国内云服务商 UCloud 进一步迭代了负载均衡产品----Vortex，成功地提升了单机性能
  - 在技术实现上，UCloud Vortex与Google Maglev颇为相似。以一台普通性价比的x86 1U服务器为例，Vortex可以实现吞吐量达14M PPS(10G, 64字节线速)，新建连接200k CPS以上，并发连接数达到3000万、10G线速的转发

## [keepalived](https://wsgzao.github.io/post/keepalived/)

* 运行在 lvs 之上，是一个用于做双机热备（HA）的软件，主要功能是实现真实机的故障隔离及负载均衡器间的失败切换，提高系统的可用性
  - keepalived 是 lvs 的扩展项目, 因此它们之间具备良好的兼容性
  - 对 RealServer 的健康检查, 实现对失效机器 / 服务的故障隔离
* 原理：keepalived 通过选举（看服务器设置的权重）挑选出一台热备服务器做 MASTER 机器，MASTER 机器会被分配到一个指定的虚拟 ip，外部程序可通过该 ip 访问这台服务器，如果这台服务器出现故障（断网，重启，或者本机器上的 keepalived crash 等），keepalived 会从其他的备份机器上重选（还是看服务器设置的权重）一台机器做 MASTER 并分配同样的虚拟 IP，充当前一台 MASTER 的角色
* 选举策略：根据 VRRP 协议，完全按照权重大小，权重最大（0～255）的是 MASTER 机器，下面几种情况会触发选举
  - keepalived 启动的时候
  - master 服务器出现故障（断网，重启，或者本机器上的 keepalived crash 等，而本机器上其他应用程序 crash 不算）
  - 有新的备份服务器加入且权重最大
* 配置
  - VRRPD 配置包括三个类:
    + VRRP 同步组(synchroization group)
    + VRRP 实例(VRRP Instance)
    + VRRP 脚本

```sh
# 全局定义 (global definition)
global_defs {
   notification_email {
   acassen@firewall.loc
   failover@firewall.loc
   sysadmin@firewall.loc
   }
   notification_email_from Alexandre.Cassen@firewall.loc
   smtp_server 192.168.200.1
   smtp_connect_timeout 30
   router_id LVS_DEVEL
}
#notification_email: 表示 keepalived 在发生诸如切换操作时需要发送 email 通知以及 email 发送给哪些邮件地址邮件地址可以多个每行一个
#notification_email_from admin@example.com: 表示发送通知邮件时邮件源地址是谁
#smtp_server 127.0.0.1: 表示发送 email 时使用的 smtp 服务器地址这里可以用本地的 sendmail 来实现
#smtp_connect_timeout 30: 连接 smtp 连接超时时间
#router_id node1: 机器标识，通常配置主机名

# 静态地址和路由配置范例
static_ipaddress {
    192.168.1.1/24 brd + dev eth0 scope global
    192.168.1.2/24 brd + dev eth1 scope global
}
static_routes {
    src $SRC_IP to $DST_IP dev $SRC_DEVICE
    src $SRC_IP to $DST_IP via $GW dev $SRC_DEVICE
}
# 这里实际上和系统里面命令配置 IP 地址和路由一样例如
# 192.168.1.1/24 brd + dev eth0 scope global 相当于: ip addr add 192.168.1.1/24 brd + dev eth0 scope global
# 就是给 eth0 配置 IP 地址路由同理, 一般这个区域不需要配置
# 这里实际上就是给服务器配置真实的 IP 地址和路由的在复杂的环境下可能需要配置一般不会用这个来配置我们可以直接用 vi /etc/sysconfig/network-script/ifcfg-eth1 来配置切记这里可不是 VIP 不要搞混淆了切记切记
```

### 算法

* 衡量标准
  - 是否意识到不同节点的服务能力是不一样的，比如CPU、内存、网络、地理位置
  - 是否意识到节点的服务能力是动态变化的，高配的机器也有可能由于一些突发原因导致处理速度变得很慢
  - 是否考虑将同一个客户端，或者说同样的请求分发到同一个处理节点，这对于“有状态”的服务非常重要，比如session，比如分布式存储
  - 谁来负责负载均衡，即谁充当负载均衡器（load balancer），balancer本身是否会成为瓶颈
* 方案
  - 轮询算法（round-robin）：提供同质服务的节点逐个对外提供服务，这样能做到绝对的均衡.
    - 没有考虑到节点的差异
  - 加权轮询算法（weight round-robin）:在轮训算法的基础上，考虑到机器的差异性，分配给机器不同的权重.依赖于请求的类型，比如计算密集型，那就考虑CPU、内存；如果是IO密集型，那就考虑磁盘性能
  - 随机算法（random）:随机选择一个节点服务，按照概率，只要请求数量足够多，那么也能达到绝对均衡的效果
  - 加权随机算法（random）:在随机的时候引入不同节点的权重
  - 哈希法（hash）：根据客户端的IP，或者请求的“Key”，计算出一个hash值，然后对节点数目取模。好处就是，同一个请求能够分配到同样的服务节点，这对于“有状态”的服务很有必要
    + 当节点的数目发生变化的时候，请求会大概率分配到其他的节点，引发到一系列问题
  - 一致性哈希算法：一个物理节点与多个虚拟节点映射，在hash的时候，使用虚拟节点数目而不是物理节点数目。当物理节点变化的时候，虚拟节点的数目无需变化，只涉及到虚拟节点的重新分配。而且，调整每个物理节点对应的虚拟节点数目，也就相当于每个物理节点有不同的权重
  - 最少连接算法（least connection）：根据节点的真实负载，动态地调整节点的权重就非常重要。当然，要获得接节点的真实负载也不是一概而论的事情，如何定义负载，负载的收集是否及时
    + 每个节点当前的连接数目是一个非常容易收集的指标，因此lease connection是最常被人提到的算法
  - 响应策略：将请求转发给当前时刻响应最快的后端服务器
    + 不停的去统计每一台后端服务器对请求的处理速度了

```python
SERVER_LIST = [
      '10.246.10.1',
     '10.246.10.2',
     '10.246.10.3',
 ]
 def round_robin(server_lst, cur = [0]):
     length = len(server_lst)
     ret = server_lst[cur[0] % length]
     cur[0] = (cur[0] + 1) % length
     return ret

 WEIGHT_SERVER_LIST = {
     '10.246.10.1': 1,
     '10.246.10.2': 3,
     '10.246.10.3': 2,
 }
 def weight_round_robin(servers, cur = [0]):
     weighted_list = []
     for k, v in servers.iteritems():
         weighted_list.extend([k] * v)

     length = len(weighted_list)
     ret = weighted_list[cur[0] % length]
     cur[0] = (cur[0] + 1) % length
     return ret

def random_choose(server_lst):
    import random
    random.seed()
    return random.choice(server_lst)

def weight_random_choose(servers):
    import random
    random.seed()
    weighted_list = []
    for k, v in servers.iteritems():
        weighted_list.extend([k] * v)
    return random.choice(weighted_list)

# 如果节点列表以及权重变化不大，那么也可以对所有节点归一化，然后按概率区间选择
def normalize_servers(servers):
    normalized_servers = {}
    total = sum(servers.values())
    cur_sum = 0
    for k, v in servers.iteritems():
        normalized_servers[k] = 1.0 * (cur_sum + v) / total
        cur_sum += v
    return normalized_servers

def weight_random_choose_ex(normalized_servers):
    import random, operator
    random.seed()
    rand = random.random()
    for k, v in sorted(normalized_servers.iteritems(), key = operator.itemgetter(1)):
        if v >= rand:
            return k
    else:
        assert False, 'Error normalized_servers with rand %s ' % rand

def hash_choose(request_info, server_lst):
     hashed_request_info = hash(request_info)
     return server_lst[hashed_request_info % len(server_lst)]
```

## 资源

* [Hprose](https://hprose.com):高性能远程对象服务引擎
* [Kickball/awesome-selfhosted](https://github.com/Kickball/awesome-selfhosted):This is a list of Free Software network services and web applications which can be hosted locally. Selfhosting is the process of locally hosting and managing applications instead of renting from SaaS providers. <https://reddit.com/r/selfhosted>
* [arialdomartini/Back-End-Developer-Interview-Questions](https://github.com/arialdomartini/Back-End-Developer-Interview-Questions):A list of back-end related questions you can be inspired from to interview potential candidates, test yourself or completely ignore
* [wx-chevalier/Backend-Series](https://github.com/wx-chevalier/Backend-Series):📚 服务端应用程序开发与系统架构/微服务架构与实践，服务端基础篇 | 微服务与云原生篇 | Spring 篇 | Node.js 篇 | DevOps 篇 | 信息安全与渗透测试篇
* [lemonchann/TechClass](https://github.com/lemonchann/TechClass):项目涵盖成为一个后端开发程序员必备的技能，包括Linux、网络、架构、微服务、数据库、数据结构和算法、编程语言学习等内容 <https://lemonchann.github.io/TechClass>

## 参考

* [dianping/camel](https://github.com/dianping/camel):软负载一体解决方案，承担了F5硬负载层后的软负载工作
* [cilium](https://github.com/cilium/cilium):API Aware Networking and Security using BPF and XDP
