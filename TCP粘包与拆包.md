# 拆包

TCP将完整的包拆分成多个包进行发送

# 粘包

将多个小的包封装成一个大的数据包发送

# 原因

1.应用程序write写入的字节大小大于套接口发送缓冲区的大小

2.进行MSS大小的TCP分段

3.以太网帧的paylo大于MTU进行IP分片


# 解决方法

1.消息定长

2.包尾增加回车换行符进行分割

3.将消息分为消息头和消息体，

4.更负责的应用层协议

## Netty方法

### LineBasedFrameDecoder

一次便利ByteBuf中的可读字节，判断是否有“\n”或者“\r\n”,有，就以此位置结束。

以换行符为结束标志的解码器，支持携带结束符或不懈怠结束符两种解码方式，支持配置单行的最大长度。

### StringDecoder

将接收到的对象装换为字符创，然后接续调用后面的Handler。

### DelimiterBasedFrameDecoder

自动完成以分隔符作为码流结束标识的消息和解码

~~~bash
ByteBuf delimiter = Unpooled.copiedBuffer("$_"
  .getBytes());
ch.pipeline.addLast(
  new DelimiterBasedFrameDecoder(1024,
      delimiter)):
~~~
1.创建分隔符缓冲对象ByteBuf；

2.创建DelimiterBasedFrameDecoder对象，1024标识单条消息的最大长度，如果达到最大长度后没有找到分隔符，则抛出TooLongFrameException；第二个参数为分隔符缓冲对象

3.将其加入到ChannelPipeline；

### FixedLengthFrameDecoder

固定长度解码器，按照指定的长度对消息解码，无需考虑TCP的粘包/拆包问题










