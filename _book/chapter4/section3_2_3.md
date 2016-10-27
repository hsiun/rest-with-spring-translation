# 其他方式

除了上面描述的两种方法之外，应该考虑使用一种其他解决方案。举个例子，一个专用的报文头，如当API版本被使用的时候，`X-API-Version`应该做特定的用途。下面的代码将在我们第三版的API中处理请求来获取房间：

```
@RequestMapping(value = "/{roomId}", method = RequestMethod.GET, headers = {"X-API-Version=3"}) 
public RoomDTOv3 getRoomV3(@PathVariable("roomId") long id) {  
	Room room = inventoryService.getRoom(id);  
	return new RoomDTOv3(room); 
}
```

在这个示例中，我们指示Spring将包含报文头`X-API-Version`值为3，对`/rooms/{roomId}`的请求映射到这个方法。

无论选择使用那个技术，API设计在脑海中应该记住下面的几条原则：

* 只在需要时发布；维护向后兼容是件困难的事。
* 喜欢向前兼容，改变将会破坏向前兼容。强迫客户端升级到新的API版本不忠实可能的。
* 从一开始，设计API就应该支持变更。却决于选择的方法，API的向后移植不会简单。