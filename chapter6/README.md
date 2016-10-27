# 第六章 性能

为了部署RESTful Web服务到商业环境，必须达到一些条件。要求之一就是性能。除了获得正确的结果，RESTful端点还必须在合适的时间内做到这样。本章讨论，这些概念在真实Web服务中是如何体现出来的。性能优化技术可以运用到Web服务的不同层。然而，在这一章，我们将重点关注RESTful(Web)层。第十章，_扩展你的RESTful Web服务_，探索了应用在Web应用其他层的优化技术。下面的话题将覆盖接下来的几页：

* 使用HTTP压缩
* 使用+HTTP Cache-Control+指令
* 使用+Etag+头部
* 使用HTTP Last-Modified/If-Modified-Since头部

为了展示这些技术，我们将编写我们简单属性管理Web服务系统的房间Availability部分。