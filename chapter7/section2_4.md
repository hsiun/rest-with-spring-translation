# 基于Token鉴权

在最后一种模式我们简略讨论下基于Token的鉴权。在这种方式不是HTTP标准的一部分，但是它是很常用的一种鉴权方式。这种方式依靠一个服务器发布的加密Token，随后在客户端再通过这个Token发送每次请求。Token可以使用现代，稳健的加密算法加密。Spring通过使用`org.springframework.security.core.token.TokenService`和`org.springframework.security.core.token.Toke`这种模式提供很好的支持。

举个例子，服务开发者参考下`org.springframework.security.core.token.KeyBasedPersistenceTokenService`来简单使用这种鉴权方式。