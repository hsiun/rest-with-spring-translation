# 测试更新请求

使用Postman我们可以快速的创建测试用例去更新我们之前创建的房间。为了这样做，我们使用下面JSON作为报文主体发送一个PUT请求：
```
{		
	id:	2,		
	name: "Cool Room",		
	description: "A room that is really very cool indeed",				
	room_category_id: 1 
}
```

并且响应的结果就是被更新的房间：
```
{		
	"status": "OK",		
	"data":	{				
		id:	2,		
		name: "Cool Room",		
		description: "A room that is really very cool indeed",				
		room_category_id: 1 		
	} 
}
```

如果我们尝试更新一个不存在的房间，服务器将会返回下面的通用响应：
```
{		
	"status": "ERROR",		
	"error": {				
		"error_code": 999,				
		"description": "No room with ID 3"		
	}
}
```

由于我们不支持在资源创建时更新，服务器返回一个错误表明资源无法找到。

### 注意
参考第四章，_数据展示_，讨论了错误处理和响应格式。
