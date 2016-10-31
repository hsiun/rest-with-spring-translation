# 实现概览

这部分的目标是提供终端用户和第三方系统一个在给定时间段内查询可用房间的方法。

我们实现这个功能通过在我们的简单系统中查询所有房间，然后去掉在给定时间段内已经存在的订单，这样来计算出可用的房间。在大型酒店真实使用的系统中，一般会采用更成熟的算法来优化定位可用房间。然而，在我们这里，简单的方法也可以。因此，让我们一起考虑下下面的服务接口：
```java
public interface AvailabilityService {
	/**		
	*	Answers	the	availability status	for	the	given query.		
	*		
	*	@param	query the availability query		
	*		
	*	@return	the	availability status	for	each day in	the	requested period.		
	*/		
	public List<AvailabilityStatus> getAvailableRooms(AvailabilityQuery	query); 
}
```

这个服务进行可用查询，并且返回在给定时间内可用的房间。用户可以通过时间段和可选的房间类型查询可用的房间。

### 注意
这个服务的实现和其他相关类，可以在Packt出版社的网站上下载。