# 服务模块解析

随着全部项目结构的定义，现在我们可以专注于每个模块的声明（这里以booking模块示例）。

一些服务模块对其他服务模块有运行时依赖。举个例子，billing依靠定义在booking中的订单服务。

非常赞的是，Maven支持将一个模块打包成WAR（Web Application Archive）。然而，它并不会将代码表示成一个artifact。要这样做，我们的服务模块必须包含如下配置：

```
<project>
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>com.packtpub.rest-with-spring</groupId>
		<artifactId>rest-with-spring</artifactId>
		<version>1.0.0-SNAPSHOT</version>
		
	</parent>	
	<artifactId>rest-with-spring-billing</artifactId>
	<packaging>war</packaging>

	<build>
		<plugins>
		<plugin>
			<artifactId></artifactId>
			<version>2.6</version>
			<configuration>
				<arttachClasses>true</arttachClasses>
			</configuration>
		</plugin>
		</plugins>
	</build>
</project>
```

插件的作用是将构建WAR文件的Java代码作为单独的artifact，这样就可以到处引用他了。下面的代码片段展示了如何引用这个artifact：
```
<dependency>
	<groupId>com.packtpub.rest-with-spring</groupId>
	<artifactId>rest-with-spring-billing</artifactId>
	<version>1.0.0-SNAPSHOT</version>
	<classifier>classes<classifier>
</dependency>
```

除了'classifier'这是一个非常简单标准的依赖声明，用来将Java代码引入服务。

