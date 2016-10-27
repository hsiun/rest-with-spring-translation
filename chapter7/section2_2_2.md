### 在Spring中使用基础鉴权

让我们一起看看如何设置使得RESTful Web服务支持基础鉴权。首先，我们需要添加几个新的依赖到我们的项目中：

```
<dependency>  
    <groupId>org.springframework.security</groupId>  
    <artifactId>spring-security-config</artifactId>  
    <version>4.0.1.RELEASE</version>
</dependency> 
<dependency>  
    <groupId>org.springframework.security</groupId>  
    <artifactId>spring-security-web</artifactId>  
    <version>4.0.1.RELEASE</version> 
</dependency> 
```

这将会导入Spring的Web安全模块，正如他的配置所支持的。下一步将配置安全。我们可以在Java中这样做通过声明下面的类：

```java
@EnableWebSecurity 
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Autowired  
    public void configureGlobal(AuthenticationManagerBuilder auth)    
        throws Exception {    
        auth.inMemoryAuthentication()    
        .withUser("rest").password("rocks").roles("USER");  
    }  
    @Override  
    protected void configure(HttpSecurity http) throws Exception {    
        http.authorizeRequests()    
        .anyRequest().authenticated()    
        .and().httpBasic();  
    } 
}
```

这是个非常简单的配置，不是预生产配置，但是简单到足够表明Spring安全的配置。我们定义了一个用户名为，rest，密码为，rocks的用户。我们也指示使用HTTP基础鉴权模式验证所有请求。

### 技巧
在真实系统中，用户不会被存储在内存中（在示例中使用`auth.inMemoryAuthentication()`是这种情况），但是在数据库中密码是被加密使用的。例如，*Bcrypt*加密（<https://en.wikipedia.org/wiki/Bcrypt>）。

最后一步剩下的部分是在我们Web服务中使用这个安全配置。我们可以通过继承`org.springframework.security.web.context.AbstractSecurityWebApplicationInitializer `这样做，如下所示：

```java
public class SecurityWebApplicationInitializer extends 
         AbstractSecurityWebApplicationInitializer {
    public SecurityWebApplicationInitializer() {    
        super(SecurityConfig.class);  
    } 
}
```

传递我们的安全配置类到超类将保证所有对我们简单Web服务的请求都将被加密。
