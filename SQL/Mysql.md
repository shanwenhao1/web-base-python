# Mysql

## [innodb](http://www.cnblogs.com/Aiapple/p/5689634.html)

特点:
- 根据主键寻址速度很快
- 主键值递增的insert插入效率较好
- 主键随机insert插入操作效率差
- 因此, innodb表必须指定主键, 建议使用自增数字

innodb数据块缓存池
- 数据的读写需要经过缓存(缓存在buffer pool即在内存中)
- 数据以整页(16k)为单位读取到缓存中
- 缓存中的数据以LRU策略换出(最少使用策略)
- IO效率高, 性能好.

innodb数据持久化与事务日志
- 事务日志实时持久化
- 内存变化数据(脏数据)增量异步刷出到磁盘
- 实例故障靠重放日志恢复
- 性能好, 可靠, 恢复快

innodb关键特性
- 插入缓冲
- 两次写
- 自适应哈希索引, [B-Tree索引与哈希索引](https://www.cnblogs.com/yimixiong/p/7401527.html)
- 异步io
- 刷新邻接页