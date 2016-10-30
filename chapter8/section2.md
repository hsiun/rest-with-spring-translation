# 黑盒测试

我们构建的简单资源管理系统，我们使用Java接口来实现RESTful层和服务实现的解耦。除了有助于代码库的结构和阻止紧耦合，这个过程也有助于单元测试。确实，当我们测试我们应用的Web侧时，替代使用具体服务实现可以通过模拟来实现。举例，请看下面的单元测试代码：

```
public class RoomsResourceTest {  
    @Test  
    public void testGetRoom() throws Exception {    
        RoomsResource resource = new RoomsResource();    
        InventoryService inventoryService = ...    
        ApiResponse response = resource.getRoom(1);    
        assertEquals(Status.OK, response.getStatus());    
        assertNotNull(response);    
        RoomDTO room = (RoomDTO) response.getData();    
        assertNotNull(room);    
        assertEquals("Room1", room.getName());  
    } 
}
```

当我们调用`RoomResource.getRoom()`获取一个存在的房间时，我们期望返回非空，成功响应一个包含表示房间的有效实体。而不是使用真实的`com.packtpub.springrest.inventory.InventoryService`实现，那样做依赖于数据库。我们可以创建一个模拟的实现。这个模拟测试必需允许我们测试通过`com.packtpub.springrest.inventory.web.RoomsResource`处理不同用例且展示预定义的行为。这可以通过两种方法实现，这正是下一小节所要说明的。
