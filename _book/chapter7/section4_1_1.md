# 正则表达式

另外一个非常有用的验证注解是`@javax.validation.constraints.Pattern`。这个注解允许基于正则表达式来验证域。举个例子，让我们一起看下`CreditCardDetails`类：

```Java
public class CreditCardDetails {  
	@NotNull  
	private String cardOwner;  

	@Pattern(regexp = "\\b(?:4[0-9]{12}(?:[0-9]{3})?|" +          
			"5[12345][0-9]{14}|3[47][0-9]{13}|" +          
			"3(?:0[012345]|[68][0-9])[0-9]{11}|" +          
			"6(?:011|5[0-9]{2})[0-9]{12}|" +          
			"(?:2131|1800|35[0-9]{3})[0-9]{11})\\b")  
	private String cardNumber;  

	@Pattern(regexp = "[0-9]{2}/[0-9]{2}")  
	private String expiration;  

	@Pattern(regexp = "[0-9]{3,4}")  
	private String cvv; 
} 
```

我们使用验证注解声明这个类中的每个域。例如，cvv号是通过正则表达式来监测值是否是3或4个数字。


### 技巧
在拥有大量请求的系统中，使用正则表达式进行输入验证也许会增加不想要的延迟。因此，服务的设计者在使正则表达式的时候应该权衡利弊。
