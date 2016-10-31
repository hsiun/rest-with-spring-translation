# 基础验证

这种验证模式要求在`Authorization`头中包含使用Base64编码的用户名/密码对。这个可以通过修改客户端成下面这样来实现：

```java
public RemoteBookingServiceClient(String serviceUrl, String username, String password) {
	template = new RestTemplate();  
	String credentials = Base64.getEncoder().encodeToString((username + ":" + password).getBytes());  
	template.getInterceptors().add((request, body, execution) -> {    
		request.getHeaders().add("Authorization", "Basic " + credentials);    
		return execution.execute(request, body);  
	}); 
}
```

这个新的构造方法使用用户名和密码来验证客户端。然后它生成了Base64编码的凭证，为了每次请求都能带上`Authorization`，定义了一个新的`org.springframework.http.client.ClientHttpRequestInterceptor`。Spring的拦截器以适当的格式添加头部，并允许请求执行。