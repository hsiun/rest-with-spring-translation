# Java Bean注解

为了实现输入验证，我可以使用在JavaEE6中引入的Java Bean验证注解。为了展示他们的用法，让我们一起实现在我们简单Web服务中查询订单的端点。我们订单服务接受下格式Java类的请求：

```java
public class BookingRequest {
    @Min(1)  
    private final long roomId;

    @NotNull  
    private final DateRange dateRange;
  
    @Size(min = 1, max = 128)  
    private final String customerName;

    @NotNull  
    private CreditCardDetails creditCardDetails; 
}
```

可以看到这里使用了`@javax.validation.constraints.Min`,`@javax.validation.constraints.NotNull`和`@javax.validation.constraints.Size`。`@Min`注解允许定义roomId最小验证值。`@NotNull`注解保证这个域非空。最后，`@Size`注解帮助保证了客户的名字不会长于数据库这个类型的大小。

