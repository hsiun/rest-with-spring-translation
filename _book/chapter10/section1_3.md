# 负载均衡

服务设计者用来支持处理集群最有用的工具是负载均衡。使用一种算法（例如，轮询或者最小连接），负载均衡器将进入的请求分发给多个后端服务器处理。下面的图说明了这种结构：

![负载均衡](http://ofboy2upv.bkt.clouddn.com/%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1.PNG)

负载均衡解决方案的范围包括从企业级商业应用，如F5的BIG-IP（<https://f5.com/products/big-ip>），到开源的软件解决方法，如HAProxy（<http://www.haproxy.org>）。