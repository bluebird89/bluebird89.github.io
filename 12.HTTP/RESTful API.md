RESTful

C/S:请求端的分布式，建立在分布式体系上，通过互联网通信，具有高延时（high latency）、高并发等特点。如何开发在互联网环境中使用的软件。

REST（Representational State Transfer）这个词，是Roy Thomas Fielding在他2000年的博士论文中提出的。Fielding是一个非常重要的人，他是HTTP协议（1.0版和1.1版）的主要设计者、Apache服务器软件的作者之一、Apache基金会的第一任主席。

主语为资源 所谓"资源"，就是网络上的一个实体，或者说是网络上的一个具体信息。你可以用一个URI（统一资源定位符）指向它，每种资源对应一个特定的URI。要获取这个资源，访问它的URI就可以，因此URI就成了每一个资源的地址或独一无二的识别符。URI只代表资源的实体，不代表它的形式。严格地说，有些网址最后的".html"后缀名是不必要的，因为这个后缀名表示格式，属于"表现层"范畴，而URI应该只代表"资源"的位置。它的具体表现形式，应该在HTTP请求的头信息中用Accept和Content-Type字段指定，这两个字段才是对"表现层"的描述。

表现层："资源"是一种信息实体，它可以有多种外在表现形式。我们把"资源"具体呈现出来的形式，叫做它的"表现层"（Representation）。

状态转化（State Transfer）：访问一个网站，就代表了客户端和服务器的一个互动过程。在这个过程中，势必涉及到数据和状态的变化。 互联网通信协议HTTP协议，是一个无状态协议。这意味着，所有的状态都保存在服务器端。因此，如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）。而这种转化是建立在表现层之上的，所以就是"表现层状态转化"。 客户端用到的手段，只能是HTTP协议。具体来说，就是HTTP协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。它们分别对应四种基本操作：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源。

- （1）每一个URI代表一种资源； - （2）客户端和服务器之间，传递这种资源的某种表现层； - （3）客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。

注意：

- URI不包含动词，动词在http协议中
- 复杂动作做成服务含有参数

指南：

域名部署： <https://api.example.com/v1/> 或者 <https://example.org/api/v1/> 或者将版本号放在HTTP头信息中

路径endpoint：每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的"集合"（collection），所以API中的名词也应该使用复数。

HTTp动词：

```
GET（SELECT）：从服务器取出资源（一项或多项）。
POST（CREATE）：在服务器新建一个资源。
PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。
DELETE（DELETE）：从服务器删除资源。
```

还有两个不常用的HTTP动词。 HEAD：获取资源的元数据。 OPTIONS：获取信息，关于资源的哪些属性是客户端可以改变的。

例子： GET /zoos：列出所有动物园 POST /zoos：新建一个动物园 GET /zoos/ID：获取某个指定动物园的信息 PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息） PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息） DELETE /zoos/ID：删除某个动物园 GET /zoos/ID/animals：列出某个指定动物园的所有动物 DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物

过滤信息： ?limit=10：指定返回记录的数量 ?offset=10：指定返回记录的开始位置。 ?page=2&per_page=100：指定第几页，以及每页的记录数。 ?sortby=nameℴ=asc：指定返回结果按照哪个属性排序，以及排序顺序。 ?animal_type_id=1：指定筛选条件

状态码（Status Codes） 200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。 201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。 202 Accepted - [_]：表示一个请求已经进入后台排队（异步任务） 204 NO CONTENT - [DELETE]：用户删除数据成功。 400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。 401 Unauthorized - [_]：表示用户没有权限（令牌、用户名、密码错误）。 403 Forbidden - [_] 表示用户得到授权（与401错误相对），但是访问是被禁止的。 404 NOT FOUND - [_]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。 406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。 410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。 422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。 500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。

错误处理（Error handling） 如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error作为键名，出错信息作为键值即可。

返回结果 GET /collection：返回资源对象的列表（数组） GET /collection/resource：返回单个资源对象 POST /collection：返回新生成的资源对象 PUT /collection/resource：返回完整的资源对象 PATCH /collection/resource：返回完整的资源对象 DELETE /collection/resource：返回一个空文档

RESTful API最好做到Hypermedia，即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么。比如 api.example.com {"link": { "rel": "collection <https://www.example.com/zoos>", "href": "<https://api.example.com/zoos>", "title": "List of zoos", "type": "application/vnd.yourformat+json" }} rel表示这个API与当前网址的关系（collection关系，并给出该collection的网址），href表示API的路径，title表示API的标题，type表示返回类型。

API的身份认证应该使用OAuth 2.0框架。 （2）服务器返回的数据格式，应该尽量使用JSON，避免使用XML。