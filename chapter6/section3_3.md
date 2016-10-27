# 添加HTTP缓存

正如在这章开头讨论的，对HTTP有几种可以使用的缓存方法。在这一节，我们使用`Last-Modified/If-Modified-Since`头部来避免通过线缆发送不必要的数据。为了这样做，我们需要访问HTTP响应。动手来修改我们的端点吧：

```java
@RequestMapping(method = RequestMethod.GET) 
public ApiResponse getAvailability(  
	@RequestParam("from") 
	String from,  
	@RequestParam("until") 
	String until,  
	@RequestParam(value = "roomCategoryId", required = false) 
	String categoryId, WebRequest request) {  
	// omitted 
}
```

Spring将映射新的属性到`org.springframework.web.context.request.WebRequest`对象，这个对象代表一个请求。

下一步是计算出捕获当前响应状态的时间。在我们这里，我们可以使用订单的更新日期，这是最近在请求时间里更新的。

然后，在我们端点的方法体内，我们可以借助Spring对缓存的支持，这一点如下所示：

```Java
AvailabilityQuery query = new AvailabilityQuery(dateRange, categoryId); 
// we use the last updated booking date as our Last Modified value 
Date lastUpdatedBooking = getLastModified(query); 
if (request.checkNotModified(lastUpdatedBooking.getTime())) {    
	return null; 
} 
// perform the query and return the availability status
```

对于`WebRequest.checkNotModified()`的使用，我们用来比较`If-Modified-Since`请求头部的值和我们计算的值。如果这个值相匹配，我们不需要处理这个请求，且Spring将会返回一个304响应。另外，我们可以执行并处理Availability请求，并且包括我们生成的`Last-Modified`报文头。

### 注意

调用`WebRequest.checkNotModified()`将保证响应相关HTTP报文头被设置。因此，如果数据没有改变，不用进一步处理请求，且开发者可以安全的返回`null`，替代手动构建304响应。

例如，新的用户第一次请求Availability，服务器将以下面的报文头来响应：

```
HTTP/1.1 200 OK 
Server: Apache-Coyote/1.1 
Last-Modified: Sun, 14 Jun 2015 22:00:00 GMT 
Content-Type: application/json;charset=UTF-8
Transfer-Encoding: chunked 
Date: Mon, 15 Jun 2015 12:12:32 GMT
```

重新发布同样的请求，用户浏览器将包括下面报文头:

```
GET /availability?from=2016-12-01&until=2016-12-01 HTTP/1.1 
// omitted 
If-Modified-Since: Sun, 14 Jun 2015 22:00:00 GMT
```

接下来服务器将会比较请求提供的时间戳和我们的最后修改日期，并发起一个304响应：

```
HTTP/1.1 304 Not Modified 
Server: Apache-Coyote/1.1 
Date: Mon, 15 Jun 2015 12:16:03 GMT
```

这个方法同时处理服务器减少请求的数量（假设生成最后修改日期的花费小于处理请求）和服务器发送数据总量，其结果是提升了性能。