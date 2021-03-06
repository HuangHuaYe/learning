# Redis

redis是单进程单线程.

## 特性

1. 速度快
2. 支持丰富的数据类型
3. 支持事务
4. 功能丰富: 缓存,消息,过期时间

## 适用场景

1. session共享
2. 缓存
3. 队列(官方不推荐)
4. 排行榜
5. 发布/订阅设计

## 数据结构

- string
- hash
- list
- set
- sortedSet
- HyperLogLog

## redis 与消息队列

不要用redis做消息队列,因为这不是redis的设计目标.

## 缓存雪崩

- redis崩掉,请求全部走到后面的数据库了: 实现高可用(主从), 设置本地缓存,redis做持久化.
- 缓存数据同时过期: 加上一个随机值在过期时间上,错开过期时间.

## 缓存穿透

- 大量的请求没有命中缓存,走后面的数据库

解决方法:

- 提前拦截
- 缓存设置空数据

## 如何做热点数据的缓存

设置淘汰策略,当内存使用到达了设置的最大区间,开始利用策略淘汰

1. volatile-lru: 从已经设计过期的数据中淘汰最少使用的
2. volatile-ttr: 从已设置过期的数据中淘汰即将过期的
3. volatile-random: 从已设置过期的数据中随机淘汰
4. allkeys-lru: 全部数据淘汰最少使用的
5. allkeys-random: 全部数据随机淘汰
6. noenviction: 禁止淘汰

## 持久化

- RDB
  默认开启,按照配置的指定时间将内存的数据快照到磁盘中.
- AOF
  每个写操作都会记录,以日志的形式记录.redis启动的时候会按照日志从头执行一遍恢复数据.

