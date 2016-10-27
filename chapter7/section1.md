# booking服务

在我们深入如何用Spring处理安全之前，让我们先讨论下我们在这一章将会使用的资源管理系统的一部分：booking（订单）服务。

如名所示，这部分将提供我们财产管理系统中处理和管理订单的必要功能，一起看下下面Java接口：

```java
public interface BookingService {  
	/**  
	 * Looks up the booking with the given identifier.  
	 *  
	 * @param bookingId the booking identifier to look up  
	 * @return the booking with the given ID  
	 */  
	public Booking getBooking(long bookingId);
	/**  
	 * Answers all bookings for the given date range.  
	 *  
	 * @param dateRange the date range to retrieve bookings for  
	 * @return the bookings in the given date range  
	 */  
	public List<Booking> getBookings(DateRange dateRange);
	/**  
	 * Processes the given booking  
	 *  
	 * @param request the booking request  
	 * @return the result of the request  
	 */  
	 public BookingResponse book(BookingRequest request); } 
```

这个接口允许我们处理并搜索订单。假设这个接口的实现是可用的，我们现在转移我们的注意力到构建必要的RESTful端点去发布这些功能。