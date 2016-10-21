# Availability和booking服务

让我们一起看下我们简单属性管理系统的Availability和Booking部分。Availability模块是依赖Booking服务的。为了处理这些，我们为Booking服务定义了一个简单的客户接口，如下所示：

```Java
public interface BookingServiceClient {
    /**     
    * Looks up the booking with the given identifier.     *     
    * @param bookingId the booking identifier to look up     *     
    * @return the booking with the given ID     */    
    public Booking getBooking(long bookingId); 
}
```

这个客户单接口只定义了一个方法，通过ID查找订单。我们首先的部署方法是让两部分运行在单独的JVM上。因此，我们实现了一个可以操作Availability服务的远程客户端：

```Java
public class RemoteBookingServiceClient implements BookingServiceClient {
	private final String serviceUrl;  
	private final RestTemplate template;
	public RemoteBookingServiceClient(String serviceUrl) {    
	if (serviceUrl == null) {      
		throw new IllegalArgumentException("serviceUrl cannot be null");    
	}    
	this.serviceUrl = serviceUrl;    
	template = new RestTemplate();  }
	@Override  
	public Booking getBooking(long bookingId) {    
	//omitted to clarity    
	return (Booking) ResponseHandler.handle(      
		() -> template.exchange(serviceUrl + "/bookings/" + bookingId, HttpMethod.GET, null, typeReference).getBody());  
	} 
}
```

在这一章的前部分，我们教导如何使用`org.springframework.web.client.RestTemplate`去远程调用服务。现在，为了减少延迟，我们决定将两个模块运行在同一个JVM上。使用这样的客户端实现将取消将两个服务部署在同一个进程上所有好处。因此，我们需要一个新的实现：

```Java
public class LocalBookingServiceClient implements BookingServiceClient {
	@Autowired
	private BookingService bookingService;
	@Override  
	public Booking getBooking(long bookingId) {    
		com.packtpub.springrest.model.Booking booking = bookingService.getBooking(bookingId);    
		Booking clientBooking = new Booking();    
		clientBooking.setId(booking.getId());    
		// omitted setting other fields for clarity    
		return clientBooking;  
	} 
}
```

对于这个新的实现，我们简单授权给订单系统通过任何网络遍历真实服务。然后服务端需要传递数据给客户端。
