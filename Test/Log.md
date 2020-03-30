# log

写日志  测试代码作为编码的一部分

## 原理

* 记录器 负责产生日志记录的原始信息，比如（原始信息，日志等级，时间，记录的位置）等信息
* 过滤器 负责按指定的过滤条件过滤掉我们不需要的日志（比如按日志等级过滤）
* 格式化器 :负责对原始日志信息按照我们想要的格式去格式化
* 输出器 负责将将要进行记录的日志（一般经过过滤器及格式化器的处理后）记录到日志目的地（例如：输出到文件中或者通过网络发送出去）

## 日志分析

* 使用数据库来进行日志分析，一个很重要的点就是如何将各种异构的日志文件导入到的数据库中，因为数据库首先需要按照固定格式创建表结构——这个过程通常称为 ETL。当数据导入后，可以采用大家熟悉的 SQL 进行日志的各种分析。
* 数据规模比较大的情况，一般会使用分布式技术
    - 采用 hadoop 存储日志数据，后续采用 MapReduce 的 job 或者 spark 等进行分析
    - 如果希望采用 SQL 的方案来分析，可以采用 Hive 这些类似数据库的系统。这类系统适合于批量的进行分析。如果需要实时分析则需要引入一些实时的处理系统。
* 问题
    - 日志分析最大的问题是字段抽取复杂:对所有日志进行字段抽取的工作量很大，其次日志会随着产品版本更新发生变化，而且日志入库时很难预知后续的分析对字段的需求。因此需要一个功能强大且易用的日志抽取功能，以及搜索时按需临时抽取字段的能力。
    - 需要灵活可配置的分析能力。 如果每次分析都需要写代码进行,工作量大而且使用的门槛比较高
    - 实时性和性能问题。随着日志数据量的增长，想要实时监控分析数据，就必然会影响系统性能。这二者的平衡与优化
* 日志分析中的搜索引擎主要用于数据的读写：即实时的接收最新产生的日志数据，并进行索引，以实时或者准实时的方式提供给用户进行搜索和统计分析。

## [allinurl / goaccess](https://github.com/allinurl/goaccess):GoAccess is a real-time web log analyzer and interactive viewer that runs in a terminal in *nix systems or through your browser. https://goaccess.io

* 完全实时 终端每200毫秒更新一次，HTML每秒更新一次。
* 需要最少的配置 直接接日志文件并运行，选择日志格式，然后让GoAccess解析访问日志并向您显示统计信息。
* 跟踪应用程序响应时间 跟踪服务请求所花费的时间。如果您要跟踪正在降低网站速度的页面，则非常有用。
* 几乎所有Web日志格式 GoAccess 允许使用任何自定义日志格式字符串。预定义的选项包括 Apache，Nginx，Amazon S3，Elastic Load Balancing，CloudFront等。
* 增量日志处理 需要数据持久性吗？GoAccess 能够通过磁盘 B + Tree 数据库增量处理日志。
* 仅一个依赖 GoAccess是用C语言编写的。要运行它，你只需要将 ncurses 作为依赖项
* 访问次数 按小时或日期来统计请求数，访问者，带宽等。
* 多个虚拟主机的指标 有多个虚拟主机？它具有一个面板，该面板显示哪个虚拟主机正在消耗大多数Web服务器资源。
* 颜色方案可定制的 Tailor GoAccess 可以适合您自己的颜色口味/方案。通过终端，或者简单地在HTML输出上应用样式表。
* 对大型数据集的支持 GoAccess 为大型数据集提供了一个磁盘B + Tree存储。
* Docker支持 能够从上游构建 GoAccess 的Docker映像。
* GoAccess允许任何自定义日志格式字符串。使用 -log-format 参数指定日志格式，预定义的选项包括但不限于：
    - COMBINED | 联合日志格式（Apache、Nginx等）
    - VCOMBINED | 支持虚拟主机的联合日志格式
    - COMMON | 通用日志格式
    - VCOMMON | 支持虚拟主机的通用日志格式
    - W3C | W3C 扩展日志格式
    - SQUID | Native Squid 日志格式
    - CLOUDFRONT | 亚马逊 CloudFront Web 分布式系统
    - CLOUDSTORAGE | 谷歌云存储
    - AWSELB | 亚马逊弹性负载均衡
    - AWSS3 | 亚马逊简单存储服务 (S3)
* 三种类型的存储方式
    - 默认哈希表 内存哈希表可以提供较好的性能，缺点是数据集的大小受限于物理内存的大小。GoAccess 默认使用内存哈希表。如果你的内存可以装下你的数据集，那么这种模式的表现非常棒。此模式具有非常好的内存利用率和性能表现。
    - Tokyo Cabinet 磁盘 B+ 树
使用这种模式来处理巨大的数据集，大到不可能在内存中完成任务。当数据提交到磁盘以后，B+树数据库比任何一种哈希数据库都要慢。但是，使用 SSD 可以极大的提高性能。往后您可能需要快速载入保存的数据，那么这种方式就可以被使用。
    - Tokyo Cabinet 内存哈希表 作为默认哈希表的替换方案。因为使用通用类型在内存表现以及速度方面都很平均
* 自定义 日志/日期 格式 配置文件位于：`%sysconfdir%/goaccess.conf` 或者 `~/.goaccessrc` `%sysconfdir%`` 可能是 `/etc/`, `/usr/etc/` 或者 `/usr/local/`etc/
    - time-format 参数 time-format 后跟随一个空格符，指定日志的时间格式，包含普通字符与特殊格式说明符的任意组合。他们都由百分号 (%)开始。参考 man strftime。%T 或者 %H:%M:%S 注意：如果给定的时间戳以微秒计算，则必须在 time-format 中使用参数 %f。
    - date-format 参数 date-format 后跟随一个空格符，指定日志的日期格式，包含普通字符与特殊格式说明符的任意组合。他们都由百分号 (%)开始。参考 man strftime。 注意：如果给定的时间戳以微秒计算，则必须在 date-format 中使用参数 %f 。
    - log-format 参数 log-format 后跟随一个空格符或者制表分隔符(\t)，用于指定日志字符串格式。
    - 特殊格式说明符
        + %x 匹配 time-format 和 date-format 变量的日期和时间字段。用于使用时间戳来代替日期和时间两个独立变量的场景。
        + %t 匹配 time-format 变量的时间字段。
        + %d 匹配 date-format 变量的日期字段。
        + %v 根据 canonical 名称设定的服务器名称(服务区或者虚拟主机)。
        + %e 请求文档时由 HTTP 验证决定的用户 ID。
        + %h 主机(客户端IP地址，IPv4 或者 IPv6)。
        + %r 客户端请求的行数。这些请求使用分隔符(单引号，双引号)引用的部分可以被解析。否则，需要使用由特殊格式说明符(例如：%m, - %U, %q 和 %H)组合格式去解析独立的字段。
        + 注意: 既可以使用 %r 获取完整的请求，也可以使用 %m, %U, %q and %H 去组合你的请求，但是不能同时使用。
        + %m 请求的方法。
        + %U 请求的 URL。
        + 注意: 如果查询字符串在 %U 中，则无需使用 %q。但是，如果 URL 路径中没有包含任何查询字符串，则你可以使用 %q 查询字符串将附加在请求后面。
        + %q 查询字符串。
        + %H 请求协议。
        + %s 服务器回传客户端的状态码。
        + %b 回传客户端的对象的大小。
        + %R HTTP 请求的 "Referer" 值。
        + %u HTTP 请求的 "UserAgent" 值。
        + %D 处理请求的时间消耗，使用微秒计算。
        + %T 处理请求的时间消耗，使用带秒和毫秒计算。
        + %L 处理请求的时间消耗，使用十进制数表示的毫秒计算。
        + %^ 忽略此字段。
        + %~ 继续解析日志字符串直到找到一个非空字符(!isspace)。
        + ~h 在 X-Forwarded-For (XFF) 字段中的主机(客户端 IP 地址，IPv4 或者 IPv6)。
* 参考
    - https://goaccess.cc/
    - https://github.com/allinurl/goaccess

```sh
# 源码安装
wget https://tar.goaccess.io/goaccess-1.3.tar.gz
tar -xzvf goaccess-1.3.tar.gz
cd goaccess-1.3/
./configure --enable-utf8 --enable-geoip=legacy
make
make install

# Debian / Ubuntu
echo "deb https://deb.goaccess.io/ $(lsb_release -cs) main" | sudo tee -a /etc/apt/sources.list.d/    goaccess.list
wget -O - https://deb.goaccess.io/gnugpg.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install goaccess
## 注意事项： 要获得磁盘上的支持（Trusty + 或 Wheezy +），请运行：
sudo apt-get install goaccess-tcb

# CentOS / RedHat
yum install goaccess -y

# OS X / Homebrew
brew install goaccess

# 要输出到终端并生成交互式报告
goaccess access.log

# 生成 HTML 报告
goaccess --log-format=COMBINED access.log -a > report.html
# 生成 JSON 报告
goaccess --log-format=COMBINED access.log -a -d -o json > report.json
# 生成 CSV 文件
goaccess --log-format=COMBINED access.log --no-csv-summary -o csv > report.csv
# GoAccess 还为实时过滤和解析提供了极大的灵活性。例如，要从goaccess启动以来通过监视日志来快速诊断问题：
tail -f access.log | goaccess -
# 更妙的是，进行筛选，同时保持打开的管道保持实时分析，我们可以利用的 tail -f 和匹配模式的工具，如grep，awk，sed，等：
tail -f access.log | grep -i --line-buffered 'firefox' | goaccess --log-format=COMBINED -
# 或从文件的开头进行解析，同时保持管道处于打开状态并应用过滤器
tail -f -n +0 access.log | grep -i --line-buffered 'firefox' | goaccess -o report.html    --real-time-html -
# 监示多个日志文件
goaccess access.log access.log.1
# 实时 HTML 输出 生成实时HTML报告的过程与创建静态报告的过程非常相似。只--real-time-html需要使其实时即可。
goaccess --log-format=COMBINED access.log -o /usr/share/nginx/html/your_s
```

## 工具

* [Graylog2/graylog2-server](https://github.com/Graylog2/graylog2-server):Free and open source log management https://www.graylog.org/
* [klaussinani/signale](https://github.com/klaussinani/signale):👋 Hackable console logger
* [Graylog](https://www.graylog.org/products/open-source)
* [Nagios](https://www.nagios.org/downloads/)
* [Elastic Stack](https://www.elastic.co/products)
    - *Elasticsearch* 旨在帮助用户使用多种查询语言和类型在数据集中找出匹配项。速度是这个工具的最大优势。它可以扩展成由数百个服务器节点组成的集群，轻松处理 PB 级的数据。
    - *Kibana* 是一个可视化工具，它与 Elasticsearch 一起运行，允许用户分析他们的数据并构建强大的报告。当你第一次在服务器集群上安装 Kibana 引擎时，你将获得一个显示数据统计、图形甚至动画的界面。
    - *Logstash*，它是作为一个纯粹的、进入 Elasticsearch 数据库的服务器端管道。你可以使用各种编码语言和 API 集成 Logstash。这样，你的网站和移动应用程序中的信息就可以直接输入到强大的 Elastic Stalk 搜索引擎中。
* [LOGalyze](http://www.logalyze.com)
* [Fluentd](https://www.fluentd.org)
* [rsyslog/rsyslog](https://github.com/rsyslog/rsyslog):a Rocket-fast SYStem for LOG processing http://www.rsyslog.com
