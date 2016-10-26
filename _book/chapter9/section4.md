# 异常处理

第三章，_第一个端点_，接触到了定义一个包含错误代码和错误描述的固定响应格式。推测客户端会定义一个异常来封装调用失败的原因。我们可以这样做，因此，定义了下面的异常类：


```
public class ClientException extends RuntimeException {
    private final int errorCode;  
    private final String errorDescription;
    public ClientException(ApiError error) {    
        super(error.getErrorCode() + ": " + error.getDescription());    this.errorCode = error.getErrorCode();    
        this.errorDescription = error.getDescription();  
    }

    public int getErrorCode() {    
        return errorCode;  
    }
    public String getErrorDescription() {    
        return errorDescription; 
    } 
} 
```

消费RESTful Web服务的客户端使用这个异常处理将会有一个持久的方式来管理和报告错误。然而，在少数几个情况下通用的异常处理要求在客户端做更多工作。举个例子，服务器也许会生成一个特殊的错误，当它不能处理当前请求，并要求客户端推迟几秒后重新发布它们的请求。

在这种情况下，如果它们能捕获这个特殊的异常而不是缺省处理这类问题，这将会使得服务消费者的工作更容易。客户端实现应该声明继承自`ClientExceptio`调用，例如，`ServerOverloadedClientException`，并抛出异常代替这一类相关地方。


细心的读者也许注意到了，我们声明`ClientException`为一个不检查的异常。这给我们能力在不暴露异常的情况下去管理我们的异常处理。

### 注意

选择使用被检查的还是不被检查的异常通常时个人喜好，而不是技术动机。要求在客户端库的每个方法中捕获异常是有好处的而不是笨重的。想到的，不捕获异常也许会导致消费者无法处理它们本应该能处理的错误情况，