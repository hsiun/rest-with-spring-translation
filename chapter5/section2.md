# 创建资源

我们简单管理系统的Inventory部分处理的是房间。在第三章，_第一个端点_，我们建立了一个端点访问房间。让我们一起看下如何定义一个端点创建新的资源：

```
@RestController 
@RequestMapping("/rooms") 
public class RoomsResource {
	@RequestMapping(method = RequestMethod.POST)		
	public ApiResponse addRoom(@RequestBody RoomDTO room) {				
		Room newRoom = createRoom(room);				
		return new ApiResponse(Status.OK, new RoomDTO(newRoom));		
	} 
} 
```

我们添加了一个新的方法到我们RoomsResource类，这个方法用来处理创建新的房间。正如第三章中描述的，`@RequestMapping`用来将请求映射到Java方法。这里，我们映射POST请求到addRoom()函数。

### 技巧
@RequestMapping没有指明路径值的话，等价于使用"/"。我们对传入的新房间使用`@RequestBody`注解。这个注解指示Spring将进入的web请求体映射到方法参数。Jackson在这里被用于转换JSON请求体到Java对象。

关于我们的新方法，使用下面JSON体POST请求<http://localhoost:8080/rooms>的结果是将创建一间新的房间。
```
{		
	name: "Cool Room",		
	description: "A room that is very cool indeed",	
	room_category_id: 1 
}
```

我们新的方法将返回这个新建的房间：

```
{		
	"status":"OK",		
	"data":{				
		"id":2,				
		"name":"Cool Room",				
		"room_category_id":1,				
		"description":"A room that is very cool indeed"		
	} 
}
```

我们可以（只返回新资源的ID）在响应创建资源的时候。然而，因为我们也许头脑清醒或者另外操作数据发送，返回全部资源是一个最佳实践。