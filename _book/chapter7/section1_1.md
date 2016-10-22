# REST资源

正如我们在第三章，_使用Maven和Gradle构建RESTful Web服务_中所看到的，我们可以通过使用下面代码，暴露通过ID检索订单的功能：

```java
@RestController 
@RequestMapping("/bookings") 
public class BookingsResource {
    @Autowired  
    private BookingService bookingService;

    @RequestMapping(value = "/{bookingId}", method = RequestMethod.GET)  
    public BookingDTO getBooking(@PathVariable("bookingId") long bookingId) {    
        return new BookingDTO(bookingService.getBooking(bookingId));  
    } 
}
```

在下面部分，我们将学习如何将安全运用到这些端点。