# 表示版本

在之前的例子中，我们对`Rooms`产生了不同的表示。我应该因此考虑下通过MIME类型版本来管理版本。下面的示例代码片段展示了我们可以如何通过Spring Web来实现：

```java
@RequestMapping(value = "/{roomId}", method = RequestMethod.GET) 
public RoomDTO getRoom(@PathVariable("roomId") long id) 
{  
	Room room = inventoryService.getRoom(id);  
	return new RoomDTO(room); 
}

@RequestMapping(value = "/{roomId}", method = RequestMethod.GET, consumes = "application/json;version=2") 
public RoomDTOv2 getRoomV2(@PathVariable("roomId") long id) {  
	Room room = inventoryService.getRoom(id);  
	return new RoomDTOv2(room); 
}
```

对于这个设置，当它们请求报文头设置`Content-Type`为`application/json;version=2`时，`getRoomV2()`将被调用。