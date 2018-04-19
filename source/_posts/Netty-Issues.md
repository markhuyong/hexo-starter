---
title: Netty Issues
date: 2018-04-02 14:05:36
tags:
	- netty
	- Java
	- bug

categories:
	- Java
---

# too Many duplicated TCP links

```
root@production-watchdog:~# netstat -an|grep 65003| sort -n | uniq -c
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:11547   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:16857   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:19251   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:21405   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:22151   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:24348   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:25293   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:31504   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:33963   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:37082   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:37454   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:38615   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:40626   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:42882   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:45746   ESTABLISHED
      1 tcp6       0      0 10.10.10.10:65003      11.11.11.11:48254   ESTABLISHED
```
如果存在以下情况，主板断电、重启、弱网环境等，主板无法主动正确关闭已经建立的SOCKET连接，导致服务端出现冗余的连接。
主板断电后再上电，旧的连接已经失效，但是会由于未正确关闭，而发生冗余：


# Netty ByteBuf leak

- [Netty.docs: Reference counted objects](http://netty.io/wiki/reference-counted-objects.html)
