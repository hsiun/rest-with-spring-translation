# HTTP请求映射

将特定的HTTP方法映射到类或是Java方法是可行的。我们的`RoomsResource`类发布一个通过ID检索房间的方法。它的声明如下所示：
```
@RequestMapping(value = "/{roomId}", method = RequestMethod.GET)
```

在类级的注解组合中，带有以下`/rooms/{roomId}`值的GET请求将被映射到`RoomResource.getRoom()`。

其他方法的请求（如，PUT或者DELETE）将不会映射到这个Java方法。