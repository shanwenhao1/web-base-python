# 服务端完整项目示例

客户端通过连接池([Http持久连接](https://www.cnblogs.com/kingszelda/p/8988505.html), 复用连接, 节省资源)请求服务器
<br>─分布式服务器集群通过[http报文解析](https://blog.csdn.net/chf1142152101/article/details/74162755): 
获取用户区服信息和id 及所请求的接口对应的ID(每个方法对应的ID唯一), json格式
<br>─根据客户端请求参数, 编写对应的函数进行处理(涉及到redis及sql数据查询及更新), 
以及rpc或http调用拆分后的微服务(比如聊天、行为日志等), 所有的服务中都会运用TraceID进行跟踪(有的需要sessionID)
<br>─服务端处理完成后会将结果封装成json字符串格式返回给客户端.


## 所使用的技术的机制

### HTTP持久化策略

HTTP/1.1的连接默认情况下都是持久连接.如果要显式关闭,需要在报文中加上Connection:Close首部.
即在HTTP/1.1中,所有的连接都进行了复用

HttpClien中使用了连接池来管理持有连接,同一条TCP链路上,连接是可以复用的.HttpClient通过连接池的方式进行连接持久化.
<br>其实“池”技术是一种通用的设计,其设计思想并不复杂:</br>
- 当有连接第一次使用的时候建立连接
- 结束时对应连接不关闭,归还到池中
- 下次同个目的的连接可从池中获取一个可用连接
- 定期清理过期连接

客户端如何清理过期连接: HttpClient中会有一个单独的线程来扫描连接池中的连接, 
发现有离最近一次使用超过设置的时间后,就会清理.