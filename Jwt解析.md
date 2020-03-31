### Jwt解析

#### 一: 什么是jwt

json web token ，由三部分组成:header(头部)，payload(载荷，我们要存储的信息)  signature（签证）

通常组成是header.payload.signature 这是三部分加密以后的

1.  header 声明类型 以及加密算法
2. payload 载荷。标准声明 公有声明 私有声明
3. signature: HMACSHA256( base64UrlEncode(header) + '.' + base64UrlEncode(payload)  , 'secret')，其中secret是在服务端生成的。最外层的256是在头部声明的加密类型。
4. 所以最终组成就是 header (base64后的).payload (base64后的).signature这三部分，中间用.连接。

#### 二: cookie和session方式和jwt方式

cookie和session方式有以下缺点:

1.  使用cookie和session方式更耗费内存，随着用户的增加服务端开销明显增加，而基于token方式直接是基于一个规则解析，不需要另外存在，直接在登录时保存在前端即可
2. 当web服务扩展时，分布式情况下，需要做session共享(方式:1、redis以及memereche 2、session在tomcat之间复制，即一个节点，存储所有的session, )，浪费资源。
3. 容易产生csrf攻击，用户浏览登录A网站， A网站cookie存储了cookie用户身份信息，然后此时浏览B网站，假设cookie被B网站劫持了，就可以仿冒用户A去进行某些相关操作。

####  三：spring secruity  集成jwt

