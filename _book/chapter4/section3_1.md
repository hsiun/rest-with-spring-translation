# HATEOAS

RESTful提供了一种方法用于服务器的消费者进行自我发现。让我们考虑下面对RESTful端点的响应：
```json
{
	"id": 1,
	"category": "http://myservice.com/categories/33"
}

```

这个响应包含了一个链接到资源的超文本连接，这样消费者提前预知从哪里获取资源。

对于这个方法，服务的设计者可以通过给出新的超文本连接来表明发生了改变，并且退休的旧连接也不需要服务消费者做出任何修改。这是一种强大的机制，可以帮助我们有效的管理服务变更。