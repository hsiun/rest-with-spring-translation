# ETags

Etags提供了一个验证缓存响应的机制。它使得缓存更有效，并且极大的提高了服务响应的时间。发出响应后，服务器一般使用资源压缩的状态：
```
"ETag": "xyz123"
```

当客户端需要补发一个新的请求来获取缓存响应，这个响应中应该在`If-None-Match`头部中包含ETag：
```
"If-None-Match": "xyz123"
```

然后服务器可以将这个头部和资源的当前状态对比。如果资源改变了，服务器可以发布一个带有新资源的响应。另外，服务器也可以返回`304 Not Modified`响应。


