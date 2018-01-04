# Neo4j

Neo4j是一个图形数据库，这也就意味着它的数据并非保存在表或集合中，而是保存为节点以及节点之间的关系。在Neo4j中，节点以及关系都能够包含保存值的属性，此外：

* 可以为节点设置零或多个标签（例如Author或Book）
* 每个关系都对应一种类型（例如WROTE或FRIEND_OF）
* 关系总是从一个节点指向另一个节点（但可以在不考虑指向性的情况下进行查询）

特点

* 自带一套易于学习的查询语言（名为Cypher）
* 不使用schema，因此可以满足你的任何形式的需求
* 与关系型数据库相比，对于高度关联的数据（图形数据）的查询快速要快上许多
* 它的实体与关系结构非常自然地切合人类的直观感受
* 支持兼容ACID的事务操作
* 提供了一个高可用性模型，以支持大规模数据量的查询，支持备份、数据局部性以及冗余
* 提供了一个可视化的查询控制台，你不会对它感到厌倦的

不适用场景

* 记录大量基于事件的数据（例如日志条目或传感器数据）
* 对大规模分布式数据进行处理，类似于Hadoop
* 二进制数据存储
* 适合于保存在关系型数据库中的结构化数据

## 参考

* [](https://neo4j.com/)