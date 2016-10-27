# 删除资源

这并没有什么值得惊讶的是，我们使用`DELETE`动词去删除一个REST资源。你也许已经想到，删除请求的路径是/rooms/{roomId}。处理删除房间的Java方法如下所示：

```
@RequestMapping(value = "/{roomId}", method = RequestMethod.DELETE) 
public ApiResponse deleteRoom(@PathVariable long roomId)	{		
	try {				
		Room room = inventoryService.getRoom(roomId);				
		inventoryService.deleteRoom(room.getId());				
		return new ApiResponse(Status.OK, null);		
	} catch (RecordNotFoundException e)	{				
		return new ApiResponse(Status.ERROR, null, new ApiError(999, "No room with ID " + roomId));		
	} 
}
```
通过声明将请求方法映射到`@RequestMethod.DELETE`，Spring将使用这个方法来处理DELETE请求。

因为这个资源已经被删除，在响应中返回被删除的资源不符合大多数场景。服务设计者可以选择返回一个布尔标志去表明这个资源已经被成功删除。在我们这里，我们使用我们响应的状态部分去处理这个返回给消费者的信息。删除一个资源的响应如下所示：

```
{		
	"status":	"OK" 
}
```
对于这些操作，我们Inventory服务现在有了完整的CRUD API。在结束这章之前，一起来讨论下现在REST开发者可以如何处理不是所有HTTP动词都能被使用的场景。

