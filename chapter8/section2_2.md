# 使用mocking库实现stubbing

当提到Java中mocking库的时候有好几个选项。如JMock（<http://www.jmock.org>）或者是EasyMock（http://easymock.org）。**Mockito**是其中最流行的之一。Mockito是一个mocking框架，它让开发者写出很纯粹的测试并提供了简单API。开发者可以通过加入下面的依赖到它们项目描述器中来添加Mockito到它们的Maven项目中。

```xml
<dependency>  
	<groupId>org.mockito</groupId>  
	<artifactId>mockito-core</artifactId>  
	<version>1.9.5</version>  
	<scope>test</scope> 
</dependency>
```

为了展示如何使用Mockito，看一眼下面的测试：

```java
@Test 
publi void testUpdateRoom() {  
	InventoryService service = mock(InventoryService.class);  
	RoomCategory category = ... // skipped for clarity  
	Room room = ... // skipped for clarity  
	when(service.getRoom(1)).thenReturn(room);  
	when(service.getRoomCategory(anyLong()))  
		.thenReturn(category);  
	Room updatedRoom = ... // skipped for clarity  
	updatedRoom.setDescription("It's an awesome room!");  
	ApiResponse response = resource.updateRoom(1, new RoomDTO(updatedRoom));
	assertEquals(Status.OK, response.getStatus());  
	assertEquals("It's an awesome room!", ((RoomDTO) 
		response.getData()).getDescription()); } 
```

这个测试验证如果可能的话更新存在的房间。代替我们自己实现`InventoryService`，我们通过`mock(InventoryService.class)`使用Mockito来创建mock实现。下一步是当调用的时候指示我们的mock返回一个房间和房间的目录。这是通过使用` when(…).thenReturn(…)`实现的。这种模式添加行为到我们的mock。举例，当`InventoryService.getRoom()`被调用来查询ID为1的房间是`when(service.getRoom(1)).thenReturn(room)`将使我们的mock服务返回一个房间。