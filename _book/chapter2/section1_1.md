# Apache Maven的依赖管理

依赖管理是一种让开发更简单的构建特征。它减少了手动下载第三方库的需要，并且将他们打包进应用。Maven有一个基于artifact仓库健壮的依赖管理系统。

### 技巧 ###
Maven的主仓库被称之为中央仓库，可以在<http://maven.org>搜索到。

为了声明依赖，前面章节展示的简单POM文件可以修改成下面格式：
```
// 为了方便阅读，省略上面的内容
	<version>1.0.0-SNAPSHOT</version>
	<packaging>war</packaging>
	<dependencies>
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hiberante-core</artifactId>
			<version>4.1.9.Final</version>
		</dependency>

		<!-- 用于测试的依赖项 -->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.11</version>
			<scope>test</scope>
		</dependency>
	</dependencies>

</project>
```

在修正版POM文件的<dependencies>标签中声明了两个依赖项：

* **Hibernate**：这是一个标准依赖，在编译项目之前Maven将会自动下载它。

* **JUnit**：对于这个依赖，Maven会改变用来编译和执行单元测试的类路径。

另一个非常受欢迎的构建工具是Gradle，将会在下一节讨论Gradle。