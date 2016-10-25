# HTTP公钥

HTTP公钥钉（HPKP）是一种先信任在使用的安全模式，这种技术可以阻止假冒的SSL证书。RESTful Web服务支持的HPKP响应将包含在头部，`Public-Key-Pins`，包含它们证书的对象公钥信息（SPKI）的哈希。当客户端应用程序第一次接收到这个值时，他应该缓存它。并且验证使用前面发布的头部值验证所有后来的响应。如果值不匹配，客户端应用可以随时阻止和不正当服务器的进一步交流。

然而Spring框架对HPKP不提供额外支持，它可以直接实现这个安全特性，通过使用请求过滤。

### 注意

你可以在<https://en.wikipedia.org/wiki/HTTP_Public_Key_Pinning>阅读关于HTTP公钥签名的更多信息。
