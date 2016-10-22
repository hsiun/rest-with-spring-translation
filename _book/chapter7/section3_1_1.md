### URL映射

扩展我们之前的示例，我们可以修改`SecurityConfig`来声明一个细粒度的URL映射如下：

```
@EnableWebSecurity public	class	SecurityConfig	extends	WebSecurityConfigurerAdapter	{		@Override		protected	void	configure(HttpSecurity	http)	throws	Exception	{				http.authorizeRequests()				.antMatchers(HttpMethod.GET,	"/bookings/**").hasRole("ADMIN")				.anyRequest().authenticated();		} }
```

对于这个新版本，我们指示Spring只允许管理员访问读取订单。所有其他端点接收来自使用任何角色鉴权用户的请求。我们可以通过修改我们的类成下面这样来实现这个：

```
@EnableWebSecurity public	class	SecurityConfig	extends	WebSecurityConfigurerAdapter	{		@Autowired		public	void	configureGlobal(AuthenticationManagerBuilder	auth)		throws	Exception	{				auth.inMemoryAuthentication()				.withUser("rest").password("rocks").roles("USER")				.and()				.withUser("admin").password("admin").roles("ADMIN");		} } 
```

和我们rest用户一起，我们现在使用用户名，admin，和密码，admin声明了一个管理员用户。

对于这个新的配置，如果我们使用USER登陆并尝试访问订单，服务将返回一个`403 Forbidden`响应。局部的，现在你可以在Web浏览器中通过打开<http://localhost:8080/bookings/1>来测试这个行为。

### 注意
因为在HTTP基础鉴权或者是HTTP摘要鉴权模式下浏览器会换成凭证，登出是有一点棘手到 ，通常需要关闭浏览器。值得感谢的是，现代浏览器允许私密浏览。这个特征可以帮助我们加速开发并且测试Web服务的安全性。


这种方式整个的有助于Web服务的安全性，但是当要求更细粒度的鉴权是也坑内带来麻烦。确实，配置（Java或XML之一）可能会变得极难维护。下一节将描述一个更加灵活的方法。