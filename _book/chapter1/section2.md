# Spring框架和REST

我们假定读者已经熟悉**Spring Framework**（从这里跳转到[Spring](http://www.spring.io)）。这样在这章我们就能专注于使用Spring构建RESTful Web服务的特点。

由于REST是关联到URIs的，因此Spring Web MVC框架提供了构建RESTful端点所有必要的工具。注解，如`org.springframework.web.bind.annotation.RequestMapping`和`org.springframework.web.bind.annotation.RequestParam`用在建立的端点中实现URLs和参数的基础映射。第三章，_第一个端点_将讨论这些注解并且提供示例代码展示怎么使用它们。

### 注意
关于Spring Web MVC的索引文档可以在<http://docs.spring.io/spring/docs/current/spring-framework-reference/html/mvc.html>找到。


随着技术要点的列出，现在让我们一起看看这样的RESTful服务。通过本书，我们将构建一个简单的Web服务，这个服务用于管理酒店及订单和账单。