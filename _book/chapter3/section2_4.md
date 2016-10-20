# 请求参数映射

除了路径参数，请求参数也可以被索引到`RestController`类。`@org.springframework.web.bind.annotation.RequestParam`参数提供将HTTP查询参数映射到Java方法的属性。为了说明参数映射，让我添加新的查找方法到我们的资源类：
```java
@RequestMapping(method = RequestMethod.GET) 
public List<RoomDTO> getRoomsInCategory(@RequestParam("categoryId") long categoryId) {		
	RoomCategory category = inventoryService.getRoomCategory(categoryId);		
	return inventoryService.getAllRoomsWithCategory(category)
		.stream().map(RoomDTO::new).collect(Collectors.toList()); }
```

对如<http://localhost:8080/rooms?categoryId=1>URL的请求，将会由这个方法处理，并且方法的属性`categoryId`将会被设置为1。这个方法将以JSON格式返回一列通过给定目录查到的房间，如下所示：
```
[		
	{				
		"id": 1,				
		"name": "Room 1",				
		"roomCategoryId": 1,				
		"description": "Nice, spacious double bed room with usual amenities"				
	} 
]
```

### 技巧
服务的设计者也可以不使用参数来声明这个端点。举个例子，URL的模式应该会是`/rooms/categories/{categoryId}`。这个方法对于提升缓存性能有额外的好处，因为不是所有的浏览器和代理都会缓存查询参数的。参考第六章，_性能_，获取关于缓存技术的更多细节。

随着我们在本书的余下部分持续实现我们的属性管理系统，我们将继续练习这种映射结构。第五章，_REST中的CRUD操作_，将着重介绍在REST中如何使用这些注解映射CRUD（创建，读取，更新和删除）操作。

### 技巧

之前的代码片段促使我们使用新的Java流API，这些在Java 8中提出的新API对于函数式编程有一些好处。<http://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html>可以阅读更多信息。