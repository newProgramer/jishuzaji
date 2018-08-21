# 简介

JWT是一种用于双方之间传递安全信息的简洁的、URL安全的表述性声明规范。JWT作为一个开放的标准（[RFC 7519](https://link.jianshu.com?t=https://tools.ietf.org/html/rfc7519)），定义了一种简洁的，自包含的方法用于通信双方之间以Json对象的形式安全的传递信息。因为数字签名的存在，这些信息是可信的，JWT可以使用HMAC算法或者是RSA的公私秘钥对进行签名。

**简洁\(Compact\)**

可以通过URL，POST参数或者在HTTP header发送，因为数据量小，传输速度也很快

**自包含\(Self-contained\)**

负载中包含了所有用户所需要的信息，避免了多次查询数据库

# 结构

JWT包含了使用.分隔的三部分： Header\(头部\).Payload\(负载\).Signature\(签名\)

### Header

Header中通常包含两部分:token类型和采用的加密算法

### Payload

Token的第二部分是负载，它包含了claim， Claim是一些实体（通常指的用户）的状态和额外的元数据，有三种类型的claim：

_reserved_, _public_ 和 _private_.

**Reserved claims**

这些claim是JWT预先定义的，在JWT中并不会强制使用它们，而是推荐使用，常用的有 iss（签发者）,exp（过期时间戳）, sub（面向的用户）, aud（接收方）, iat（签发时间）。

**Public claims**

根据需要定义自己的字段，注意应该避免冲突

**Private claims**

这些是自定义的字段，可以用来在双方之间交换信息 负载使用的例子：{ "sub": "1234567890", "name": "John Doe", "admin": true} 上述的负载需要经过`Base64Url`编码后作为JWT结构的第二部分。

# Signature

创建签名需要使用编码后的header和payload以及一个秘钥，使用header中指定签名算法进行签名。

因为用户的状态在服务端的内存中是不存储的，所以这是一种`无状态`的认证机制。

# JWT管理Session有以下缺点

* **更多的空间占用**:将原存在服务端session中的各类信息都保存在jwt中,可能造成jwt占用的空间变大,需要考虑cookie的空间限制等因素,如果存放在Local Storage,则可能收到XSS攻击.
* **更不安全**:这里特制将JWT存放在Local Storage中, 然后使用Javascript取出后作为HTTP header发送给服务端的方案。在Local Storage中保存敏感信息并不安全，容易受到跨站脚本攻击，跨站脚本（Cross site script，简称xss）是一种“HTML注入”，由于攻击的脚本多数时候是跨域的，所以称之为“跨域脚本”，这些脚本代码可以盗取cookie或是Local Storage中的数据。
* **无法作废已颁布的令牌。**所有的认证信息都在JWT中，由于在服务端没有状态，即使你知道了某个JWT被盗取了，你也没有办法将其作废。在JWT过期之前（你绝对应该设置过期时间），你无能为力。
* **不易应对数据过期。**与上一条类似，JWT有点类似缓存，由于无法作废已颁布的令牌，在其过期前，你只能忍受“过期”的数据。

# 应用场景

验证邮件

