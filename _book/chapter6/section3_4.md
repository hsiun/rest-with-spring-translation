# 通过Etag缓存

当产生的最后修改日期是不合适的时候，ETags可以用来作为替代。Spring以过滤器的形式对ETags提供透明支持，过滤器可以添加到REST servlet上。这个过滤器自动对响应生成一个MD5的哈希值。

过滤器可以添加在Web应用描述器（web.xml）中：

```xml
<filter>		
	<filter-name>etagFilter</filter-name>		
	<filter-class>				
		org.springframework.web.filter.ShallowEtagHeaderFilter		
	</filter-class> 
</filter> 
<filter-mapping>		
	<filter-name>etagFilter</filter-name>		
	<url-pattern>/*</url-pattern> 
</filter-mapping>
```

另一种选择，当使用Spring Boot的时候，可以通过添加配置类来添加过滤器：

```java
@Configuration 
@EnableWebMvc 
@ComponentScan 
public class WebApplicationConfiguration extends WebMvcAutoConfiguration {
	@Bean		
	public Filter etagFilter() {				
		return new ShallowEtagHeaderFilter();		
	} 
} 
```

当客户端第一次发起对availability的请求，服务器返回下面的报文头部：

```
HTTP/1.1
200 OK Server: Apache-Coyote/1.1 
ETag: "09f4ab0b7ca5d8280fbb890a6a5e1c220" 
Content-Type: application/json;charset=UTF-8 
Content-Length:	463 
Date: Mon, 15 Jun 2015 12:40:31 GMT
```

重新发布同样请求，Web浏览器将会包含下面头部：

```
GET /availability?from=2016-12-01&until=2016-12-01 HTTP/1.1 
// omitted 
If-None-Match: "09f4ab0b7ca5d8280fbb890a6a5e1c220"
```

服务器将会回复下面响应：

```
HTTP/1.1 304 Not Modified Server: Apache-Coyote/1.1 
ETag: "09f4ab0b7ca5d8280fbb890a6a5e1c220" 
Date: Mon, 15 Jun 2015 12:50:00 GMT 
```

并没有发送真实的响应体，并且浏览器被指示使用他自己本地缓存的拷贝了替代。由于这种方法在缓存数据没有改变的情况下提供了透明机制，因此它对于提升服务器端的性能没有帮助。