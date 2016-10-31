# HTTP摘要鉴权

类似于HTTP基础鉴权模式，HTTP摘要鉴权模式也使用用户名和密码来验证用户。然而，不想之前的模式，凭证不是使用简单的编码格式通过网络发送的。而是使用MD5加密的用户名和密码，且只有这个信息的一部分被发送了。当服务器接收到这个请求，它使用相同的算法生成一个其他的MD5哈希值，并比较这两个值。如果匹配，用户输入了正确的密码。如果不，则鉴权失败，并返回一个合适的状态码。

在Spring中设置摘要验证，`org.springframework.security.web.authentication.www.DigestAuthenticationFilt`过滤器必须配置好。这个过滤器将发布如下所示的验证报文头：

```
WWW-Authenticate: Digest realm="My Realm", qop="auth", nonce="MTQzNDUzMjIyNTE3MDplZjRmYzFmYzZkNDZkNDE4NzE2ZmRkNzAzMmM2YmM0ZQ==" 
```

这个过滤器将会处理所有请求中`Authorization`报文头。例如：

```
Authorization: Digest username="rest", realm="My Realm", nonce="MTQzNDUzMjM0OTk2MzoyNjQwOTA0MDI0MTEzN2E2ZjIzOGMxZDU0ZTlkY2MxYQ==", uri="/bookings/3", response="1bc4974dd8ca156568149f3944cf42c8", qop=auth, nc=00000001, cnonce="6ae950660ea900bf"
```

访问安全资源，服务器将会发送带有`WWW-Authenticate`报文头的401响应。浏览将会通过体相用输入验证并使用` Authorization`报文头包含MD5加密的用户凭证重新发布请求。

为了支持摘要验证，让我们修改我们的`SecurityConfig`类：

```java
@EnableWebSecurity public class SecurityConfig extends WebSecurityConfigurerAdapter {
	@Override  
	protected void configure(HttpSecurity http) throws Exception {    
		http.authorizeRequests()    
		.anyRequest().authenticated()    
		.exceptionHandling()    
		.authenticationEntryPoint(digestEntryPoint())    
		.and()    
		.addFilter(digestAuthenticationFilter());  
	}  
	// rest of the code omitted for clarity 
}
```

对于这个更新实现，我们更换基础验证为更安全的再要认证模式。

### 注意

由于HTTP摘要认证提供了一个在不安全网络上发送凭证的机制。，读者应该知道MD5算法已知的现在和应该小心处理的地方。更多信息可以在<https://en.wikipedia.org/wiki/Digest_access_authentication>找到。