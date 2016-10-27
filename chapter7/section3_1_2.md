# 资源注解

不想集中配置，非常类似在前面某部分讨论的，可以通过注解在在资源类中直接控制资源访问。Spring使用`org.springframework.security.access.prepost.PreAuthorize`提供了一个基于表达式的访问控制机制。
让我们一起修改下在这章开头描述过的那个端点：

```
@RestController 
@RequestMapping("/bookings") 
public class BookingsResource {
	@PreAuthorize("hasRole('ROLE_ADMIN')")  
	@RequestMapping(value = "/{bookingId}", method = RequestMethod.GET)    
	public BookingDTO getBooking(@PathVariable("bookingId") long bookingId) {    
		// omitted  
	} 
} 
```

在我们端点中添加`@PreAuthorize("hasRole('ADMIN')")`声明来指示Spring Security只授权给管理员访问这个资源。如果用户尝试调用这个端点，服务将会返回一个`403 Forbidden`响应。


### 技巧
如果资源需要被多个角色访问，可以使用下面的表达式：
```
hasAnyRole('role1, role2')
```

现在让我们把注意力转移到安全的其他也扮演着非常重要角色方面：输入验证。下一节探讨如何使用Spring实现输入验证。