---
title: Redis
date: 2021-01-11 21:27:34
categories:
- Program
- Database
tags:
- Redis
- Database
---

## 锁设计原则
1. 所有操作都可分为增删改查，改可用删除和增加来实现，但改更快并且具有原子性。
1. 只有获得锁才能对锁进行删和改。
1. 注意区分又状态和无状态。凡是涉及到有状态的API(lock, unlock)要特别小心。要与无状态API(圆的面积)模块区分开。
1. 系统状态尽可能的少，太多状态容易出问题。


## 基于Redis的分布式锁
1. Redis Lua脚本具有原子性

### 实现思想：
1. 获取锁的时候，使用setnx加锁，并使用expire命令为锁添加一个超时时间，超过该时间则自动释放锁，锁的value值为一个随机生成的UUID，通过此在释放锁的时候进行判断。
1. 获取锁的时候还设置一个获取的超时时间，若超过这个时间则放弃获取锁。
1. 释放锁的时候，通过UUID判断是不是该锁，若是该锁，则执行delete进行锁释放。

### 超时后又多个程序获得锁解决方法
1. 将过期时间设置足够长，确保代码逻辑在锁释放之前能够执行完成
1. `为获取锁的线程增加守护线程，为将要过期但未释放的锁增加有效时间`

### [使用守护线程特点](https://segmentfault.com/a/1190000022935064)
1. `一定要用SET key value NX PX milliseconds 命令`:如果不用，先设置了值，再设置过期时间，这个不是原子性操作，有可能在设置过期时间之前宕机，会造成死锁(key永久存在)
1. `value要具有唯一性`:这个是为了在解锁的时候，需要验证value是和加锁的一致才删除key。这是避免了一种情况：假设A获取了锁，过期时间30s，此时35s之后，锁已经自动释放了，A去释放锁，但是此时可能B获取了锁。A客户端就不能删除B的锁了。



## Redis server

``` shell
git clone https://github.com/redis/redis.git
cd redis && make
cd src
./redis-server
```

## Redis client

``` shell
./redis-cli

## cmd
set foo bar
get foo

## change dump.rdb path
config set dir /home/xxx

# save data to dump.rdb
save
```

## hiredis (just a C client; not include server)

``` shellp
git clone https://github.com/redis/hiredis.git
cd hiredis
mkdir build; cd build; cmake ..; make;
sudo make install
./hiredis-test

## NOTE: sample are easier than hiredis-test
```

## Links
1. [redis lock华为漫画](https://bbs.huaweicloud.com/blogs/209955)
1. [Zookeeper 华为漫画](https://bbs.huaweicloud.com/blogs/209954)
1. [redis实现分布式锁](https://blog.csdn.net/xlgen157387/article/details/79036337)
1. [小米解决方案](https://xiaomi-info.github.io/2019/12/17/redis-distributed-lock/)
1. [redis分布式锁](https://juejin.cn/post/6844903830442737671)
1. [redislock C++ sample](https://github.com/yuhanfang/redislock)
1. [Redis set command(note: NX)](https://redis.io/commands/set)
1. [Redisson](https://github.com/redisson/redisson)
