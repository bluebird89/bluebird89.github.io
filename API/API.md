# API(Application Programming Interface）

实现前后端分离

*   请求地址
*   请求类型
*   参数说明
*   返回结果说明

## API gateway

* 幂等

### [encode/apistar](https://github.com/encode/apistar)

A smart Web API framework, for Python 3. 🌟 https://docs.apistar.com

* pip3 install apistar
* Create a new project in app.py, python app.py
* Open http://127.0.0.1:5000/docs/ in your browser

```py
from apistar import App, Route

def welcome(name=None):
    if name is None:
        return {'message': 'Welcome to API Star!'}
    return {'message': 'Welcome to API Star, %s!' % name}


routes = [
    Route('/', method='GET', handler=welcome),
]

app = App(routes=routes)


if __name__ == '__main__':
    app.serve('127.0.0.1', 5000, debug=True)
```

## 加密

* 考虑
    - 可变性：每次的签名必须是不一样的。
    - 时效性：每次请求的时效性，过期作废。
    - 唯一性：每次的签名是唯一的。
    - 完整性：能够对传入数据进行验证，防止篡改
* 方法
    - 发送方和接收方约定一个加密的盐值，进行生成签名。 `/api/login?username=xxx&password=xxx&sign=xxx`
    - 单向散列加密：把任意长的输入串变化成固定长的输出串，并且由输出串难以得到输入串
        + 算法：MD5 SHA MAC CRC
        + 优点
            * 方便存储：加密后都是固定大小（32位）的字符串，能够分配固定大小的空间存储。
            * 损耗低：加密/加密对于性能的损耗微乎其微。
            * 文件加密：只需要32位字符串就能对一个巨大的文件验证其完整性。
            * 不可逆：大多数的情况下不可逆，具有良好的安全性
        + 缺点：存在暴力破解的可能性，最好通过加盐值的方式提高安全性。
        + 场景：用于敏感数据，比如用户密码，请求参数，文件加密等。
        + 推荐：password_hash（）
    - 对称加密:同一个密钥可以同时用作数据的加密和解密
        + 算法：DES（AES 是 DES 的升级版，密钥长度更长，选择更多，也更灵活，安全性更高，速度更快） AES
        + 优点：算法公开、计算量小、加密速度快、加密效率高。
        + 缺点：发送方和接收方必须商定好密钥，然后使双方都能保存好密钥，密钥管理成为双方的负担。
        + 应用场景 相对大一点的数据量或关键数据的加密。
        + mcrypt_encrypt 和 mcrypt_decrypt在 PHP7.2 版本中已经被弃用了，在新版本中使用 openssl_encrypt 和 openssl_decrypt 两个方法
    - 非对称加密:需要两个密钥来进行加密和解密，这两个秘钥分别是公钥（public key）和私钥（private key）
        + 算法
            * RSA2  SHA256WithRSA   强制要求RSA密钥的长度至少为2048
            * RSA SHA1WithRSA 对RSA密钥的长度不限制，推荐使用2048位以上
        + 优点 与对称加密相比，安全性更好，加解密需要不同的密钥，公钥和私钥都可进行相互的加解密。
        + 缺点 加密和解密花费时间长、速度慢，只适合对少量数据进行加密。
        + 应用场景:适合于对安全性要求很高的场景，适合加密少量数据，比如支付数据、登录数据等。
* 密钥：
    - 将密钥设置到环境变量中，每次从环境变量中加载
    - 将密钥存放到配置中心，统一进行管理
    - 设置密钥有效期，比如一个月进行重置一次

```sh
openssl genrsa - out private_key . pem 2048
openssl rsa - in private_key . pem - pubout - out public_key . pem
```

### 方法

* [google/tink](https://github.com/google/tink):Tink is a multi-language, cross-platform library that provides cryptographic APIs that are secure, easy to use correctly, and hard(er) to misuse.
* [JSEncrypt](https://github.com/travist/jsencrypt):用于执行OpenSSL RSA加密、解密和密钥生成的Javascript库。WEB 的登录功能时一般是通过 Form 提交或 Ajax 方式提交到服务器进行验证的。为了防止抓包，登录密码肯定要先进行一次加密（RSA），再提交到服务器进行验证

## 流程

* 前后端和产品一起开会讨论项目
* 后端根据需求，首先定义数据格式和 api
* mock api 生成好文档
* 前端才是对接接口的
* postman测接口
* 这里推荐一个文档生成器 swagger
* mockjs + rap 或者 easy-mock

## 动态令牌

* OTP：One-Time Password 一次性密码。
* HOTP：HMAC-based One-Time Password 基于HMAC算法加密的一次性密码。
* TOTP：Time-based One-Time Password 基于时间戳算法的一次性密码。

### apidoc

* 配置
    - 每次导出接口文档都必须要让apidoc读取到apidoc.json文件(如果未添加配置文件，导出报错)，可以在项目的根目录下添加apidoc.json文件
    - 项目中使用了package.json文件(例如:node.js工程)，可以将apidoc.json文件中的所有配置信息放到package.json文件中的apidoc参数中
    - 参数
        + name
        + version
        + description
        + title
        + url
        + header.title
        + header.filename   页眉文件名(markdown)
        + footer.title    页脚导航标题
        + footer.filename     页脚文件名(markdown)
        + order   接口名称或接口组名称的排序列表,如果未定义，那么所有名称会自动排序 "Error", "Define", "PostTitleAndError", "PostError"

```
# 安装
npm install apidoc -g
apidoc -i myapp/ -o apidoc/ -t mytemplate/

# 支持中文title

# apidoc.json
{
  "name": "example",
  "version": "0.1.0",
  "description": "apiDoc basic example",
  "title": "Custom apiDoc browser title",
  "url" : "https://api.github.com/v1"
}

# package.json
{
  "name": "example",
  "version": "0.1.0",
  "description": "apiDoc basic example",
  "apidoc": {
    "title": "Custom apiDoc browser title",
    "url" : "https://api.github.com/v1"
  }
}
```

## 语法

```
# 注释模块: 通用可复用的注释模块(例如:接口错误响应模块),只需要在源代码中定义一次，便可以在其他注释模块中随便引用，最后在文档导出时会自动替换所引用的注释模块，定义之后您可以通过@apiUse来引入所定义的注释模块
/**
 * @apiDefine name [title]
                     [description]
 */
/**
 * @apiDefine MyError
 * @apiError [(group)] [{type}] field [description]
  * @apiError UserNotFound The <code>id</code> of the User was not found.
 */
/**
 * @apiDefine admin User access only
 * This optional description belong to to the group admin.
 */
/**
 * @apiDefine MySuccess
 * @apiSuccess {string} firstname The users firstname.
 * @apiSuccess {number} age The users age.
 */

# 标注一个接口已经被弃用
/**
 * @apiDeprecated use now (#Group:Name).
 *
 * Example: to set a link to the GetDetails method of your group User
 * write (#User:GetDetails)
 */

/**
 * @apiIgnore [hint]
 * @apiIgnore Not finished Method

 * @api {method} path [title]
 * @api {get} /user/:id

 * @apiVersion 1.6.2

 * @apiName name
 *
 * @apiDescription This is the Description.
 * It is multiline capable.
 *
 * Last line of Description.

 * @apiGroup User

 * @appUse MyError
 * @apiPermission admin|none
 * @apiUse MySuccess

 * # 定义为私有的接口，可以在生成接口文档的时候，通过在命令行中设置参数 --private false|true来决定导出的文档中是否包含私有接口
 * @apiPrivate
 *
 * 导出的html接口文档中会包含模拟接口请求的form表单；如果在配置文件apidoc.json中设置了参数sampleUrl,那么导出的文档中每一个接口都会包含模拟接口请求的form表单，如果既设置了sampleUrl参数，同时也不希望当前这个接口不包含模拟接口请求的form表单
 * @apiSampleRequest url
 * @apiSampleRequest off

 * @apiHeader [(group)] [{type}] [field=defaultValue] [description]
 * @apiHeader {String} access-key Users unique access-key.
 * @apiHeaderExample {json} Header-Example:
 *     {
 *       "Accept-Encoding": "Accept-Encoding: gzip, deflate"
 *     }
 *
 * @apiParam [(group)] [{type}] [field=defaultValue] [description]
 * @apiParam {Number} id Users unique ID.
 * @api {post} /user/
 * @apiParam {String} [firstname]  Optional Firstname of the User.
 * @apiParam {String} lastname     Mandatory Lastname.
 * @apiParam {String} country="DE" Mandatory with default value "DE".
 * @apiParam {Number} [age=18]     Optional Age with default 18.
 *
 * @apiParam (Login) {String} pass Only logged in users can post this.
 *                                 In generated documentation a separate
 *                                 "Login" Block will be generated.

 * @apiParamExample [{type}] [title]
                   example
 * @apiParamExample {json} Request-Example:
 *     {
 *       "id": 4711
 *     }
 *
 * @apiError UserNotFound The <code>id</code> of the User was not found.
 * @apiErrorExample [{type}] [title]
 *               example
 * @apiErrorExample {json} Error-Response:
 *     HTTP/1.1 404 Not Found
 *     {
 *       "error": "UserNotFound"
 *     }

 * @apiExample [{type}] title
            example
 * @apiExample {curl} Example usage:
 *     curl -i http://localhost/user/4711
 *
 * @apiSuccess [(group)] [{type}] field [description]
 * @apiSuccess (200) {String} lastname  Lastname of the User.
 * @apiSuccess {Boolean} active        Specify if the account is active.
 * @apiSuccess {Object}  profile       User profile information.
 * @apiSuccess {Number}  profile.age   Users age.
 * @apiSuccess {String}  profile.image Avatar-Image.
 *
 * @apiSuccessExample {json} Success-Response:
 *     HTTP/1.1 200 OK
 *     {
 *       "firstname": "John",
 *       "lastname": "Doe"
 *     }
 */

```

## 测试

* [apiaryio/dredd](https://github.com/apiaryio/dredd):Language-agnostic HTTP API Testing Tool https://dredd.org

## 接口

* [雅虎天气](https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20%3D%202151330&format=json)
* [价格](http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice)
* [Vespa314/bilibili-api](https://github.com/Vespa314/bilibili-api):B站API收集整理及开发，测试【开发中】 
* [douban](https://developers.douban.com/wiki/?title=guide)
* [jokermonn/-Api](https://github.com/jokermonn/-Api):📖「一个」、「Time 时光」、「开眼」、「一席」、「梨视频」、「微软必应词典」、「金山词典」、「豆瓣电影」、「中央天气」、「魅族天气」、「每日一文」、「12306」、「途牛」、「快递100」、「快递」应用 Api
* [toddmotto/public-apis](https://github.com/toddmotto/public-apis):A collective list of public JSON APIs for use in web development. https://toddmotto.com
* [pwxcoo/chinese-xinhua](https://github.com/pwxcoo/chinese-xinhua):📙 中华新华字典数据库。包括歇后语，成语，词语，汉字。提供新华字典API。
* [Binaryify/NeteaseCloudMusicApi](https://github.com/Binaryify/NeteaseCloudMusicApi):网易云音乐 Node.js API service https://binaryify.github.io/NeteaseCloudMusicApi/#/
* 豆瓣
    - [获取正在热映的电影](https://api.douban.com/v2/movie/in_theaters?city=广州&start=0&count=10)
    - [获取电影Top250](https://api.douban.com/v2/movie/top250?start=0&count=10)
    - [电影搜索](https://api.douban.com/v2/movie/search?q=神秘巨星&start=0&count=10)
    - [电影详情](https://api.douban.com/v2/movie/subject/26942674)

## Gateway

* [TykTechnologies/tyk](https://github.com/TykTechnologies/tyk)：Tyk Open Source API Gateway written in Go

## 工具

* [GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer):Headless Chrome Node API https://try-puppeteer.appspot.com/
* [thx/RAP](https://github.com/thx/RAP):Web接口管理工具，开源免费，接口自动化，MOCK数据自动生成，自动化测试，企业级管理。阿里妈妈MUX团队出品！阿里巴巴都在用！1000+公司的选择！RAP2已发布请移步至https://github.com/thx/rap2-delos http://rapapi.org
* [thx/rap2-delos](https://github.com/thx/rap2-delos):阿里妈妈前端团队出品的开源接口管理工具RAP第二代 http://rap2.taobao.org
* [encode/apistar](https://github.com/encode/apistar):A smart Web API framework, for Python 3. 🌟 https://docs.apistar.com
* [ruby-grape/grape](https://github.com/ruby-grape/grape):An opinionated framework for creating REST-like APIs in Ruby. http://www.ruby-grape.org
* [encode/django-rest-framework](https://github.com/encode/django-rest-framework):Web APIs for Django. ⚡️ https://www.django-rest-framework.org
* [paularmstrong/normalizr](https://github.com/paularmstrong/normalizr):Normalizes nested JSON according to a schema
* [swagger-api/swagger-ui](https://github.com/swagger-api/swagger-ui):Swagger UI is a collection of HTML, Javascript, and CSS assets that dynamically generate beautiful documentation from a Swagger-compliant API. http://swagger.io
* [dingo/api](https://github.com/dingo/api):A RESTful API package for the Laravel and Lumen frameworks.
* [parse-community/parse-server](https://github.com/parse-community/parse-server):Parse-compatible API server module for Node/Express http://parseplatform.org
* [interagent/http-api-design](https://github.com/interagent/http-api-design):HTTP API design guide extracted from work on the Heroku Platform API https://www.gitbook.com/read/book/gee…
* [typicode/json-server](https://github.com/typicode/json-server):Get a full fake REST API with zero coding in less than 30 seconds (seriously)
* [gongwalker/ApiManager](https://github.com/gongwalker/ApiManager):接口文档管理工具
* [tobscure/json-api](https://github.com/tobscure/json-api):JSON-API (http://jsonapi.org) responses in PHP.
* [hashicorp/vault](https://github.com/hashicorp/vault)：A tool for secrets management, encryption as a service, and privileged access management https://www.vaultproject.io/
* [nsf/termbox-go](https://github.com/nsf/termbox-go):Pure Go termbox implementation http://code.google.com/p/termbox
* [apiaryio/dredd](https://github.com/apiaryio/dredd):Language-agnostic HTTP API Testing Tool https://dredd.rtfd.io
* [hellofresh/janus](https://github.com/hellofresh/janus):An API Gateway written in Go https://hellofresh.gitbooks.io/janus
* [YMFE/yapi](https://github.com/YMFE/yapi):YApi 是一个可本地部署的、打通前后端及QA的、可视化的接口管理平台 http://yapi.demo.qunar.com/
* postman
* [SocketLog](https://github.com/luofei614/SocketLog)

## 文档

* [jsdoc3/jsdoc](https://github.com/jsdoc3/jsdoc):An API documentation generator for JavaScript. http://usejsdoc.org
* [swagger](https://app.swaggerhub.com/home)Swagger UI is a collection of HTML, Javascript, and CSS assets that dynamically generate beautiful documentation from a Swagger-compliant API. http://swagger.io
* [freeCodeCamp/devdocs](https://github.com/freeCodeCamp/devdocs):API Documentation Browser https://devdocs.io
* [lord/slate](https://github.com/lord/slate):Beautiful static documentation for your API https://spectrum.chat/slate
* YUI doc
* eolinker
* Apizza
* Yapi
* [RAP2](http://rap2.taobao.org)
* DOClever

## 参考

* [jsonapi](https://jsonapi.org/format/)
* [shieldfy/API-Security-Checklist](https://github.com/shieldfy/API-Security-Checklist):Checklist of the most important security countermeasures when designing, testing, and releasing your API
