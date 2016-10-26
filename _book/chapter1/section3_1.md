# 架构

我们的属性管理系统将被组织成四部分，如下图所示：

![架构图](http://ofboy2upv.bkt.clouddn.com/%E6%9E%B6%E6%9E%84%E5%9B%BE.PNG)

下面对这四部分进行了解释：
* Inventory服务：这个部分提供必要的功能区管理和描述房间和房间类型。

* Availability服务：这部分让用户知道在特定的时间内那些房间是可预订的。

* Booking服务：这部分将主要负责处理订单。它将会依赖Inventor服务和Availability服务来验证订单。

* Billing服务：一旦订单产生，这部分将提供能力生成单据。

