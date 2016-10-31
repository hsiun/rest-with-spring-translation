# 声明客户端

客户端一旦就位，现在让我们一起进入简单属性管理系统客户端的构建吧！我们将通过Inventory模块开始，使用下面（简单的）接口:

```java
public interface InventoryServiceClient {    
 public Room getRoom(long roomId); 
}
```

这个接口允许通过ID遍历房间。


### 注意

下一章将讨论为何将我们客户端声明为接口是一个好主意。
现在我们可以开始实现我们的客户端了：
```java
public class RemoteInventoryServiceClient implements InventoryServiceClient {
    private final String serviceUrl;    
    private final RestTemplate template;
    public RemoteInventoryServiceClient(String serviceUrl) {        
        this.serviceUrl = serviceUrl;        
        template = new RestTemplate();    
 }
 @Override    
 public Room getRoom(long roomId) {        
    ParameterizedTypeReference<ApiResponse<Room>> typeReference = new ParameterizedTypeReference<ApiResponse<Room>>() {};
    return (Room) ResponseHandler.handle(            
     () -> template.exchange(serviceUrl + "/rooms/" + roomId, HttpMethod.GET, null, typeReference).getBody());    
    } 
}
```

这里主要的类是Spring通过`org.springframework.web.client.RestTemplate`提供给我们的。这个类让我们可以通过使用`RestTemplate.exchange()`发送HTTP请求到后端服务。

正如在第四章，_数据表示_中讨论的，我们服务响应被封装为一个包括请求状态的统一的格式。因为所有的响应都被处理成统一的格式，我们可以创建一个统一的方法用一致的手段去处理他们。这就是`ResponseHandler.handle()`所做的。

因为我们使用通用的类型去处理将会包含响应实体的类型，我们需要传递这个信息给Spring，这样他才能正确提取数据。这是通过声明`ParameterizedTypeReference`实现的。

### 注意
注意这一点，JSON处理不需要特殊设置。这得感谢classpath中的Jackson，它将会自动处理转换。