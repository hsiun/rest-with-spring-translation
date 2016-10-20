# 更新端点

下面的方法提供了修改房间必要的端点。

```
@RequestMapping(value = "/{roomId}", method = RequestMethod.PUT) 
public ApiResponse updateRoom(@PathVariable long roomId, @RequestBody RoomDTO updatedRoom)	{		
	try	{				
		Room roo = updateRoom(updatedRoom);				
		return new ApiResponse(Status.OK, new RoomDTO(room));		
	} catch (RecordNotFoundException e)	{				
		return new ApiResponse(Status.ERROR, null, new ApiError(999, "No room with ID " + roomId));		
	} 
} 
```

正如在这章开始讨论的，我们将更新资源的请求映射到HTTP PUT动词。这个方法的注解`@RequestMapping(value = "/{roomId}", method = RequestMethod.PUT)`指示Spring直接PUT请求到这里。

房间Id是路径的一部分，并被映射到第一个方法参数。在类似的完成资源创建的请求中，我们使用`@RequestBody`将更新实体映射到我们第二个参数。
