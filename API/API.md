# API（Application Programming Interface) 应用程序编程接口

一些预先定义的函数或者接口，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无须访问源码，或理解内部工作机制的细节

* A well defined pipeline to process requests
* REST API done right (methods, status code and headers)
* Validation made easy
* Security beared in mind
* Policy based request throttling
* Easy to add new APIs
* Easy to document and test
* Introspection
    - API 系统自动收集 metrics，自我监控
    - 无论是撰写者，还是调用者，都很很方便的获取想要获取的信息

## 状态

* 前后端分离，业界广泛采用token方式
* 动态令牌
  - OTP：One-Time Password 一次性密码
  - HOTP：HMAC-based One-Time Password 基于HMAC算法加密的一次性密码
  - TOTP：Time-based One-Time Password 基于时间戳算法的一次性密码
* 初始
    - 第一次来登记的时候，服务器根据用户出具信息，在核验完毕身份证后（验证密码）后，发放token
    - 客户端保存token,后面访问接口时带上token
    - token 加有效期
        + 通过抓包等方式得知了服务器API的地址，就意味着可以任意调用API了，API会被盗用。为了避免这种被盗用，引入签名机制
* 签名机制：采取多数据项、用md5或者sha1
    - 固定字符串，或有规律字符串。如果客户端被反编译了，签名机制就会被人得知。所以，引入另外一个新的重要元素：时间戳
    - 时间戳
        + 判定API访问的时效性
        + 参与签名运算
    + 考虑
        + 可变性：每次的签名必须是不一样的
        + 时效性：每次请求的时效性，过期作废
        + 唯一性：每次的签名是唯一的
        + 完整性：能够对传入数据进行验证，防止篡改
    - 方法
        + 发送方和接收方约定一个加密的盐值，进行生成签名 `/api/login?username=xxx&password=xxx&sign=xxx`
        + 单向散列加密：把任意长的输入串变化成固定长的输出串，并且由输出串难以得到输入串
            * 算法：MD5 SHA MAC CRC
            * 优点
                - 方便存储：加密后都是固定大小（32位）的字符串，能够分配固定大小的空间存储。
                - 损耗低：加密/加密对于性能的损耗微乎其微。
                - 文件加密：只需要32位字符串就能对一个巨大的文件验证其完整性。
                - 不可逆：大多数的情况下不可逆，具有良好的安全性
            * 缺点：存在暴力破解的可能性，最好通过加盐值的方式提高安全性。
            * 场景：用于敏感数据，比如用户密码，请求参数，文件加密等。
            * 推荐：password_hash（）
        + 对称加密:同一个密钥可以同时用作数据的加密和解密
            * 算法：DES（AES 是 DES 的升级版，密钥长度更长，选择更多，也更灵活，安全性更高，速度更快） AES
            * 优点：算法公开、计算量小、加密速度快、加密效率高。
            * 缺点：发送方和接收方必须商定好密钥，然后使双方都能保存好密钥，密钥管理成为双方的负担。
            * 应用场景 相对大一点的数据量或关键数据的加密。
            * mcrypt_encrypt 和 mcrypt_decrypt在 PHP7.2 版本中已经被弃用了，在新版本中使用 openssl_encrypt 和 openssl_decrypt 两个方法
        + 非对称加密:需要两个密钥来进行加密和解密，这两个秘钥分别是公钥（public key）和私钥（private key）
            * 算法
                - RSA2  SHA256WithRSA   强制要求RSA密钥的长度至少为2048
                - RSA SHA1WithRSA 对RSA密钥的长度不限制，推荐使用2048位以上
            * 优点 与对称加密相比，安全性更好，加解密需要不同的密钥，公钥和私钥都可进行相互的加解密。
            * 缺点 加密和解密花费时间长、速度慢，只适合对少量数据进行加密。
            * 应用场景:适合于对安全性要求很高的场景，适合加密少量数据，比如支付数据、登录数据等。
    - 密钥：
        + 将密钥设置到环境变量中，每次从环境变量中加载
        + 将密钥存放到配置中心，统一进行管理
        + 设置密钥有效期，比如一个月进行重置一次
* 只要客户端被反编译了，加密方式和签名机制都会暴露出来，所以安全是需要双方配合的
* token或者aes加解密密码:建议走POST方式，也可以将这些信息放到http header中，也可以放到http body中
* Nonce
  - nonce 是个单调递增的整数。当某个后来的请求的 nonce，比上一个成功收到的请求的 nouce 小或者相等的时候，便会拒绝这次请求。这样一来，重复的包就不会被执行两次了
  - 可以在一定程度上防止中间人攻击
    + 是因为 nonce 的加入，使得加密后的同样订单的加密文本完全混乱
    + 会使得中间人无法通过“发送同样的包来构造重复订单“进行攻击
  - 频率较高的交易中，timestamp 可能就不是那么适合,协程 or 异步.代码很可能在发送的时候，并不是按照你想要的顺序发送给服务器，就会出现 timestamp 更大的请求反而更早发送。其次，在网络传输中，不同的包也可能有完全不同的抵达顺序，虽然你可以通过一些编程技巧来实现按顺序传输，但是如果你需要多台机器进行较为高频的交易。而且需要对同一个仓位（同一个 API Key）进行操作，就可能会变得比较麻烦

```
// 第一步请求
http.post( 'http://host.com/api/account/login', { "account":"zhengsan", "password":"123456" } ).signature( "api/account/login"+"timestamp" )
http.post( 'http://host.com/api/order/list', { "token" : "abcdefg" } ).signature( 'api/order/list' )

// 服务端验证密码并返回token
client_timestamp = get_post( 'timestamp' )
if( server_timestamp - cilent_timestamp > 30 ){
  return '过期API访问'
}
server_signature = md5( 'api/account/login' )
client_signature = http.get_post( 'signature' )
if ( server_signature != client_signature ) {
  return 'signature error';
}

password = get_post( 'password' )
account = get_post( 'account' )
server_password = get_password_by_account( 'account' )
if( password == server_password ){
  // 生成一个AES加密密码
  enc_password = "1a2b3c4d5f6g7h8i9j0k"
  // 生成原始的token
  token = "0k9j8h7i6g5f4c3b2c1az9y8x7"
  // 服务端记录token与uid对应关系
  set( token, uid )
  // 最后一步很重要，要将aes加密密码 和 token返回给客户端
  return enc_password,token
}

// 第三步，客户端收到登录后的数据：加解密密码 和 token，然后保存起来
token = get( 'token' )
enc_password = get('enc_password')
// 将这两项保存起来
save( token, enc_password )
// 先对银行卡号进行加密，然后再进行提交
bank_card = '666777888999'
enc_bank_card = encrypt( enc_password, bank_card )
http.post( "http://host.com/api/bankcard/create", { enc_bank_card, enc_password, token } ).signature( 'api/bankcard/create'+timestamp )

// 第四步，服务端收到数据后，验证API签名和timestamp时效性，最后解密数据，入库
// 验证signature和timestamp时效性
// 获取客户端传来的token enc_bankcard enc_password
token = get_post( 'token' )
enc_bankcard = get( 'enc_bankcard' )
enc_password = get( 'enc_password' )
bankcard = decrypt( enc_password, enc_bankcard )
// 根据对应关系，用token找到uid
uid = get_uid_by_token( 'token' )
// 将uid和bankcard入库
save( uid, bankcard )

openssl genrsa - out private_key . pem 2048
openssl rsa - in private_key . pem - pubout - out public_key . pem
```

## 认证、授权和凭证

* API 是无状态的，不推荐使用 Cookie
    - 使用 cookie，例如 web 项目中 ajax 的方式
    - 使用 session ID 或 hash 作为 token，但将 token 放入 header 中传递
    - 将生成的 token （可能是JWT）放入 cookie 传递，利用 HTTPonly 和 Secure 标签保护 token
* 实现认证和授权的基础是需要一种媒介（credentials）来标记访问者的身份或权利
* 认证（authentication）：指的是当前用户的身份，当用户登陆过后系统便能追踪到他的身份做出符合相应业务逻辑的操作
    - 即使用户没有登录，大多数系统也会追踪他的身份，只是当做来宾或者匿名用户来处理
    - 认证技术解决的是 “我是谁？”的问题
    - HTTP Basic Authentication
        + 客户端
            * 将用户名和密码使用冒号连接，例如 username:abc123456
            * 为了防止用户名或者密码中存在超出 ASCII 码范围的字符，推荐使用UTF-8编码
            * 将上面的字符串使用 Base 64 编码，例如 dXNlcm5hbWU6YWJjMTIzNDU2
            * 在 HTTP 请求头中加入 “Basic + 编码后的字符串”，即：Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l
            * 设置名称为 Authorization 的 header 头部
        + Base64 只能称为编码，而不是加密 (实际上无需配置密匙的客户端并没有任何可靠地加密方式，我们都依赖 TSL 协议)。这种方式的致命弱点是编码后的密码如果明文传输则容易在网络传输中泄露，在密码不会过期的情况下，密码一旦泄露，只能通过修改密码的方式
    - HMAC（AK/SK）认证：对接一些 PASS 平台和支付平台时，会要求我们预先生成一个 access key（AK） 和 secure key（SK），然后通过签名的方式完成认证请求，这种方式可以避免传输 secure key，且大多数情况下签名只允许使用一次，避免了重放攻击。
        + 利用散列的消息认证码 (Hash-based MessageAuthentication Code) 来实现的，因此有很多地方叫 HMAC 认证，实际上不是非常准确
        + HMAC 只是利用带有 key 值的哈希算法生成消息摘要，在设计 API 时有具体不同的实现
            * 客户端需要在认证服务器中预先设置 access key（AK 或叫 app ID） 和 secure key（SK）
            * 在调用 API 时，客户端需要对参数和 access key 进行自然排序后并使用 secure key 进行签名生成一个额外的参数 digest
            * 服务器根据预先设置的 secure key 进行同样的摘要计算，并要求结果完全一致
            * **注意 secure key 不能在网络中传输，以及在不受信任的位置存放（浏览器等）**
            * 每一次请求的签名变得独一无二，从而实现重放攻击，需要在签名时放入一些干扰信息
                - 质疑/应答算法（OCRA: OATH Challenge-Response Algorithm）
                    + 客户端先请求一次服务器，获得一个 401 未认证的返回，并得到一个随机字符串（nonce）
                    + 将 nonce 附加到按照上面说到的方法进行 HMAC 签名，服务器使用预先分配的 nonce 同样进行签名校验，这个 nonce 在服务器只会被使用一次，因此可以提供唯一的摘要。
                - 基于时间的一次性密码算法（TOTP：Time-based One-time Password Algorithm）：通过同步时间的方式协商到一致，在一定的时间窗口内有效（1分钟左右）
                    + 在两步验证中被大量使用：客户端服务器共享密钥然后根据时间窗口能通过 HMAC 算法计算出一个相同的验证码。TOTP HMAC-based One-time Password algorithm
* 授权（authorization）：指的是什么样的身份被允许访问某些资源，在获取到用户身份后继续检查用户的权限
    - 单一的系统授权往往是伴随认证来完成的，但是在开放 API 的多系统结构下，授权可以由不同的系统来完成，例如 OAuth
    - OAuth（开放授权）是一个开放标准，允许用户授权第三方网站访问存储在另外的服务提供者上的信息，而不需要将用户名和密码提供给第三方网站或分享他们数据的所有内容
        + OAuth 是一个授权标准，而不是认证标准。提供资源的服务器不需要知道确切的用户身份（session），只需要验证授权服务器授予的权限（token）即可
        + access token 被设计用来客户端和资源服务器之间交互,过期时间（TTL）应该尽量短，从而避免用户的 access token 被嗅探攻击
        + refresh token 是被设计用来客户端和授权服务器之间交互。帮助用户维护一个较长时间的状态，避免频繁重新授权.客户端拿着 refresh token 去获取 access token 时同时需要预先配置的 secure key，客户端和授权服务器之前始终存在安全的认证。
        + OAuth 负责解决分布式系统之间的授权问题，即使有时候客户端和资源服务器或者认证服务器存在同一台机器上。OAuth 没有解决认证的问题，但提供了良好的设计利于和现有的认证系统对接。
        + Open ID 解决的问题是分布式系统之间身份认证问题，使用Open ID token 能在多个系统之间验证用户，以及返回用户信息，可以独立使用，与 OAuth 没有关联
        + OpenID Connect 解决的是在 OAuth 这套体系下的用户认证问题，实现的基本原理是将用户的认证信息（ID token）当做资源处理。在 OAuth 框架下完成授权后，再通过 access token 获取用户的身份
        + 如果系统中需要一套独立的认证系统，并不需要多系统之间的授权可以直接采用 Open ID。如果使用了 OAuth 作为授权标准，可以再通过 OpenID Connect 来完成用户的认证。
    - 类型：grant_type：authorization_code password client_credentials
        + 授权码（authorization code）方式：向第三方应用先申请一个授权码，然后再用该码获取令
            * 流程:前端跳转到第三方应用登录链接->用户点击链接跳转到第三方应用登录并进行授权->前端跳转到所指定应用回调资源地址并伴随用于交互 AccessToken 的 Code->后端根据请求第三方应用并使用 Code 获取该用户的 AccessToken->获取 AccessToken 之后的应用即可自主的从第三方应用中获取用户的资源信息
            * 应用登记：注册一个 Application,添加回调url,得到 ClientId 和 Client Secret
            * 验证 access token
                - 在完成授权流程后，资源服务器可以使用 OAuth 服务器提供的 Introspection 接口来验证access token，OAuth服务器会返回 access token 的状态以及过期时间。在OAuth标准中验证 token 的术语是 Introspection。同时也需要注意 access token 是用户和资源服务器之间的凭证，不是资源服务器和授权服务器之间的凭证。资源服务器和授权服务器之间应该使用额外的认证（例如 Basic 认证）。
                - 使用 JWT 验证。授权服务器使用私钥签发 JWT 形式的 access token，资源服务器需要使用预先配置的公钥校验 JWT token，并得到 token 状态和一些被包含在 access token 中信息。因此在 JWT 的方案下，资源服务器和授权服务器不再需要通信，在一些场景下带来巨大的优势。同时 JWT 也有一些弱点，我会在JWT 的部分解释。
        + 隐藏式（implicit）：直接向前端颁发令牌，跳回redirect_uri，令牌的位置是 URL 锚点（fragment），而不是查询字符串（querystring）。因为 OAuth 2.0 允许跳转网址是 HTTP 协议，因此存在"中间人攻击"的风险，而浏览器跳转时，锚点不会发到服务器，就减少了泄漏令牌的风险。
            * 用于一些安全要求不高的场景，并且令牌的有效期必须非常短，通常就是会话期间（session）有效，浏览器关掉，令牌就失效了
        + 密码式（password）：使用用户名和密码，申请令牌
            * 验证身份通过后，直接给出令牌。注意，这时不需要跳转，而是把令牌放在 JSON 数据里面，作为 HTTP 回应，客户端因此拿到令牌
        + 凭证式（client credentials）：适用于没有前端的命令行应用，即在命令行下请求令牌
            * 给出的令牌，是针对第三方应用的，而不是针对用户的，即有可能多个用户共享同一个令牌
    - JWT （JSON Web Token）:一种自包含令牌，令牌签发后无需从服务器存储中检查是否合法，通过解析令牌就能获取令牌的过期、有效等信息
        + 令牌为一段点分3段式结构
            * header json 的 base64 编码为令牌第一部分
            * payload json 的 base64 编码为令牌第二部分
            * 拼装第一、第二部分编码后的 json 以及 secret 进行签名的令牌的第三部分
        + 只需要签名的 secret key 就能校验 JWT 令牌，如果在消息体中加入用户 ID、过期信息就可以实现验证令牌是否有效、过期了，无需从数据库/缓存中读取信息
        + 第一、二部分只是 base64 编码，肉眼不可读，不应当存放敏感信息
        + 自包含特性，导致了无法被撤回
* 策略
    - 基于访问控制列表（ACL）
    - 基于用户角色的访问控制（RBAC）

```
{
  ClientId: 'xxxxxxxxx',
  Client Secret: 'xxxxxxxxx',
  redirect: 'xxxxxxxxxxx'
}

前端             后端                       后端          后端
-—---------       --------------     -------------     ----------
| Client ID | -->| code + state |-->|access_token |-->| user info |
-----------       --------------     -------------     ----------

# 前端获取 code & state
GET https://github.com/login/oauth/authorize?client_id=your_client_id&redirect_uri=your_callback_url&scope=user&state=random_string
| name | type | description |
| ------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| client_id | string | 第一步中注册得到的ClientID |
| redirect_uri | string | 第一步中设置的回调地址 |
| loin | string | 推荐登录的 Github 账户，一般不填 |
| scope | string | 这个参数指定了最后能获取到的信息，取值范围有 user 和 repo 等等,默认同时取 user 和 repo 的信息，详细取值范围见Github 文档 |
| state | string | 你设定的一个随机值，用来防止 cross-sit 攻击 |
| allow_signup | string | 这个参数指定是否允许用户在认证的时候注册 Github 账号，默认是 true |
## 要求用户登录，然后询问是否同意给予授权
## 跳转到redirect_uri指定的跳转网址，并且带上授权码
http://localhost:8080/oauth/callback?code=859310e7cecc9196f4af

# 后端获取 access_token
POST https://github.com/login/oauth/access_token

| Name | Type | Description |
| ------------- | ------ | ----------------------------- |
| client_id | string | 第一步中获取到的 ClientID |
| cleint_secret | string | 第一步中获取到的 ClientSecret |
| code | string | 第二步中前端获取到的 code |
| redirect_uri | string | 第一步中设置的回调地址 |
| state | string | 第一步中设置的随机值 |
## 根据头部的 Accept 的值返回
application/x-www-form-urlencoded
access_token=e72e16c7e42f292c6912e7710c838347ae178b4a&token_type=bearer

application/json
{
  "access_token": "e72e16c7e42f292c6912e7710c838347ae178b4a",
  "scope": "repo,gist",
  "token_type": "bearer"
}

## access_token 获取用户信息
curl -H "Authorization: Bearer ACCESS_TOKEN" \
https://api.github.com/user

## 更新token
/oauth/token?
  grant_type=refresh_token&
  client_id=CLIENT_ID&
  client_secret=CLIENT_SECRET&
  refresh_token=REFRESH_TOKEN
```

## [JSON API](https://jsonapi.org/format/)

* 最早来源于Ember Data（Ember是一个JavaScript前端框架，在框架中定义了一个通用的数据格式，后来被广泛认可）
* MIME 类型:JSON API数据格式已经被IANA机构接受了注册，因此必须使用application/vnd.api+json类型。客户端请求头中Content-Type应该为application/vnd.api+json，并且在Accept中也必须包含application/vnd.api+json。如果指定错误服务器应该返回415或406状态码。
* 文档结构:在顶级节点使用data、errors、meta，来描述数据、错误信息、元信息，注意data和errors应该互斥，不能再一个文档中同时存在
    - 典型的data的对象格式:有效信息一般都放在attributes中
        + id显而易见为唯一标识，可以为数字也可以为hash字符串，取决于后端实现
        + type 描述数据的类型，可以对应为数据模型的类名
        + attributes 代表资源的具体数据
        + relationships、links为可选属性，用来放置关联数据和资源地址等数据
    - errors属性:作为列表存在，因为针对每个资源可能出现多个错误信息,HTTP状态码会使用一个通用的401，然后把具体的验证信息在errors给出来
        + code
        + 在title字段中给出错误信息
        + 如果在本地或者开发环境想打出更多的调试堆栈信息，可以增加一个detail字段让调试更加方便。需要注意的一点是，应该在生产环境屏蔽部分敏感信息，detail字段最好在生产环境不可见。
* 返回码
    - 200 OK 200是一个最常用的状态码用来表示请求成功，例如GET请求到某一个资源，或者更新、删除某资源。 需要注意的是使用POST创建资源应该返回201表示数据被创建。
    - 201 Created 如果客户端发起一个POST请求，在RESTful部分我们提到，POST为创建资源，如果服务器处理成功应该返回一个创建成功的标志，在HTTP协议中，201为新建成功的状态。文档规定，服务器必须在data中返回id和type。 下面是一个HTTP的返回例子：
    - 401 Unauthorized 如果服务器在检查用户输入的时候，需要传入的参数不能满足条件，服务器可以给出401错误，标记客户端错误，需要客户端自查。
    - 415 Unsupported Media Type 当服务器媒体类型Content-Type和Accept指定错误的时候，应该返回415。
    - 403 Forbidden 当客户端访问未授权的资源时，服务器应该返回403要求用户授权信息。
    - 404 Not Found 这个太常见了，当指定资源找不到时服务器应当返回404。
    - 500 Internal Server Error 当服务器发生任何内部错误时，应当返回500，并给出errors字段，必要的时候需要返回错误的code，便于查错。一般来说，500错误是为了区分4XX错误，包括任何服务器内部技术或者业务异常都应该返回500。
* HATEOAS(Hypermedia As The Engine Of Application State): 在没有文档的情况下找到这些资源的地址呢，一种可行的办法就是在API的返回体里面加入导航信息，也就是links
* erlang社区的webmachine或者clojure下的liberator

```json
{
  "data": [{
    "type": "articles",
    "id": "1",
    "attributes": {
      "title": "JSON:API paints my bikeshed!"
    },
    "links": {
      "self": "http://example.com/articles/1"
    },
    "relationships": {
      "author": {
        "links": {
          "self": "http://example.com/articles/1/relationships/author",
          "related": "http://example.com/articles/1/author"
        },
        "data": { "type": "people", "id": "9" }
      },
      "comments": {
        "links": {
          "self": "http://example.com/articles/1/relationships/comments",
          "related": "http://example.com/articles/1/comments"
        },
        "data": [
          { "type": "comments", "id": "5" },
          { "type": "comments", "id": "12" }
        ]
      }
    }
  }],
  "included": [{
    "type": "people",
    "id": "9",
    "attributes": {
      "first-name": "Dan",
      "last-name": "Gebhardt",
      "twitter": "dgeb"
    },
    "links": {
      "self": "http://example.com/people/9"
    }
  }, {
    "type": "comments",
    "id": "5",
    "attributes": {
      "body": "First!"
    },
    "relationships": {
      "author": {
        "data": { "type": "people", "id": "2" }
      }
    },
    "links": {
      "self": "http://example.com/comments/5"
    }
  }, {
    "type": "comments",
    "id": "12",
    "attributes": {
      "body": "I like XML better"
    },
    "relationships": {
      "author": {
        "data": { "type": "people", "id": "9" }
      }
    },
    "links": {
      "self": "http://example.com/comments/12"
    }
  }]
}
```

编译时」和「运行时」分开

## 架构

* 把 API 执行路径上的各种处理都抽象出来，放到公共路径（或者叫中间件，middleware）之中，为 API 的撰写者扫清各种障碍，同时能够促使 API 更加标准化。
* pipeline 下的组件
  - throttling：API 应该有最基本的访问速度的控制，比如，对同一个用户，发布 tweet 的速度不可能超过一个阈值，比如每秒钟 1 条（实际的平均速度应该远低于这个）。超过这个速度，就是滥用（abuse），需要制止并返回 429 Too many requests。throttling 可以使用 leaky bucket 实现（restify 直接提供）。
  - parser / validation：接下来要解析 HTTP request 包含的 headers，body 和 URL 里的 querystring，并对解析出来的结果进行 validation。这个过程可以屏蔽很多服务的滥用，并提前终止服务的执行。比如你的 API 要求调用者必须提供 X-Client-Id，没有提供的，或者提供的格式不符合要求的，统统拒绝。这个步骤非常重要，如同我们的皮肤，将肮脏的世界和我们的器官隔离开来。
  - ACL：除了基本的 throttling 和 validation 外，控制资源能否被访问的另一个途径是 ACL。管理员应该能够配置一些规则，这些规则能够进一步将不合法 / 不合规的访问过滤掉。比如说：路径为 "/topic/19805970" 的知乎话题，北京时间晚上10点到次日早上7点的时间端，允许在中国大陆显示。这样的规则可以是一个复杂的表达式，其触发条件（url）可以被放置在一个 bloom filter 里，满足 filter 的 url 再进一步在 hash map 里找到其对应的规则表达式，求解并返回是否允许显示。至于一个诸如country = "CN" && time >= 00:00CST && time < 07:00CST（这是一个管理员输入的表达式）这样的表达式如何处理，请移步 如何愉快地写个小parser。
  - normalization：顾名思义，这个组件的作用是把请求的内容预处理，使其统一。normalization 可以被进一步分为多个串行执行的 strategy，比如：
    + paginator：把 request 里和 page / sort 相关的信息组合起来，生成一个 paginator。
    + client adapter：把 API client 身份相关的信息（device id，platform，user id，src ip，...）组合成一个 adapter。
    + input adapter：输入数据的适配。这是为处女座准备的。很多时候，输入数据的格式和语言处理数据的格式不一样，这对处女座程序员是不可接受的。比如说 API 的输入一般是 snake case（show_me_the_money），而在某些语言里面（如: javascript），约定俗成的命名规则是 showMeTheMoney，所以把输入的名称转换有利于对代码有洁癖的程序员。
  - authentication：用户身份验证。主要是处理 "Authorization" 头。对于不需要验证的 API，可以跳过这一步。做 API，身份验证一定不要使用 cookie/session based authentication，而应该使用 token。现有的 token base authentication 有 oauth, jwt 等。如果使用 jwt，要注意 jwt 是 stateless 的 token，一般不需要服务器再使用数据库对 token 里的内容校验，所以使用 jwt 一定要用 https 保护 token，并且要设置合适的超时时间让 token 自动过期。
  - authorization：用户有了身份之后，进一步需要知道用户有什么样的权限访问什么样的资源。比如：uid 是 9527 的用户对 "POST /topic/"（创建一个新的话题），"PUT /topic/:id"（修改已有的话题）有访问权限，当他发起 "DELETE /topic/1234" 时，在 authorization 这一层直接被拒绝。authorization 是另一种 ACL（role based ACL），处理方式也类似。
  - conditional request：在访问的入口处，如果访问是 PUT/PATCH 这样修改已有资源的操作，好的 API 实现会要求客户端通过 conditional request（if-match / if-modified）做 concurrent control，目的是保证客户端要更新数据时，它使用的是服务器的该数据的最新版本，而非某个历史版本，否则返回 412 precondition failed（更多详情，请参考我之前的文章 撰写合格的REST API）。
  - preprocessing hook：
  - processing：API 本身的处理。这个一般是 API 作者提供的处理函数。
  - postprocessing：
  - conditional request：在访问的出口处，如果访问的是 GET 这样的操作，好的 API 实现会支持客户端的 if-none-match/if-not-modified 请求。当条件匹配，返回 200 OK 和结果，否则，返回 304 Not Modified。304 Not Modified 对客户端来说如同瑰宝，除了节省网络带宽之外，客户端不必刷新数据。如果你的 app 里面某个类别下有五十篇文章，下拉刷新的结果是 304 Not Modified，客户端不必重绘这 50 篇文章。当然，有不少 API 的实现是通过返回的数据中的一个自定义的状态码来决定，这好比「脱裤子放屁」—— 显得累赘了。
  - response normalization：和 request 阶段的 normalization 类似，在输出阶段，需要将结果转换成合适的格式返回给用户。response normalization 也有很多 strategy，比如：
    + output adapter：如果说 input adapter 是为有洁癖的程序员准备的，可有可无，那么 output adapter 则并非如此。它能保持输出格式的一致和统一。比如你的数据库里的字段是 camel case，你的程序也都是用 camel case，然而 API 的输出需要统一为 snake case，那么，在 output adapter 这个阶段统一处理会好过每个 API 自己处理。
    + aliasing：很多时候获得的数据的名称和定义好的 API 的接口的名称并不匹配，如果在每个 API 里面单独处理非常啰嗦。这种处理可以被抽取出来放在 normalization 的阶段完成。API 的撰写者只需要定义名称 A 需要被 alias 成 B 就好，剩下的由框架帮你完成。
    + partial response：partial response 是 google API 的一个非常有用的特性（见：https://developers.google.com/+/web/api/rest/#partial-response ），他能让你不改变 API 实现的情况下，由客户端来决定服务器返回什么样的结果（当前结果的一个子集），这非常有利于节省网络带宽。
  - serialization：如果 API 支持 content negotiation，那么服务器在有可能的情况下，优先返回客户端建议的输出类型。同一个 API，android 可以让它返回 application/msgpack；web 可以让它返回 application/json，而 xbox 可以获得 application/xml 的返回，各取所需。
  - postserialization：这也是个 hook，在数据最终被发送给客户端前，API 调用者可以最后一次 inject 自己想要的逻辑。一般而言，一些 API 系统内部的统计数据可以在此收集（所有的出错处理路径和正常路径都在这里交汇）。

## 子系统

* 配置管理
  - 一个公共的地方来放置预置的属性。toml
  - 配置文件可以重载（override）：系统提供一个公共的配置文件：default，然后各种运行时相关的配置文件继承并局部重载这个配置。在系统启动的时候，二者合并。
  - 运行的时候改写配置：像管理缓存一样去管理和配置相关的数据，将其封装在一个容器里：当配置被修改时，调用这个容器的 invalidate 方法 —— 这样，下次访问任意一个配置项时，会重新读入配置，并缓存起来
* CLI：不是给用户用的，是给程序员用的
  - 难点
    + CLI 的发现和自注册。你的 framework 的用户只要遵循某种 convention 撰写 CLI，这些 CLI 就会被自动集成到系统里。
    + CLI 的撰写者能够轻松地获取到系统的信息，也就是说，系统有自省（introspection）的能力。
* 测试框架
  -  functional testing 是可以全局考虑
  -  ava 描述测试的 fixture

## 契约

* 一开始随意了，简单了，会给之后的维护和更新带来无穷无尽的痛苦
* 可以很方便地描述 API 的输入输出，并生成交互式的 API 文档（读 API 文档的时候，可以在线运行 API） 设计工具有
  - swagger：缺点是太繁杂，撰写起来很麻烦
    + 通过代码反向生成 swagger 文档
    + 先撰写代码把 API 的输入输出定义清楚，然后通过这个定义来生成 swagger 文档，在 swagger-ui 里面调试和验证；当借口设计符合期望后，再完成具体的实现
  - API blueprint：更偏向 API 的文档化，所以它选择的描述语言是 markdown。validation 相关的内容用 markdown 描述不是很舒服，看别人写的文档很容易明白，自己写起来就会错漏百出。API blueprint 的工具链也是个薄弱环节，很多工具都没有或者不成熟
  - RAML

## 文档

* 格式
    - 请求地址
    - 请求类型
    - 参数说明
    - 返回结果说明
* 基于注释的 API 文档：通过代码中注释生成 API 文档的轻量级方案
    - 好处是简单易用，基本与编程语言无关
    - 因为基于注释，非常适合动态语言的文档输出，例如 Nodejs、PHP、Python。由于NPM包容易安装和使用，这里推荐 nodejs 平台下的 apidocjs
* 基于反射的 API 文档：使用 swagger 这类通过反射来解析代码，只需要定义好 Model，可以实现自动输出 API 文档。这种方案适合强类型语言例如 Java、.Net，尤其是生成一份稳定、能在团队外使用的 API 文档
    - swagger 实际上是一整套关于 API 文档、代码生成、测试、文档共享的工具包，包括 :
        + Swagger Editor 使用 swagger editor 编写文档定义 yml 文件，并生成 swagger 的 json 文件,提供线上版本，也可以本地使用
        + Swagger UI 解析 swagger 的 json 并生成 html 静态文档
        + Swagger Codegen 可以通过 json 文档生成 Java 等语言里面的模板文件（模型文件）
        + Swagger Inspector API 自动化测试
        + Swagger Hub 共享 swagger 文档
* 使用契约进行前后端协作：在团队内部，前后端协作本质上需要的不是一份 API 文档，而是一个可以供前后端共同遵守的契约
    - 前后端可以一起制定一份契约，使用这份契约共同开发，前端使用这份契约 mock API，后端则可以通过它简单的验证API是否正确输出
    - **契约测试**:消费者驱动的契约  Spring cloud contract
    - 后端根据需求，生成 API 定义文件，就可以进一步完成生成 HTML 静态文档、模拟 API 数据等操作
    - 前端对接接口,通过 swagger 的 node 版本 swagger-node 自带的 mock 模式启动一个 Mock server，然后根据约定模拟自己想要的数据, mockjs + rap 或者 easy-mock
    - 管理契约文件:单独增加了一个管理契约文件的 git仓库，并使用 git 的submodule 来引用到各个涉及到了的代码仓库中
        + 单独放置还有一个额外的好处:构建契约测试时，可以方便的发送到一台中间服务器。一旦 API 契约发生变化，可以触发 API提供的契约验证测试
* RAML RestFul API 统一建模语言 （RESTful API Modeling Language）,构建出 API 协作的工具链，设计、构建、测试、文档、共享。

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

### apidoc

* 每次导出接口文档都必须要让apidoc读取到apidoc.json文件(如果未添加配置文件，导出报错)，可以在项目的根目录下添加apidoc.json文件
* 项目中使用了package.json文件(例如:node.js工程)，可以将apidoc.json文件中的所有配置信息放到package.json文件中的apidoc参数中
* 参数
    - name
    - version
    - description
    - title
    - url
    - header.title
    - header.filename   页眉文件名(markdown)
    - footer.title    页脚导航标题
    - footer.filename     页脚文件名(markdown)
    - order   接口名称或接口组名称的排序列表,如果未定义，那么所有名称会自动排序 "Error", "Define", "PostTitleAndError", "PostError"

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

## 语法
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

## 前后端实践

* 问题
    - 接口频繁变动：需要提高需求的理解能力和接口设计能力
    - 接口文档在定接口时起到一定作用，写完接口就没有用了
    - 接口文档落后：**没有给我们带来价值**
    - 测试： “提测” 之前只能喝茶，“提测” 之后又忙的要命
* 解决：让接口文档发挥价值，提高变动接口的成本，测试尽早介入。加大契约修改成本
    - 接口文档发挥出价值，就要赋予契约的意义。
    - 契约应该由前端同学来驱动，前后端共同协商。由于前端同学与 UX 接触比较紧密，更了解页面所需的数据以及整体的 User Journey，前端同学驱动会更加合理。
    - 契约敲定之后，要生成 Mock Server，前后端同学就要依照契约各自开发。Mock Server 可暂时替代后台服务，帮组前端开发，同时，测试同学也可以依照契约文档来编写测试脚本，使用 Mock Server 进行脚本验证。
    - 后端接口发生变化除了口头通知以外必须修改契约：修改契约的成本变高

## [raml-mocker](https://github.com/xbl/raml-mocker)

基于 Raml 使用 Nodejs 开发的 Mock Server 工具，使用 Raml 描述接口中设置 response 的 example 指令即可，raml-mocker 会解析 Raml 文件，并启动一个 Mock Server，将  example 的内容返回给浏览器。

* 配置 `.raml-config.json`
    - controller: controller 目录路径
    - raml: raml 文件目录
    - main: raml 目录下的入口文件
    - port:  mock server 服务端口号
    - plugins: 插件

```sh
git clone https://github.com/xbl/raml-mocker-starter.git raml-api
cd raml-api
git remote rm origin
yarn install
yarn|npm start

curl -i http://localhost:3000/api/v1/users/1/books/
# or
curl -i http://localhost:3000/api/v1/users/1/books/1

# 生成 API 可视化文档
yarn|npm run build

yarn test
```

## 恶意调用

## 加密

* https:面对charles等抓包工具时，其实并没有什么卵用，只要配置一下根证书瞬间可以看到一切明文

```
// 加密密码
password = '123456'
// 需要加密的内容
message = 'Hello World!'
// 利用加密密码对内容进行加密
enc_message = encrypt( password, message )
// 解密
dec_message = decrypt ( password, enc_message )
print dec_message   // Hello World!
```

## 接口

* [public-apis/public-apis](https://github.com/public-apis/public-apis):A collective list of free APIs for use in software and web development. https://ultimatecourses.com
* [雅虎天气](https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20%3D%202151330&format=json)
* [价格](http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice)
* [Vespa314/bilibili-api](https://github.com/Vespa314/bilibili-api):B站API收集整理及开发
* [jokermonn/-Api](https://github.com/jokermonn/-Api):📖「一个」、「Time 时光」、「开眼」、「一席」、「梨视频」、「微软必应词典」、「金山词典」、「豆瓣电影」、「中央天气」、「魅族天气」、「每日一文」、「12306」、「途牛」、「快递100」、「快递」应用 Api
* [toddmotto/public-apis](https://github.com/toddmotto/public-apis):A collective list of public JSON APIs for use in web development. https://toddmotto.com
* [pwxcoo/chinese-xinhua](https://github.com/pwxcoo/chinese-xinhua):📙 中华新华字典数据库。包括歇后语，成语，词语，汉字。提供新华字典API。
* [Binaryify/NeteaseCloudMusicApi](https://github.com/Binaryify/NeteaseCloudMusicApi):网易云音乐 Node.js API service https://binaryify.github.io/NeteaseCloudMusicApi/#/
* 豆瓣
    - [douban](https://developers.douban.com/wiki/?title=guide)
    - [获取正在热映的电影](https://api.douban.com/v2/movie/in_theaters?city=广州&start=0&count=10)
    - [获取电影Top250](https://api.douban.com/v2/movie/top250?start=0&count=10)
    - [电影搜索](https://api.douban.com/v2/movie/search?q=神秘巨星&start=0&count=10)
    - [电影详情](https://api.douban.com/v2/movie/subject/26942674)

## 工具

* [Branca](https://branca.io/):Authenticated and encrypted API tokens using modern crypto.
* [restify](link)
  - validator  joi
  - swagger
  - waterline
  - log:bunyan
  - ava / rewire / supertest / nyc
* Gateway
    - [TykTechnologies/tyk](https://github.com/TykTechnologies/tyk)：Tyk Open Source API Gateway written in Go
* [GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer):Headless Chrome Node API https://try-puppeteer.appspot.com/
* [thx/RAP](https://github.com/thx/RAP):Web接口管理工具，开源免费，接口自动化，MOCK数据自动生成，自动化测试，企业级管理。阿里妈妈MUX团队出品！阿里巴巴都在用！1000+公司的选择！RAP2已发布请移步至https://github.com/thx/rap2-delos http://rapapi.org
* [thx/rap2-delos](https://github.com/thx/rap2-delos):阿里妈妈前端团队出品的开源接口管理工具RAP第二代 http://rap2.taobao.org
* [encode/apistar](https://github.com/encode/apistar):A smart Web API framework, for Python 3. 🌟 https://docs.apistar.com
* [ruby-grape/grape](https://github.com/ruby-grape/grape):An opinionated framework for creating REST-like APIs in Ruby. http://www.ruby-grape.org
* [encode/django-rest-framework](https://github.com/encode/django-rest-framework):Web APIs for Django. ⚡️ https://www.django-rest-framework.org
* [paularmstrong/normalizr](https://github.com/paularmstrong/normalizr):Normalizes nested JSON according to a schema
* [dingo/api](https://github.com/dingo/api):A RESTful API package for the Laravel and Lumen frameworks.
* [parse-community/parse-server](https://github.com/parse-community/parse-server):Parse-compatible API server module for Node/Express http://parseplatform.org
* [interagent/http-api-design](https://github.com/interagent/http-api-design):HTTP API design guide extracted from work on the Heroku Platform API https://www.gitbook.com/read/book/gee…
* [typicode/json-server](https://github.com/typicode/json-server):Get a full fake REST API with zero coding in less than 30 seconds (seriously)
* [tobscure/json-api](https://github.com/tobscure/json-api):JSON-API (http://jsonapi.org) responses in PHP.
* [hashicorp/vault](https://github.com/hashicorp/vault)：A tool for secrets management, encryption as a service, and privileged access management https://www.vaultproject.io/
* [nsf/termbox-go](https://github.com/nsf/termbox-go):Pure Go termbox implementation http://code.google.com/p/termbox
* [apiaryio/dredd](https://github.com/apiaryio/dredd):Language-agnostic HTTP API Testing Tool https://dredd.rtfd.io
* [hellofresh/janus](https://github.com/hellofresh/janus):An API Gateway written in Go https://hellofresh.gitbooks.io/janus
* [SocketLog](https://github.com/luofei614/SocketLog)
* 加密
    - [google/tink](https://github.com/google/tink):Tink is a multi-language, cross-platform library that provides cryptographic APIs that are secure, easy to use correctly, and hard(er) to misuse.
    - [JSEncrypt](https://github.com/travist/jsencrypt):用于执行OpenSSL RSA加密、解密和密钥生成的Javascript库。WEB 的登录功能时一般是通过 Form 提交或 Ajax 方式提交到服务器进行验证的。为了防止抓包，登录密码肯定要先进行一次加密（RSA），再提交到服务器进行验证
* 测试
  - Poster 火狐浏览器的一个插件
    - postman
    - [liyasthomas/postwoman](https://github.com/liyasthomas/postwoman):https://github.com/liyasthomas/postwoman
    - [apiaryio/dredd](https://github.com/apiaryio/dredd):Language-agnostic HTTP API Testing Tool https://dredd.org
    - [airbnb/hypernova](https://github.com/airbnb/hypernova):A service for server-side rendering your JavaScript views
    - RESTClient是用java Swing编写的基于http协议的接口测试工具
    - Fiddler是一个http协议调试代理工具，它能够记录并检查所有你的电脑和互联网之间的http通讯，设置断点，查看所有的“进出”Fiddler的数据（指cookie,html,js,css等文件，这些都可以胡乱修改的意思）,测试的数据都可以保存,但测试记录不方便查询
    - SoapUI是一个免费、开源、跨平台的功能测试解决方案。一个易于使用的图形界面，和企业级功能，让你轻松和soapUI迅速创建和执行自动化的功能，回归测试和负载测试
    - Apache JMeter是Apache组织开发的基于Java的开源的测试工具， JMeter 可以用于对服务器、网络或对象模拟巨大的负载，来自不同压力类别下测试它们的强度和分析整体性能,对应用程序做功能/回归测试/接口测试，同时Jmeter+Ant+Jenkins也可以搭建接口和性能的持续集成测试平台
    - WireMock是一个非常轻量级的支持HTTP mock的服务,可以用于单元测试或模拟测试环境服务端，它支持HTTP响应头，请求验证，代理/拦截，记录/回放存根和故障注入
    - 冒烟测试用poster，集成测试用Jmeter
* 文档
    - [swagger-api/swagger-ui](https://github.com/swagger-api/swagger-ui):Swagger UI is a collection of HTML, Javascript, and CSS assets that dynamically generate beautiful documentation from a Swagger-compliant API. http://swagger.io
    - [YMFE/yapi](https://github.com/YMFE/yapi):YApi 是一个可本地部署的、打通前后端及QA的、可视化的接口管理平台 http://yapi.demo.qunar.com/
    * [gongwalker/ApiManager](https://github.com/gongwalker/ApiManager):接口文档管理工具
    - [jsdoc3/jsdoc](https://github.com/jsdoc3/jsdoc):An API documentation generator for JavaScript. http://usejsdoc.org
    - [swagger](https://app.swaggerhub.com/home)Swagger UI is a collection of HTML, Javascript, and CSS assets that dynamically generate beautiful documentation from a Swagger-compliant API. http://swagger.io
    - [freeCodeCamp/devdocs](https://github.com/freeCodeCamp/devdocs):API Documentation Browser https://devdocs.io
    - [lord/slate](https://github.com/lord/slate):Beautiful static documentation for your API https://spectrum.chat/slate
    - YUI doc
    - eolinker
    - Apizza
    - Yapi
    - [RAP2](http://rap2.taobao.org)
    - DOClever
    - [insomnia](https://insomnia.rest/):Design and debug APIs like a human, not a robot.
    - [star7th / showdoc](https://github.com/star7th/showdoc):ShowDoc is a tool greatly applicable for an IT team to share documents online一个非常适合IT团队的在线API文档、技术文档工具 https://www.showdoc.cc
* 抓包
    - Charles
    - fiddler
    - [Wireshark](https://www.wireshark.org)
    - [avwo/whistle](https://github.com/avwo/whistle):HTTP, HTTP2, HTTPS, Websocket debugging proxy https://wproxy.org/
* API 文档/契约生成工具
    - apidoc
    - swagger
    - blue sprint
    - RAML
* mock
    - wiremock
    - json-server
    - node-mock-server
    - node-mocks-http
    - [nuysoft/Mock](https://github.com/nuysoft/Mock):A simulation data generator http://mockjs.com
* HTTP 请求拦截器
    - axios-mock-adapter
    - jquery-mockjax
* 契约/API 测试工具
    - Spring Cloud Contract
    - Pact
    - Rest-Assured
* HoServer
* [APIJSON / APIJSON](https://github.com/APIJSON/APIJSON):🏆码云最有价值开源项目 🚀后端接口和文档自动化，前端(客户端) 定制返回 JSON 的数据和结构！🏆Gitee Most Valuable Project 🚀A JSON Transmission Protocol and an ORM Library for automatically providing APIs and Docs. http://apijson.org

## 参考

* [OAI/OpenAPI-Specification](https://github.com/OAI/OpenAPI-Specification):The OpenAPI Specification Repository https://openapis.org
* [jsonapi](https://jsonapi.org/format/)
* [shieldfy/API-Security-Checklist](https://github.com/shieldfy/API-Security-Checklist):Checklist of the most important security countermeasures when designing, testing, and releasing your API
* [microsoft/api-guidelines](https://github.com/microsoft/api-guidelines):Microsoft REST API Guidelines
* [Best Practices for Designing a Pragmatic RESTful API](https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)
