# 通过Maven启动服务

另外一个在开发时启动Web服务（没有IDE）的方法是通过使用Jetty Maven插件。下面的POM节选展示了必要的配置：
```xml
<build>	
	<plugins>				
		...				
		<plugin>						
			<groupId>org.mortbay.jetty</groupId>						
			<artifactId>jetty-maven-plugin</artifactId>						
			<configuration>								
				<useTestScope>true</useTestScope>								
				<stopPort>8005</stopPort>								
				<stopKey>DIE!</stopKey>								
				<systemProperties>										
					<systemProperty>												
						<name>jetty.port</name>												
						<value>8080</value>										
					</systemProperty>								
				</systemProperties>						
			</configuration>				
		</plugin>		
	</plugins> 
</build>
```
当这个插件被添加到POM文件中后，现在可以通过运行下面的命令启动服务了：

```
mvn jetty:start
```

之后服务可以通过http://localhost:8080 访问。

注意这一点，当服务处于运行中时，这个应用不会暴露出任何的端点，下一章我们将学校如何创建一个RESTful端点，但是现在，开发者可以创建下满的控制器用于快熟测试本服务：
```java
import	org.springframework.web.bind.annotation.*;
@RestController 
public	class	HelloWorldResource	{
	@RequestMapping(method	=	RequestMethod.GET)				
	public	String	helloWorld(){								
		return	"Hello,	world!";				
	} 
}
```

一旦控制器就位，访问http://localhost:8080 将会展示下面内容：
```
Hello, world!
```