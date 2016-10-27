# Gradle的依赖管理

Gradle提供了依赖解决方案。它可以被设置为使用Maven的中央仓库。让我们一起考虑一个简单的构建（在一个叫build.gradle的文件中）：
```
apply plugin: 'java'

repositories {
	mavenCentral()
}
```

我们指示Gradle，我们将要构建一个Java项目，并且依赖项可以从Maven的中央仓库获取。现在我们可以把需要的依赖项简单的声明成下面这样：
```
dependencies {
	runtime group: 'org.hibernate', name: 'hibernate-core', version: '4.1.9.Final'
	testCompile group: 'junit', name: 'junit', version '4.+'
}
```

上面这个Gradle构建文件声明了两个依赖项：

* Hibernate：这是一个运行时依赖，将会被用于整个项目编译期间，并且将会打包进应用
* JUnit：这个依赖项将会被添加到classpath中，并且会被用于整个项目运行测试的时候。这种类型的依赖项不会打包进最终项目。


### 技巧
#### 下载示例代码
你可以通过你的账号在<http://www.packtpub.com>下载所有购买的Packt出版图书的代码。无论你在哪里购买的本书，你都可以访问<http://www.packtpub.com/support>，包含文件下载地址的电子邮件将直接发给你。

### 技巧
添加下面内容到构建文件，就可以使用远程Maven仓库了：
```
repositories {
	maven {
		url "http://repo.mycompany.com"
	}
}
```

Maven和Gradle对构建我们的简单RESTful服务都提供了很好的支持，并且所有的构建脚本可以和本书的代码一起下载。现在，让我们将注意力转移到我们属性管理系统的结构。