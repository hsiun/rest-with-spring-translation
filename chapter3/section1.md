# Inventory服务

我们属性管理服务的一个核心就是展现房间，这个房间代表的是顾客可以预定的物理房间。房间被组织成目录。一个房间目录表示一组逻辑上相似的房间。举个例子，我们会有一个_双人房_目录来保存所有两张床的房间。房间包含的属性如下代码所示：
```java
@Entity(name = "rooms") 
public class Room {
		private long id;		
		private RoomCategory roomCategory;		
		private	String name;		
		private	String description;
		@Id		
		@GeneratedValue		
		public long getId() {				 
			return id;
		}
		@ManyToOne(cascade = {CascadeType.PERSIST, CascadeType.REFRESH}, fetch = FetchType.EAGER)		public RoomCategory getRoomCategory() {				
			return roomCategory;		
		}
		@Column(name = "name", unique = true, nullable = false, length = 128)		
		public String getName()	{				
			return name;		
		}
		@Column(name = "description")		
		public String getDescription() {				
			return description;	
		} 
} 
```

由于使用了*Java持久化API(JPA)*和Hibernate，房间有一个自动生成的注解（感谢`@javax.persistence.Id` 和 `@javax。persistence.GeneratedValue` 注解）:这个选项描述必须和一个唯一且强制的命令一起。

### 注意

JPA不在本书范围之内。关于它的信息可以在<http://en.wikipedia.org/wiki/Java_Persistence_API>

另外，目录和房间之间一对多关系的表明是通过使用`@javax。persistence.ManyToOne`注解表明的。

`Inventory`服务提供对房间和目录的访问。这部分提供了几个可用的操作。然而，我们本章只对其中一个操作感兴趣。因此，让我们考虑下面的Java接口：
```
public interface InvertoryService {
	public Room getRoom(long roomId);

	//出于简化的目的省略
}
```

这个服务接口给我们通过房间Id来查找房间的能力。估计我们会有这个接口的一个实现，下一步就是通过我们 的RESTful接口暴露这个这个接口。下面的章节描述了如何这样做。
