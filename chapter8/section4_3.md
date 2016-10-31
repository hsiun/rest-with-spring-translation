# Postman

正如我们在第五章，_REST中的CRUD操作_中简略讨论到的，我们可以借助Postman写测试用例去验证我们的RESTful服务。这种测试是有效，统一的测试。举个例子，如果我们通过REST API写个测试检查房间可用服务，我们将测试到我们系统的availability，inventory和booking部分。Postman提供定义一个测试集合的能力，如下面截图所展示的：
![Postman](http://ofboy2upv.bkt.clouddn.com/PostMan2.PNG)

我们可以调用预定的环境迅速运行整个集合，并且保证返回预期的结果。

### 注意
在免费版本中，Postman对测试没有提供完整的支持。开发着必需获取证书，才能添加它们需要的调用。