# [mongo](https://github.com/mongodb/mongo)

The MongoDB Database <https://www.mongodb.com/>

* 由C＋＋写就，其名字来自humongous这个单词的中间部分。关于它的一个最简洁描述为：scalable, high-performance, open source, schema-free, document-oriented database。MongoDB的主要目标是在键/值存储方式（提供了高性能和高度伸缩性）以及传统的RDBMS系统（丰富的功能）架起一座桥梁，集两者的优势于一身。
* 数据结构：db->collection->document（BSON（binary json）存放于硬盘）,BSON是Binary JSON 的简称，是一个JSON文档对象的二进制编码格式。BSON同JSON一样支持往其它文档对象和数组中再插入文档对象和数组，同时扩展了JSON的数据类型。如：BSON有Date类型和BinDate类型。
* BSON被比作二进制的交换格式，如同Protocol Buffers，但BSON比它更“schema-less”，非常好的灵活性但空间占用稍微大一点
* 跟一般的key-value数据库不一样的是，它的value中存储了结构信息,以单文档为单位存储的，可以任意给一个或一批文档新增或删除字段，而不会对其它文档造成影响，这就是所谓的schema-free，这也是文档型数据库最主要的优点。
* 最大的特点是支持的查询语言非常强大，其语法有点类似于面向对象的查询语言，几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引。Mongo还可以解决海量数据的查询效率，根据官方文档，当数据量达到50GB以上数据时，Mongo数据库访问速度是MySQL10 倍以上。

## 安装

* 下载安装（或通过包工具）
* 添加系统变量：C:\Program Files\MongoDB\Server\3.4\bin（echo 'export PATH=/usr/local/mongodb/bin:$PATH'>>~/.bash_profile）
* 创建数据库文件路径:C:\data\db(/data/db)
* 通过命令行工具启动服务: mongod（本地访问<http://localhost:27017/）MongoDB系统的主要守护进程，用于处理数据请求，数据访问和执行后台管理操作，必须启动，才能访问MongoDB数据库>
* [软件源](ttp://repo.mongodb.org/apt/ubuntu/dists/)
* PHP不同版本的扩展库使用版本不一样 php5 使用内置方法 php7.1 使用composer扩展mongodb/mongodb

```sh
### ubnutu
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list  # MongoDB尚未发布Bionic Beaver软件包，但Xenial软件包在Ubuntu 18.04 LTS上运行良好,。 如果您在该网页上看到一个目录“b ionic”，则将上述命令中的单词“xenial”替换为“bionic”一词。
sudo apt-get  update
sudo apt-get install -y mongodb-org

systemctl start mongod # 启动MongoDB
systemctl enable mongod # 添加为在启动时启动的服务

sudo service mongodb start | stop | restart
pgrep mongo -l # 查看服务状态

sudo apt-get --purge remove mongodb mongodb-clients mongodb-server # 卸载

## Mac
brew services mongodb # 启动服务

mongo -version
```

## 特点

* 事务支持：目前只支持单文档事务，需要复杂事务支持的场景暂时不适合
* 灵活的文档模型：没有固定的Schema，JSON 格式存储最接近真实对象模型，对开发者友好，方便快速开发迭代
* 高可用复制集 满足数据高可靠、服务高可用的需求，运维简单，故障自动切换
* 可扩展分片集群 海量数据存储，服务能力水平扩展
* 高性能 mmapv1、wiredtiger、mongorocks（rocksdb）、in-memory 等多引擎支持满足各种场景需求
* 强大的索引支持 地理位置索引可用于构建 各种 O2O 应用、文本索引解决搜索的需求、TTL 索引解决历史数据自动过期的需求
* Gridfs 解决文件存储的需求
* aggregation & mapreduce 解决数据分析场景需求，用户可以自己写查询语句或脚本，将请求都分发到 MongoDB 上完成

### 服务端配置

* 配置文件:/etc/mongod.conf
* 开启mongo服务端的命令，参数写入配置文档，以参数-f启动 `mongod -f C:datadbmongodb_config.config`

* --dbpath ：存储MongoDB数据文件的目录`mongod * --dbpath=C:datadb`
* --directoryperdb：指定每个数据库单独存储在一个目录中（directory），该目录位于–dbpath指定的目录下，每一个子目录都对应一个数据库名字。
* --logpath ：指定mongod记录日志的文件
* --fork：以后台deamon形式运行服务mongod -fork
* --journal：开始日志功能，通过保存操作日志来降低单机故障的恢复时间
* --config（或-f）：配置文件，用于指定runtime options
* --bind_ip ：指定对外服务的绑定IP地址
* --port ：指定mongo连接到mongod监听的TCP端口，默认的端口值是27017；
* --auth：启用验证，验证用户权限控制
* --syncdelay：系统刷新disk的时间，单位是second，默认是60s
* --replSet ：以副本集方式启动mongod，副本集的标识是setname
* --nodb: 阻止mongo在启动时连接到数据库实例；
* --host ：指定mongod运行的server，如果没有指定该参数，那么mongo尝试连接运行在本地（localhost）的mongod实例；
* --db：指定mongo连接的数据库
* --username/-u 和 –password/-p ：指定访问MongoDB数据库的账户和密码，只有当认证通过后，用户才能访问数据库；
* --authenticationDatabase ：指定创建User的数据库，在哪个数据库中创建User时，该数据库就是User的Authentication Database；

```sh
# 服务启动
/usr/bin/mongod -auth --config /etc/mongod.conf

`#pt-online-schema-change  --alter="add index   IX_id_no(id_no)"  \    --no-check-replication-filters  --recursion-method=none  --user=dba    \    --password=123456  D=test,t=t1 --execute`

＃　对于MongoDB创建索引要在后台创建，避免锁表,使用范例
db.t1.createIndex({idCardNum:1},{background:1})

bindIp:  127.0.0.1  修改为：bindIp:  0.0.0.0

# 添加超级管理员,客戶端鏈接需要選擇修改類型 basic
db.createUser(
  {
    user: "adminee",
    pwd: "admin",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
db.auth("adminee","admin")

# add root
db.createUser({user:"admin", pwd:"admin123", roles:[{role:"root", db:"admin"}]})
ExecStart=/usr/bin/mongod –auth –config /etc/mongod.conf # nano /lib/systemd/system/mongod.service add auth

systemctl daemon-reload # 重新加载systemd服务
sudo service mongod restart

mongo -u admin -p admin123 --authenticationDatabase admin
```

### 客户端

* 如果_id已经存在，insert不做操作，save做更新操作；如果不加_id字段，两者作用相同都是插入数据
* 添加的数据其结构是松散的，只要是bson格式均可，列属性均不固定，根据添加的数据为准。先定义数据再插入，就可以一次性插入多条数据
* 不需要预先定义 collection ，在第一次插入数据后，collection 会自动的创建
* 条件操作符
  - $gt : >
  - $lt : <
  - $gte: >=
  - $lte: <=
  - $ne : !=、<>
  - $in : in
  - $nin: not in
  - $all: all
  - $not:

```sql
mongo --help

mongoimport --db test --collection restaurants --drop --file ~/Downloads/primer-dataset.json
mongo
help

# 查看mongod的启动参数
db.serverCmdLineOpts()
```

## 库操作

```sql
# 显示数据库列表
show dbs

use yourDB # 切换当前数据库至yourDB
db.getName() # 获取数据库名称
db.dropDatabase() # 删除数据库
db.help() # 显示数据库操作命令
```

## 集合操作

```sql
show collections # 显示当前数据库中的集合（类似关系数据库中的表table）
db.yourCollection.help() # 显示集合操作命令
db.getCollectionNames()
db.printCollectionStats() # 查看各collection的状态
db.createColletion(‘byc’) # 创建集合
db.copyDatabase('mail_addr','mail_addr_tmp') # 拷贝数据库
db.test.drop() # 删除指定集合
# 删除一个集合
db.collection.deleteOne()
# 删除多个集合
db.collection.deletMany()
```

## 数据操作

```sql
db.users.insert({"name":"name 1",age:21})
db.student.insert({_id:1, sname: 'zhangsan', sage: 20}) #_id可选
db.student.save({_id:1, sname: 'zhangsan', sage: 22}) #_id可选
# 循环插入10条记录
for(var i=1;i<=10;i++){
    db.test.insert({"name":"king"+i,"age":i})
}

var arr= [];
for(var i=0;i<10000;i++){
   arr.push({counter:i});
}
db.restaurants.insert(arr);

db.restaurants.find()
db.restaurants.findOne()
db.restaurants.find().pretty() # 格式化显示查询结果
db.restaurants.find().count() # 查询数据条数

db.restaurants.find( { "address.zipcode": "10075" } ).limit(10)
db.restaurants.find().skip(3).limit(5);  # 从第3条记录开始，返回5条记录(limit 3, 5)

db.restaurants.find( { "grades.score": { $gt: 30 } } )
db.users.find({$where: "this.age > 18"});
db.users.find("this.age > 18");
db.restaurants.find({counter:{$gt:66, $lt:666}});
db.restaurants.find( { "cuisine": "Italian", "address.zipcode": "10075" } ) # and
db.restaurants.find( { $or: [ { "cuisine": "Italian" }, { "address.zipcode": "10075" } ] }) # or
db.users.find({creation_date:{$gt:new Date(2010,0,1), $lte:new Date(2010,11,31)}); # 查询 creation_date > '2010-01-01' and creation_date <= '2010-12-31' 的数据
db.users.find({name: {$ne: "bruce"}, age: {$gte: 18}});  # 查询 name <> "bruce" and age >= 18 的数据
db.users.find({age: {$in: [20,22,24,26]}}); # 查询 age in (20,22,24,26) 的数据
db.users.find('this.age % 10 == 0'); # 查询 age取模10等于0 的数据
db.users.find({age : {$mod : [10, 0]}});  # 取模10等于0 的数据
db.users.find({favorite_number : {$all : [6, 8]}});
db.users.find({name: {$not: /^B.*/}}); # 查询不匹配name=B*带头的记录
db.users.find({age : {$not: {$mod : [10, 0]}}}); # 查询 age取模10不等于0 的数据

# 设置第二个参数：字段中部分内容或者提取这个字段内的部分内容，1显示 0隐藏 _id如果不设置默认是1
db.users.find({ name : "bruce" }, {age:1, address:1}); # 选择返回age、address和_id字段
db.users.find({name: {$exists: true}}); # 查询所有存在name字段的记录
db.users.find({name: {$type: 2}}); # 查询所有name字段是字符类型的
db.users.find({age: {$type: 16}}); # 查询所有age字段是整型的
db.users.find({name: /^b.*/i}); # 查询以字母b或者B带头的所有记录

## 排序
db.restaurants.find().sort( { "borough": 1, "address.zipcode": 1 } ) # sort  1 for ascending and -1 for descending.

db.test.distinct('msg')

db.restaurants.update(
    { "name" : "Juni" },
    {
      $set: { "cuisine": "American (New)" },
      $currentDate: { "lastModified": true }
    }
)
# Update Multiple Documents
db.restaurants.update(
  { "address.zipcode": "10016", cuisine: "Other" },
  {
    $set: {
    cuisine: "Category To Be Determined" },
    $currentDate: { "lastModified": true }
  },
  { multi: true}
)
# To replace the entire document except for the _id field
db.restaurants.update(
   { "restaurant_id" : "41704620" },
   {
     "name" : "Vella 2",
     "address" : {
              "coord" : [ -73.9557413, 40.7720266 ],
              "building" : "1480",
              "street" : "2 Avenue",
              "zipcode" : "10075"
     }
   }
)
db.student.update(
  {"_id" : ObjectId("5bd6a46f1eb7a22fa07cb382")},
    {
      $set:{
        isDel:1
      }
    }
);
# group 格式
db.restaurants.aggregate(
   [
     { $group: { "_id": "$borough", "count": { $sum: 1 } } }
   ]
);
# 含有where条件
db.restaurants.aggregate(
   [
     { $match: { "borough": "Queens", "cuisine": "Brazilian" } },
     { $group: { "_id": "$address.zipcode" , "count": { $sum: 1 } } }
   ]
);

db.restaurants.remove( { "borough": "Manhattan" } )
db.restaurants.remove( { "borough": "Queens" }, { justOne: true } ) # limit the remove operation to only one of the matching documents
db.restaurants.remove( { "borough": "Queens" },  true) # limit the remove operation to only one of the matching documents
db.restaurants.remove( { } ) # Remove All Documents

# 索引管理
db.restaurants.createIndex( { "cuisine": 1 } )
db.restaurants.createIndex( { "cuisine": 1, "address.zipcode": -1 } )

show profile # 查看profiling
```

## 用户管理

```sql
use admin # 进入数据库admin
show users # 显示所有用户

db.addUser('name','pwd')
db.system.users.find() # 查看用户列表

db.removeUser('name') # 删除用户
db.auth('name','pwd') # 用户认证

db.shutdownServer() # 退出命令行
```

## 数据关系

* 一对一
* 一对多
* 多对多

```js
// 一对一
db.aAndb.insert([
 {name:"杨过",wife:{name:"小龙女",sex:"女"},sex:"男"},
  {name:"杨过",wife:{name:"小龙女",sex:"女"},sex:"男"}
])


// 一对多  比如  微博 和 微博评论
db.weibo.insert([
  {weibo:"世界这么大，我想去看看"},
  {weibo:"我要做一名web开发者！！！"}
])
db.weibo.find();
db.comments.insert([
{
weibo_id: ObjectId("5bdd89e06a5e78f4cfc2b9c8"),
list:[
   "那你有钱吗",
    "一个人吗？？去呢啊？？",
    "加油！！"
]
},
{
weibo_id: ObjectId("5bdd89e06a5e78f4cfc2b9c9"),
list:[
   "那你要学习HTML",
   "那还要你要学习css",
    "加油！！"
]
}
]);
db.comments.find();
// # 查询一对多
var weibo_id= db.weibo.findOne({"weibo" : "世界这么大，我想去看看"})._id;
db.comments.find({weibo_id: weibo_id});

// # 多对多 老师《------》学生
//插入老师集合
db.teachers.insert([
{
  name:"语文老师",
  teacher_id: 1,
  student_id:[
     1001,
     1002,
     1003
  ]
  },
{
  name:"数学老师",
  teacher_id: 2,
  student_id:[
     1001,
     1002,
     1003
  ]
  },
{
  name:"英语老师",
  teacher_id: 3,
  student_id:[
     1001,
     1002,
     1003
  ]
 }
])
db.teachers.find();

//插入学生集合
db.students.insert([
{
  name:"小明",
  student_id: 1001,
  teacher_id:[
     1,
     2,
     3
  ]
  },
{
  name:"小红",
  student_id: 1002,
  teacher_id:[
     1,
     2,
     3
  ]
  },
{
  name:"小刚",
  student_id: 1003,
  teacher_id:[
     1,
     2,
     3
  ]
 }
])

db.students.find();
db.teachers.find();
```

## mongodump mongorestore

备份和恢复数据库

## mongoexport mongoimport

导入导出JSON、CSV和TSV数据

## mongosniff

网络嗅探工具，用来观察发送到数据库的操作

## docker

- `mkdir -p ~/mongo ~/mongo/db` #  db目录将映射为mongo容器配置的/data/db目录,作为mongo数据的存储目录
- 创建Dockerfile

```
FROM debian:wheezy

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added

RUN groupadd -r mongodb && useradd -r -g mongodb mongodb

RUN apt-get update \ && apt-get install -y --no-install-recommends \ numactl \ && rm -rf /var/lib/apt/lists/*

# grab gosu for easy step-down from root

ENV GOSU_VERSION 1.7 RUN set -x \ && apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \ && wget -O /usr/local/bin/gosu "<https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg> --print-architecture)" \ && wget -O /usr/local/bin/gosu.asc "<https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg> --print-architecture).asc" \ && export GNUPGHOME="$(mktemp -d)" \ && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \ && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \ && rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \ && chmod +x /usr/local/bin/gosu \ && gosu nobody true \ && apt-get purge -y --auto-remove ca-certificates wget

# gpg: key 7F0CEB10: public key "Richard Kreuter [richard@10gen.com](mailto:richard@10gen.com)" imported

RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 492EAFE8CD016A07919F1D2B9ECBEC467F0CEB10

ENV MONGO_MAJOR 3.0 ENV MONGO_VERSION 3.0.12

RUN echo "deb <http://repo.mongodb.org/apt/debian> wheezy/mongodb-org/$MONGO_MAJOR main" > /etc/apt/sources.list.d/mongodb-org.list

RUN set -x \ && apt-get update \ && apt-get install -y \ mongodb-org=$MONGO_VERSION \ mongodb-org-server=$MONGO_VERSION \ mongodb-org-shell=$MONGO_VERSION \ mongodb-org-mongos=$MONGO_VERSION \ mongodb-org-tools=$MONGO_VERSION \ && rm -rf /var/lib/apt/lists/* \ && rm -rf /var/lib/mongodb \ && mv /etc/mongod.conf /etc/mongod.conf.orig

RUN mkdir -p /data/db /data/configdb \ && chown -R mongodb:mongodb /data/db /data/configdb VOLUME /data/db /data/configdb

COPY docker-entrypoint.sh /entrypoint.sh ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 27017 CMD ["mongod"]
```

- docker build -t mongo:3.2 .
- docker run -p 27017:27017 -v $PWD/db:/data/db -d mongo:3.2

## 水平扩展

MongoDB 中的 Sharding 正式为了水平扩展而设计的。MongoDB 中通过 Shard 支持服务器水平扩展，通过 Replication 支持高可用（HA）。

### MongoDB Shard

* 将数据库表中的数据按照一定的边界分成若干组，每一组放到一台 MongoDB 服务器上。以用户年龄age为进行Sharding（切分）的Shard Key。每一个 Shard 服务器存储数据的一个子集，
* 查询时通过mongos，它可以被称为 Shard 集群中的路由器。处理来自应用服务器的请求，它是在应用服务器和Shard 集群之间的一个接口。
* config server，它存储 Shard 集群中所有其他成员的配置信息，mongos会到这台config server查看集群中其他服务器的地址，这是一台不需要太高性能的服务器，因为它不会用来做复杂的查询计算，值得注意的是，在 MongoDB3.4 以后，config server必须是一个replica set。存储 shard 集群的配置信息，通常部署在一个 replica set 上。
* [mtools](https://github.com/rueckstiess/mtools):A collection of scripts to set up MongoDB test environments and parse and visualize MongoDB log files.是用来创建各种 MongoDB 环境的命令行工具，代码使用python写的，可以通过pip install安装到你的环境上

## 图书

* 《MongoDB The Definitive Guide》
* MongoDB大数据处理权威指南（第2版）
* NoSQL数据库技术实战

## 工具

* [shortid](https://github.com/dylang/shortid):Short id generator. Url-friendly. Non-predictable. Cluster-compatible. <https://www.npmjs.org/package/shortid>
* 客户端
  - [Robo 3T](https://robomongo.org/):Robo 3T (formerly Robomongo) is the free lightweight GUI for MongoDB enthusiasts.
  - [robomongo](https://github.com/Studio3T/robomongo):Native cross-platform MongoDB management tool <http://robomongo.org>
  - [Studio 3T](https://studio3t.com/):Studio 3T is the GUI that makes working with MongoDB easy.Available for Windows, Mac, and Linux.
  - [NoSQLBooster](https://nosqlbooster.com/):NoSQLBooster for MongoDB (formerly MongoBooster) is a shell-centric cross-platform GUI tool for MongoDB v2.6-3.6, which provides fluent query builder, SQL query SQL Query, update-in-place, ES2017 syntax support and true intellisense experience.
  - [mongoose](https://github.com/Automattic/mongoose):MongoDB object modeling designed to work in an asynchronous environment. <http://mongoosejs.com>
* 云服务
  - [mlab](https://mlab.com/):Database-as-a-Service for MongoDB

## 参考

* [MongoDB Docs](https://docs.mongodb.com/)
* [mongo-cluster-docker](https://github.com/senssei/mongo-cluster-docker):Docker compose config for mongodb cluster
* [MongoDB的水平扩展，你做对了吗？](https://juejin.im/entry/5a0266a76fb9a0450908ec76)
* [MongoDB集群优化](https://mp.weixin.qq.com/s?__biz=MzI4NTA1MDEwNg==&mid=2650785533&idx=1&sn=ceeb7833d721ab5c5a9ae76397405f93&chksm=f3f97368c48efa7ef6cb96ec4cbc2b1bc50f4510bcba7bb48dffd76be509d36b8fb099574446)
