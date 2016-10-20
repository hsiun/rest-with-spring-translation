# 数据转换对象设计模式

数据转换对象，是对应用各层之间专递信息的一个简单封装。这个模式在数据存储层和数据表现层之间提供了一个很好的抽象层。

这样对象的定义一般来说是没有业务逻辑的，只有各项数据简单的获取设置方法。在我们简单属性管理Web系统的情境下，作为例子，我们为`Rooms`声明一个DTO类。下面的代码片段展示了这个DTO类：

```Java
public class RoomDTO implements Serializable {
	private static final long serialVersionUID = 2682046985632747474L;
	private long id;				
	private	String name;				
	private	long roomCategoryId;				
	private	String description;
				
	public RoomDTO(Room	room)	{								
		this.id	= room.getId();								
		this.name = room.getName();								
		this.roomCategoryId	= room.getRoomCategory().getId();								
		this.description = room.getDescription();				
	}

	public long getId()	{								
		return id;				
	}
				
	public String getName() {								
		return name;				
	}

	public long getRoomCategoryId()	{								
		return roomCategoryId;				
	}

	public String getDescription() {								
		return description;				
	} 
}
```

在这个例子中，我们定义了将要在我们服务的数据层（在这里，我们的API以JSON响应）使用的房间属性。我们数据层对象以一个构造器参数传入，这样DTO对象可以很容易的初始化。

DTO对象不需要实现`java.io.Serializable`。然而，可以这样做，为了在不同的JVM上运行应用的不同层，这样做是有用的。

### 注意
你可以在维基百科的<http://en.wikipedia.org/wiki/Data_transfer_object>阅读这个模式特点。

读者也许知道这个模式也被称为值-对象设计模式。早起的Java EE文献错误的使用这个属于描述数据转换。

语义上来说，值-对象设计模式和DTO设计模式十分不同。DTO对象是一个自定义版本的数据模型对象，值-对象对象表示固定的数据集，类似于Java的枚举类型。他们通常通过值来确定并且不会改变。

### 技巧
当使用Java持久化API（正如我们在简单Web服务中使用Hibernate做的），DTO是非常有用的，混合了持久化和表示层的概念在一个类中是非常灵活的，并且通常也会引起冲突。