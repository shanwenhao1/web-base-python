### [Tornado](http://www.nowamagic.net/academy/part/13/325/)

Tornado采用 多进程 + 非阻塞 + epoll模型, 属于非阻塞式服务器.
- [epoll](http://www.nowamagic.net/academy/detail/13321005)基于事件的方式实现并发.

三个基本模块: 
- 为了实现高并发和高性能, 使用了一个IOLoop来处理socket的读写事件, IOLoop基于epoll, 可以高效的响应网络事件.
- 实现了IOStream类, 用来处理socket的异步读写.
- HTTPConnection类处理http的请求

Tornado不仅仅是一个Web框架, 它还完整地实现了HTTP服务器和客户端, 可分为四层:
- 最底层的EVENT层处理IO事件
- TCP层实现了TCP服务器, 负责数据传输
- HTTP/HTTPS层基于HTTP协议实现了HTTP服务器和客户端
- 最上层为Web框架, 包含了处理器、模板、数据库连接、认证、本地化等等Web框架需要具备的功能.