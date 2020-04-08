### Redis学习：

##### 简介：

1. REmote Dictionary Server(Redis)是一个用Salvatore Sanfilippo写的key-value存储系统。(key-value数据库)
2. Redis是一个开源的使用ANSI C语言编写、遵守BSD协议、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。
3. 它通常被称为**数据结构服务器**，因为值（value）可以是 **字符串(String)**, **哈希(Hash)**, **列表(list)**, **集合(sets)** 和 **有序集合(sorted sets)**等类型。

redis是完全**开源免费**的，遵守BSD协议，是一个高性能的key-value数据库

redis支持**数据的持久化**，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。

redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。

redis支持**数据的备份**，即master-slave模式的数据备份。

##### 优势：

- 性能极高 - Redis能读的速度是110000次/s，写的速度是81000次/s
- 丰富的数据类型 - Redis支持二进制案例的String，Lists，Hashes，Sets及Ordered Sets数据类型操作。
- 原子 - Redis的所有操作都是原子性的，即要么执行成功要么失败完全不执行。单个操作是原子性的，多个操作也支持事务，即原子性，通过MULT和EXEC指令包起来。
- 丰富的特性 - Redis还支持publish/subscribe，通知，key过期等特性。

##### 与其他key-value存储的不同点：

1、Redis有更加复杂的数据结构并提供对他们的原子性操作

2、Redis运行在内存但是可以持久化到硬盘

##### 安装：

1、打开cmd窗口，进入到redis路径下运行：

```cmd
redis-server.exe redis.windows.conf
```

2、出现redis的图形界面，保持该cmd窗口运行

3、另外启动一个新的cmd窗口，运行：

```cmd
redis-cli.exe -h 127.0.0.1 -p 6379
set myKey abc	//设置键值对，myKey为键，abc是值
get myKey		//根据键获取值，得到 “abc”
```



##### Redis配置：

配置文件名称redis.windows.conf，也可以通过CONFIG命令查看和设置

```cmd
//使用 GET 名称 来获取 值
redis 127.0.0.1:6379> CONFIG GET CONFIG_SETTING_NAME
//实例
redis 127.0.0.1:6379> CONFIG GET loglevel
1) "loglevel"
2) "notice"

//通过使用 * 来获取所有配置项
redis 127.0.0.1:6379> CONFIG GET *

//使用SET来修改配置
redis 127.0.0.1:6379> CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE、
//实例
redis 127.0.0.1:6379> CONFIG SET loglevel "notice"
OK
redis 127.0.0.1:6379> CONFIG GET loglevel
1) "loglevel"
2) "notice"
```



```redis
save 900 1
save 300 10
save 60 10000

```





##### Redis主从：