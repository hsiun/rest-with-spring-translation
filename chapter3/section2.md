# REST和MVC模式

Spring Web MVC模式提供了传统** 模型 视图 控制器 **模式的实现。而REST不要求使用任何特定的模式，使用MVC模式非常自然的符合了RESTful的资源和模型通过控制器发布的特点。视图在我们这里将会是一个JSON表示的模型。

不用担心太多，让我们看一眼：
```java
@RestController @RequestMapping("/rooms") 
public class RoomsResource	{
	private final InventoryService inventoryService;
	public RoomsResource(InventoryService inventoryService)	{				
		this.inventoryService = inventoryService;		
	}
	@RequestMapping(value = "/{roomId}", method = RequestMethod.GET)		
	public RoomDTO getRoom(@PathVariable("roomId") String roomId)	{				
		RoomDTO room = ...				
		//	omitted	for	sake of clarity				
		return	room;		
	} 
}
```

通过使用`@org.springframework.web.bind.annotation.RestController`，我们告诉Spring `RoomResource`是一个控制器。

### 技巧

一般来说，这个控制器类也许被期望称为`RoomController`。然而，在RESTful架构模型中，关键概念是关于资源解析。因此，使用_Resource_后缀更加符合REST原则。

在这些代码中需要注意的其他注解是
`@org.springframework.web.bind.annotation.RequestMapping`。这个将会在下一节讨论。

### 注意
* 数据转换对象（DTO）*模式在这里（RoomDTO）被引用到了，但是我们将在第四章_数据表示_中看到更多细节。DTO提供了表示层和持久化层之间有效的解耦。