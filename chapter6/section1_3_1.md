### Spring Boot

如果Web服务使用Spring Boot并且运行在Tomcat或者Jetty中，支持gzip压缩可以通过在`application.properties`中添加下面两条属性来实现。

```
server.compression.enabled=true 
server.compression.mime-types=application/json
```

这个属性样板打开了压缩选项，这样稍后应用到JSON正文的压缩就有保证了。

### 技巧
将gzip压缩应用到没有压缩的内容时它工作最好。确实，将gzip压缩应用到已经压缩的内容，如图片，数据大小可能不太会减少，而且浪费CPU周期。
