# RabbitMQ

由于 TCP 连接的创建和销毁开销较大，且并发数受系统资源限制，会造成性能瓶颈。RabbitMQ 使用信道的方式来传输数据。信道是建立在真实的 TCP 连接内的虚拟连接，且每条 TCP 连接上的信道数量没有限制。

## 应用场景

1. 跨系统异步通信
2. 多个应用之间解藕
3. 应用内的同步转化
4. 请求削峰

## 消息队列原理

- 生产者: 消息的创建者,负责创建和推送数据到消息服务
- 消费者: 消息的接收方,处理消息服务推送的消息
- 代理: 快递员的角色(RabbitMQ)

## RabbitMQ重要的组件

- ConnectionFactory（连接管理器）：应用程序与Rabbit之间建立连接的管理器，程序代码中使用。
- Channel（信道）：消息推送使用的通道。
- Exchange（交换器）：用于接受、分配消息。
- Queue（队列）：用于存储生产者的消息。
- RoutingKey（路由键）：用于把生成者的数据分配到交换器上。
- BindingKey（绑定键）：用于把交换器的消息绑定到队列上

## vhost

类似于rabbitMQ的子服务,拥有独立的exchange,queue,bingding等.可以看作是一个系统下的不同用户

## 可靠性

1. 消息持久化
2. ACK确认机制
3. 集群尽享
4. 消息补偿

## 持久化

优点:
大大提高可靠性
缺点:
降低吞吐量

## 广播模式(exchange类型)

1. fanout,所有bind到对应exchange的queue都可以接受到消息
2. direct: 通过routingKey和exchange决定唯一的queue
3. topic: 所有符合routingKey所bind的queue都可以接收到消息

## 节点

- 磁盘节点
- 内存节点