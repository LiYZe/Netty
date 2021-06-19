# BIO

一个独立的Acceptor线程监听客户端连接，收到客户端连接请求后为每个客户端创建新的线程进行链路处理，完成后，通过输出流返回应答给客户端，销毁线程。

<div align = "center"> <img src = "https://user-images.githubusercontent.com/37955886/122642776-a87eec80-d13e-11eb-807b-012dfdc9a36d.png"/></div>

## 缺点

缺乏弹性伸缩能力

# 伪异步I/O编程

后端通过线程池处理多个客户端打的请求接入。

<div align = "center"> <img src = "https://user-images.githubusercontent.com/37955886/122642826-f693f000-d13e-11eb-87af-3193ca927bd5.png"/></div>

# NIO

提供了SocketChannel和ServerSocketChannel两种套接字通道实现。均支持阻塞和非阻塞

## 缓冲区Buffer

对象，包含写入或者独处的数据。本质为数组，还提供了对数据的结构化访问和维护读写位置等信息。

NIO库中所有数据都用缓冲区处理

## 通道Channel

网络数据通过Channel读取和写入。双向，全双工。

可分为两大类：网络读写SelectableChannel；文件操作FileChannel

## 多路复用Selector

不断轮询注册在其上的Channel，如果某个Channel上游读或写时间，则Channel处于就绪状态，Selector会轮询出来，送过SelectionKey获取就绪Channel集合，进行后续的I/O操作。

## 服务端

<div align = "center"> <img src = "https://user-images.githubusercontent.com/37955886/122643111-86866980-d140-11eb-816c-476efe359162.png"/></div>

## 客户端

<div align = "center"> <img src = "https://user-images.githubusercontent.com/37955886/122643133-ac137300-d140-11eb-82f7-b5515b0fe27b.png"/></div>

# AIO

提供异步文件通道和异步套接字通道实现。

获取操作结果：通过java.util.concurrent.Future类表示异步操作的结果；在执行异步操作的时候传入一个java.nio.channels.

CompletionHandler接口的实现类作为操作完成的回调。


