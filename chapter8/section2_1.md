# 简单黑盒测试

为了提供必要的行为，我可以简答创建一个Inventory服务实现：

```
InventoryService inventoryService = new InventoryService() {  
	@Override  
	public Room getRoom(long roomId) {    
		if (roomId == 1) {      
			Room room = new Room();      
			room.setName("Room1");      
			room.setDescription("Room description");      
			RoomCategory category = new RoomCategory();      
			category.setName("Category1");      
			category.setDescription("Category description");      
			room.setRoomCategory(category);      
			return room;    
		} else {      
			throw new RecordNotFoundException("");    
		}  
	}  
	// rest of code omitted 
}; 
```

在这种方法中，我们手动实现`InventoryService`接口并插入我们需要的代码。我们也返回RoomId为1时房间的值，除此之外也抛出`RecordNotFoundException`异常。

出于可读性的考虑，我们省略了这些代码片段中发布其他方法的部分。但是这里就是简单模拟测试部分的挑战。开发者不得不写大量代码提供没有值的单元测试，但是每当新的功能添加到服务中时这些代码必须要更改。这就是Mock测试库被提出的原因，下一节讨论使用这样的库。
