# 第二层缓存

第二层缓存是可选且完全可配置的。这种缓存策略能够定义每一个实体和多个提供者被额外支持的。

* *Ehcache*(<http://www.ehcache.org/>)：这是一个开源的Java缓存，支持在内存和磁盘上缓存数据。Ehcache可以被设置为分布式缓存。它是Hibernate第二层缓存一个非常流行的选择。

* *OSCache*(<https://java.net/projects/oscache>)：这是一个鲜为人知的Java缓存框架。这个框架不在继续开发，列在这里是为了完整。

* *JBoss Cache*(<http://jbosscache.jboss.org>)：这个缓存框架的目标是提供一个企业级的集群解决方案。它基于JGroups组播库。他是完全事务和集群的。
