# 使用Spring Boot进行集成测试

通过使用方便的注解Spring Boot对继承测试提供了很好的支持，正如下面的代码片段所展示的：

```java
@RunWith(SpringJUnit4ClassRunner.class) 
@SpringApplicationConfiguration(classes = WebApplication.class) 
@WebAppConfiguration 
@IntegrationTest("integration_server:9000") 
public class BookingsResourceIntegrationTest {
	@Test  
	public void runTests() {    
		// ...  
	} 
}
```

正如在本章之前描述的，`@org.junit.runner.RunWith`注解允许使用一个具有选择性的测试runner。在这里，我们使用Spring的runner代替JUnit默认的。另外，我们指定通过`@org.springframework.boot.test.IntegrationTest`来指定连接的地址。对于这些注解，我们可以连接到运行我们简单订单服务的服务器，和运行针对它的集成测试套件。

### 技巧
你可以参考下一章远程调用RESTful Web服务的示例代码。可以用相同的技术来实现集成测试。
