# RESTful Web服务中的gzip压缩

现在我们知道gzip是HTTP压缩更广泛的选择，我们将在我们的RESTful Web服务中支持gzip压缩，让我们一起看下如何实现。

处理压缩一般会下降到servlet来处理（举个例子，Tomcat，Jetty，JBoss，等）。你可以参考这些容器的文档来了解他们支持压缩的细节。

