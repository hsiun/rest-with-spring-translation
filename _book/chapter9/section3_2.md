# 摘要验证

对于这种验证模式，让我们一起看下开发者怎么将Apache的HttpClient（https://hc.apache.org）作为底层的HTTP客户端框架。为了实现这个目标，我们需要添加下面依赖到我们项目。

```xml
<dependency>  
    <groupId>org.apache.httpcomponents</groupId>  
    <artifactId>httpclient</artifactId>  
    <version>4.3.4</version> 
</dependency>
```

另外，我们要我们创建`RestTemplate`实例的方法：

```java
CredentialsProvider provider = new BasicCredentialsProvider(); 
CloseableHttpClient client = HttpClientBuilder.create().setDefaultCredentialsProvider(provider).build(); UsernamePasswordCredentials credentials = new UsernamePasswordCredentials(username, password); 
provider.setCredentials(AuthScope.ANY, credentials); 
RestTemplate template = new RestTemplate(new DigestAuthHttpRequestFactory(host, client));
```

通过传递请求的工厂给模板，我们可以让HttpClient来管理摘要验证。如下所示，我们需要创建一个``的继承类：

```java
@Override		
protected HttpContext createHttpContext(HttpMethod httpMethod, URI uri)	{								
	AuthCache authCache = new BasicAuthCache();								
	authCache.put(host,	new DigestScheme());								
	BasicHttpContext localcontext = new BasicHttpContext();								
	localcontext.setAttribute(AUTH_CACHE, authCache);								
	return localcontext;				
} 
```

这个类创建了一个存储了摘要凭证的HTTP上下文。
