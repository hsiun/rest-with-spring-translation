# 验证订单

我们的``类应该先验证进入系统的订单请求，然后再来处理他们。一起来添加下面的端点：

```
@RestController @RequestMapping("/bookings") 
public class BookingsResource {  
    @RequestMapping(method = RequestMethod.POST)  
    public ApiResponse book(@Valid @RequestBody BookingRequest request) {    
        BookingResponse response = bookingService.book(request);    
        return new ApiResponse(Status.OK, response);  
    } 
}
```

当POST请求发送到`/bookings/`时这个方法将会被调用。通过简单添加`@Valid`注解到这个方法，Spring将会保证进入的订单请求首先会运行通过我们定义的验证规则。

例如，使用Postman，我们可以发送如下所示POST请求：

```
{  
	"roomId":1,  
	"dateRange": {
		"from":"2017-01-01","to":"2017-01-02"},  
		"customerName":"Jane Doe",  "creditCardDetails": {    
			"cardNumber": "0111-1111-1111-1111",    
			"cardOwner": "John Doe",    
			"expiration": "01/20",    
			"cvv": "020"  
		} 
	} 
}
```

由于身份证号没有通过验证（它以0开始了），服务将响应一个*400 BadResponse*错误。