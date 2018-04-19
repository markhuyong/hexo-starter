---
title: redisson EVAL failed in tencent cloud
tags: 
    - redis
    - redisson
    - tencent
    - Java
categories:
    - Java
---

# when use tencent cloud `Cloud Redis Storage` not support `EVAL` command

- Log
```
2018-04-01 23:59:19 WARN  [nioEventLoopGroup-10-1] i.n.channel.DefaultChannelPipeline 151 - An exceptionCaught() event was fired, and it reached at the tail of the pipeline. It usually means the last handler in the pipeline did not handle the exception.
org.redisson.client.RedisException: ERR unknown command ' EVAL '. channel: [id: 0x126df2e7, L:/172.17.0.4:42414 - R:/172.31.48.16:6379] command: (EVAL), params: [local v = redis.call('hget', KEYS[1], ARGV[1]); redis.call('hdel', KEYS[1], ARGV[1]); return v, 1, redisson_live_object:{223030303030303030303033303030303122}:com.parkbox.domain.DeviceStatus:uniqueId..., PooledUnsafeDirectByteBuf(ridx: 0, widx: 14, cap: 256)]
    at org.redisson.client.handler.CommandDecoder.decode(CommandDecoder.java:243)
    at org.redisson.client.handler.CommandDecoder.decode(CommandDecoder.java:103)
    at io.netty.handler.codec.ByteToMessageDecoder.decodeRemovalReentryProtection(ByteToMessageDecoder.java:489)
    at io.netty.handler.codec.ReplayingDecoder.callDecode(ReplayingDecoder.java:367)
    at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:265)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:362)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:348)
    at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:340)
    at io.netty.channel.ChannelInboundHandlerAdapter.channelRead(ChannelInboundHandlerAdapter.java:86)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:362)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:348)
    at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:340)
    at io.netty.channel.ChannelInboundHandlerAdapter.channelRead(ChannelInboundHandlerAdapter.java:86)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:362)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:348)
    at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:340)
    at io.netty.channel.ChannelInboundHandlerAdapter.channelRead(ChannelInboundHandlerAdapter.java:86)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:362)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:348)
    at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:340)
    at io.netty.channel.DefaultChannelPipeline$HeadContext.channelRead(DefaultChannelPipeline.java:1359)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:362)
    at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:348)
    at io.netty.channel.DefaultChannelPipeline.fireChannelRead(DefaultChannelPipeline.java:935)
    at io.netty.channel.nio.AbstractNioByteChannel$NioByteUnsafe.read(AbstractNioByteChannel.java:134)
    at io.netty.channel.nio.NioEventLoop.processSelectedKey(NioEventLoop.java:645)
    at io.netty.channel.nio.NioEventLoop.processSelectedKeysOptimized(NioEventLoop.java:580)
    at io.netty.channel.nio.NioEventLoop.processSelectedKeys(NioEventLoop.java:497)
    at io.netty.channel.nio.NioEventLoop.run(NioEventLoop.java:459)
    at io.netty.util.concurrent.SingleThreadEventExecutor$5.run(SingleThreadEventExecutor.java:858)
    at io.netty.util.concurrent.DefaultThreadFactory$DefaultRunnableDecorator.run(DefaultThreadFactory.java:138)
    at java.lang.Thread.run(Thread.java:748)
2018-04-01 23:59:21 DEBUG [nioEventLoopGroup-10-1] c.p.protoc

```
	- [腾讯云暂时不开放redis一些脚本命令](https://cloud.tencent.com/document/product/239/4073)
	
	- [Cloud Redis Storage](https://cloud.tencent.com/product/crs)
	
	- [Redisson使用起来很方便，但是需要redis环境支持eval命令 - 沧海一滴 - 博客园](http://www.cnblogs.com/softidea/p/5973591.html)
	- [基于Redis实现分布式锁，Redisson使用及源码分析 - 文章 - 伯乐在线](http://blog.jobbole.com/99751/)

