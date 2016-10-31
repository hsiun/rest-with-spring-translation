# 重写HTTP方法

在某些情况下（举个例子，当服务或者是它的消费者在严苛的企业防火墙之后的时候，或者主要消费者是Web网页），这时候可能只有GET和POST HTTP方法是可以使用的。在这种情况下，可以通过在请求中传递定制的头部来模拟缺少的动词。

举个例子，资源更新请求可以由设置了自定义头部（如，X-HTTP-Method-Override）为PUT的POST请求来处理，重写设置表明我们通过POST请求模拟PUT请求。下面的方法将处理这种方案：

```java
@RequestMapping(value = "/{roomId}", method = RequestMethod.POST, headers = {"X-HTTP-Method-Override=PUT"}) 
public ApiResponse updateRoomAsPost(@PathVariable("roomId") long id, @RequestBody RoomDTO updatedRoom) {		
	return updateRoom(id, updatedRoom); 
}
```

通过在映射注解中设置`header`属性，Spring请求路由将拦截带有我们自定义头部的POST请求，并调用这个方法。一般来说`POST`请求将依然会映射到这个Java方法，我们把创建新房间放到一起。

