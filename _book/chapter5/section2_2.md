# JSON VS 表单数据

发送表单是在在Web中创建一个实体的传统方法，而且他也很容易用于创建新的RESTful资源。我们可以改变我们的方法成下面这样子：

```
@RequestMapping(method = RequestMethod.POST, consumes = MediaType.APPLICATION_FORM_URLENCODED_VALUE) 
public ApiResponse addRoom(String name, String description, long roomCategoryId) {
	Room room = createRoom(name, description, roomCategoryId);
	return new ApiResponse(Status.OK, new RoomDTO(room)); 
}
```

主要的不同就是（和前面的方法）这是我们告诉Spring映射到表单请求代替JSON请求。另外，替代使用对象作为参数，我们独立的接收每一个值。

默认情况下，Spring将使用Java方法属性的名字映射传入表单的输入。开发者可以改变这种行为，通过使用@RequestParam("...")注解属性映射到一种特殊的输入名称。

在主要的Web服务消费者是Web应用的情况下，使用表单请求也许更恰当。在大多数情况下，然而，