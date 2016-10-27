# REST资源

现在让我们考虑，我们需要创建来通过RESTful API发布的这些功能的端点。先回答一个基础的问题，再来实现这个端点，问题就是这个资源在哪个URL下可用？一种可能的方法是在我们已存在的房间资源上添加一个新的端点（参考第三章，_第一个端点_）。然而，由于我们需要不仅仅是返回一列房间，这不是主要的程序逻辑。除此之外，出于扩展的理由，我们也许需要部署这部分结构在一个单独的Inventory服务结构上（这些概念在第十章，_扩展RESTful Web服务_中讨论）。因此，我们将新的资源暴露在新的URL之下：

```Java
@RestController 
@RequestMapping("/availability") 
public class AvailabilityResource {
	@RequestMapping(method = RequestMethod.GET)  
	public ApiResponse getAvailability(    
		@RequestParam("from") String from,    
		@RequestParam("until") String until,   
		@RequestParam(value = "roomCategoryId", required = false) String categoryId) {    
   // omitted  
 } 
}
```

对于这个新的Spring `RestConroller`，可以通过如<http://localhost:8080/availability?from=2016-12-01&until=2016-12-01>的URL查下可用的房间。这个URL将返回在2016年12月1号可用的房间列表。

### 注意

使用什么样的格式表示日期需要上升到开发者来决定。举个例子，日期可以接受UNIX时间<https://en.wikipedia.org/wiki/Unix_time>。在我们这里，我们选择ISO 8601格式<https://en.wikipedia.org/wiki/ISO_8601>来表示时间，这样更有利于人类阅读。

而且，我们也定义了称之为`roomCategoryId`的查询参数，这是一个可选参数。在Spring中，我们可以通过使用下面的注解实现这个目的:
```
@RequestParam(value = "roomCategoryId", required = false) 
```

正如我们在第五章，_REST中的CRUD操作_看到的，这个注解指示Spring如果查询参数`roomCategoryId`存在，则映射为Java方法参数。


### 技巧
如果没有声明这个参数为不必须，这个参数出现在了URL中，Spring将产生一个带有400HTTP状态码的错误响应。

查询给定时间内可用的房间将返回下面数据：
```
{		
	"status": "OK",		
	"data":	[{				
		"date":	"2016-12-01",				
		"rooms": [{						
			"id": 1,						
			"name":	"Room 1",						
			"roomCategoryId": 1,						
			"description":	"Nice, spacious double bed room with usual amenities"				
		}]	
	}] 
}
```

如前所述，这个响应的特定期间内可用房间列表。在这儿，ID为1房间在2016年12月1号可用。

这个RESTful端点一旦定义，让我们一起看下如何为这个端点添加HTTP缓存支持。