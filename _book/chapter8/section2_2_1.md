# Mockito和Spring

通过使用`@org.springframework.beans.factory.annotation.Autowired`，Spring提供了机制自动将bean注入到类中。这个注解可以如下这样使用：

```java
@RestController @RequestMapping("/bookings") 
public class BookingsResource {
    @Autowired
    private BookingService bookingService; } 
```

在启动时，Spring将查询所有声明未`InventoryService`类型的bean，并注入它。这个机制减少了需要实现的样板代码。然而，它使得测试有点复杂，例如这些代码，我们不直接访问可用的`bookingService`实例。谢天谢地，Mockito提供了几个有用的注解来绕过这个限制。我们可以如下声明我们的测试类：

```java
@RunWith(MockitoJUnitRunner.class) 
public class BookingsResourceTest {
    @InjectMocks    
    private BookingsResource resource;
    @Mock    
    private BookingService bookingService; 
}
```

第一个注解（@org.junit.runner.RunWith）允许我们使用Mockito的runner替代标准的JUnit runner。对于` @org.mockito.InjectMocks`，我们将这个域标记为注入。另外，我们使用`@org.mockito.Mock`声明`bookingService`。这将会自动生成一个mock，并且这个mock将会被注入到我们`BookingsResource`实例中。然后我们可以运行我们测试资源和服务的类用具体例证说明我们。


### 注意
通过它们的网站<http://mockito.org>阅读关于Mockito的更多信息。