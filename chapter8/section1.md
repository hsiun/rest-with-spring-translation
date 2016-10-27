# 单元测试Spring控制器

一旦我们使用注解将Java方法声明为RESTful端点，一般的单元测试就可以部署了。Java实际上的单元测试库是Junit。Junit是一个用于创建可重复测试的简单框架。下面的代码表明了我们可以如何测试RESTful端点：

```
public class AvailabilityResourceTest {  
    @Test  
    public void testGetAvailability() throws Exception {    
        AvailabilityService service = ...    
        AvailabilityResource resource = new AvailabilityResource(service);    
        WebRequest request = ...    
        // invalid from date    
        ApiResponse response = resource.getAvailability(null, "2017-01-02", "1", request);    
        assertEquals(Status.ERROR, response.getStatus());    
        assertEquals(17, response.getError().getErrorCode());    
        // from is after until    
        response = resource.getAvailability("2017-01-03", "2017-01-02", "1", request);    
        assertEquals(Status.ERROR, response.getStatus());    
        assertEquals(17, response.getError().getErrorCode());  } }
```

大多数读者对这种方式的测试应该很熟悉。这里，我们确认了可用服务部分（我们简单资源管理系统的）不接受无效数据。这段代码中没有覆盖到的是`com.packtpub.springrest.availability.AvailabilityService`和`org.springframework.web.context.request.WebRequest`实例是如何获取的。这两个接口依赖我们并不打算真正实现。在测试中，我们仅仅对测试我们资源类中的代码感兴趣。下一节讨论的模拟测试就是处理这种情况。