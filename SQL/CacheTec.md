# 缓存工具

## [Redis](https://blog.csdn.net/hjm4702192/article/details/80518856)

redis数据类型:
- string
- hash: 存放的是结构化的对象
- list: 可以做简单的消息队列的功能; 可以利用lrange命令,做基于redis的分页功能,性能极佳,用户体验好
- set: set堆放的是一堆不重复值的集合, 所以可以做全局去重的功能
- sorted set: 多了一个权重参数score, 集合中的元素能够按score进行排列

redis 的过期策略以及内存淘汰机制:
- redis 采用的是定期删除 + 惰性删除策略
    - redis默认每隔100ms检查, 是否有过期的key, 有过期key则删除. redis不是将所有的key检查一次, 
    而是随机抽取进行检查(如果全部key进行检查, redis岂不是卡死). 因此只采用定期删除策略, 
    会导致很多key到时间没有删除.
    - 惰性删除派上用场, 在你获取某个key的时候, redis会检查一下, 如果过期了此时就会删除.
    
redis当物理内存用完时, 会将一些很久没用到的value交换到磁盘中去.

redis支持数据备份(master-slave模式备份)
    
## [Memcache](https://blog.csdn.net/kangvcar/article/details/78591899)

- memcache可以用来缓存图片、视频等. 只支持K/V存储.
- memcache挂掉后, 数据直接丢失了, 而redis会定期持久化数据至磁盘中
- 过期策略: memcache在set时就指定,例如set key1 0 0 8,即永不过期.
Redis可以通过例如expire 设定,例如expire name 10.


Redis除做NoSQL数据库外, 还可做消息队列、数据堆栈和数据缓存等, Memcached适合于缓存SQL语句、数据集、
用户临时性数据、延迟查询数据和session等.


## 杂谈  

- [python redis操作](https://www.jianshu.com/p/2639549bedc8)
- [redis和memcached区别](https://blog.csdn.net/hackercn9/article/details/54846048)
