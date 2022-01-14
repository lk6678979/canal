# canal比较
## 安装
https://github.com/alibaba/canal/wiki/QuickStart
### 设计理念
canal-admin的核心模型主要有：  

1. instance，对应canal-server里的instance：一个最小的订阅mysql的队列  
2. server，对应canal-server，一个server里可以包含多个instance  
3. 集群，对应一组canal-server，组合在一起面向高可用HA的运维  
简单解释：  
1. instance因为是最原始的业务订阅诉求，它会和 server/集群 这两个面向资源服务属性的进行关联，比如instance A绑定到server A上或者集群 A上，
2. 有了任务和资源的绑定关系后，对应的资源服务就会接收到这个任务配置，在对应的资源上动态加载instance，并提供服务
  * 动态加载的过程，有点类似于之前的autoScan机制，只不过基于canal-admin之后可就以变为远程的web操作，而不需要在机器上运维配置文件  
2. 将server抽象成资源之后，原本canal-server运行所需要的canal.properties/instance.properties配置文件就需要在web ui上进行统一运维，每个server只需要以最基本的启动配置 (比如知道一下canal-admin的manager地址，以及访问配置的账号、密码即可)
