# 让服务执行起来

对于Maven和Gradle，可以将服务打包为WAR格式。然而，为了在开发期间快速启动和调试的应用，我们将实现一个可执行Java类。借助Spring Boot，这是很容易通过下面类代码实现的：
```
package com.packtpub.restspring.app;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class WebApplication {
	
	public static void main(String[] args) {
		SpringApplication.run(WebApplication.class, args);
	}
}
```
这个类通过搜索所有的web部分并加载他们来启动我们的应用。

### 技巧
添加如下Maven依赖来访问`org.springframework.boot.SpringApplication`:

```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
	<version>1.2.3.RELEASE</version>
</dependency>
```

Spring Boot的好处在于，它不需要设置和配置。一旦这个类被执行，借助内置的Tomcat，服务将可以通过8080端口访问。

### 注意
Spring Boot的信息可以在<http://projects.spring.io/spring-boot/>找到。
