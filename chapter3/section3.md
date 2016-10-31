# 运行服务

建立在第二章，_通过Maven和Gradle构建一个RESTful的Web服务_的基础上，我们可以通过使用Spring Boot快速的启动，运行我们的服务。出于此目的，我们需要创建一个主类，如下所示：

```Java
package com.packtpub.springrest.inventory; 
//	imports	omitted 
@SpringBootApplication 
public class WebApplication	{
	public static void main(String[] args) {				
		SpringApplication.run(new Object[]{WebApplication.class, "inventory.xml"}, args);				
		InventoryService inventoryService = context.getBean(InventoryService.class);		
	} 
}
```

在你最拿手的IDE中运行这个类将启动一个内嵌的Tomcat实例，并且发布你的资源。服务将可以通过<http://localhost:8080>访问。作为示例，访问<http://localhost:8080/rooms/1>将返回下面内容：
```json
{
	"id": 1,
	"name": "Room 1",
	"rommCategoryId": 1,
	"description": "Nice, spacious double bed room with usual amenities"
}
```

### 注意
不同于第二章，_通过Maven和Gradle构建一个RESTful的Web服务_，在这个例子混合了自动探测和基于XML的配置。同时传递程序的类和我们XML的Spring配置（inventory.xml），Spring Boot将加载所有声明在XML中他能找到的注解了的bean。