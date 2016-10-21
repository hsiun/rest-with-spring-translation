# 基础设置

客户端库应该是自包含并且可移植的，这样RESTful Web服务的消费者才可能使用它们。假设在服务端和客户侧共享代码。如果这样做，将会使得客户端可服务端代码紧耦合且阻碍客户端库的移植性。

在我们简答属性管理服务的实际情况中，我们将把客户端库作为一个新的Maven模块来构建。这个模块需要以下依赖：

```XML
<dependency>		
	<groupId>org.springframework</groupId>		
	<artifactId>spring-web</artifactId>		
	<version>4.1.6.RELEASE</version> 
</dependency> 
<dependency>		
	<groupId>commons-logging</groupId>		
	<artifactId>commons-logging</artifactId>		
	<version>1.1.3</version> 
</dependency> 
<dependency>		
	<groupId>com.fasterxml.jackson.core</groupId>		
	<artifactId>jackson-databind</artifactId>		
	<version>2.3.2</version>
</dependency>
```

使用Spring构建RESTful客户端，我们最少需要Spring的Web模块。另外，Spring运行时需要Apache `commons-logging`库。最后，我们将借助Jackson实现客户端Java类和服务端JSON表示之间数据的绑定。
