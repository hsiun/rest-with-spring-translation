# 快速测试端点

在第八章，_测试RESTful Web服务_将比较全面的覆盖如何有效的测试一个REST Web服务，但是为了快速测试我们新创建的端点。一起看下如何用Postman测试我们能创建新的房间。

### 注意
Postman是一个提供构建和测试Web Api的工具，他是一个Google Chrome插件。

下面的截图展示了Postman是怎样被用于测试这个端点的：

![Postman发送请求](http://ofboy2upv.bkt.clouddn.com/PostMan.PNG)

在Postman中，我们将内容的头部(application/json)和请求体发送POST请求到URL(<http://localhost:8080/rooms>)。发送这个请求将创建新房间并返回。

![结果](http://ofboy2upv.bkt.clouddn.com/%E7%BB%93%E6%9E%9C.PNG)