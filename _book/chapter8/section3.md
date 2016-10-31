# 测试安全性

Spring对单元测试有很好的支持。开发者可以添加新的依赖到它们的Maven项目中来包含Spring对测试的支持，如下：

```xml
<dependency>    
	<groupId>org.springframework</groupId>    
	<artifactId>spring-test</artifactId>    
	<version>4.1.6.RELEASE</version>    
	<scope>test</scope> 
</dependency> 
<dependency>    
	<groupId>org.springframework.security</groupId>    
	<artifactId>spring-security-test</artifactId>    
	<version>4.0.1.RELEASE</version>    
	<scope>test</scope> 
</dependency> 
```

因为我们不希望这些依赖被包括进最终产品，我们指明了`test`范围。这么做将指示这些库尽在测试的时候在classpath中可用。

在第七章，_处理安全_，我们添加安全性到我们简单资源管理系统的订单部分。作为参考，我们限制访问RESTful端点获取订单，如下：

```java
@PreAuthorize("hasRole('ADMIN')") 
@RequestMapping(value = "/{bookingId}", method = RequestMethod.GET) 
public ApiResponse getBooking(@PathVariable("bookingId") long bookingId) {    
	// omitted 
}
```

在标准单元测试中，我们不能只允许管理员访问这个端点。使用Spring的测试支持，我们可以像下面这样来对这个端点写单元测试：

```java
@RunWith(SpringJUnit4ClassRunner.class) 
@ContextConfiguration("classpath:booking-test.xml") 
public class BookingsResourceTest {
	@Autowired  
	private BookingService bookingService;  
	@Autowired  
	private BookingsResource resource;
	@Test(expected = AuthenticationCredentialsNotFoundException.class)  
	public void testGetBookingNotLoggedIn() throws Exception {    
		resource.getBooking(1);  
	}
	@Test(expected = AccessDeniedException.class)  
	@WithMockUser  
	public void testGetBookingNotAdmin() throws Exception {    
		resource.getBooking(1);
	}
	@Test  
	@WithMockUser(roles = {"ADMIN"})  
	public void testGetBookingValidUser() throws Exception {    
		when(bookingService.getBooking(1)).thenReturn(new Booking());    
		assertNotNull(resource.getBooking(1));  、
	} 
}
```

通过使用`@org.junit.runner.RunWith`注解测试类，我们使用Spring的runner代替标准的JUnit runner。

因为没有在`testGetBookingNotLoggedIn()`定义鉴权，我们希望异常能被抛出。

感谢`@org.springframework.security.test.context.support.WithMockUser`，我们第二种测试方式声明了一个用户。然而，因为用户有默认的角色，USER，我们也希望异常能被抛出。

最终，第三种测试方法（testGetBookingValidUser()）使用正确的角色声明了一个用户，并且因此可以处理遍历ID为1的订单。
