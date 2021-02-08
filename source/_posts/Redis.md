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

## 基于Redis的分布式锁
1. Redis Lua脚本具有原子性

### 实现思想：
1. 获取锁的时候，使用setnx加锁，并使用expire命令为锁添加一个超时时间，超过该时间则自动释放锁，锁的value值为一个随机生成的UUID，通过此在释放锁的时候进行判断。
1. 获取锁的时候还设置一个获取的超时时间，若超过这个时间则放弃获取锁。
1. 释放锁的时候，通过UUID判断是不是该锁，若是该锁，则执行delete进行锁释放。



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

## redis lock using hiredis
1. [redis实现分布式锁](https://blog.csdn.net/xlgen157387/article/details/79036337)
1. [redis分布式锁](https://juejin.cn/post/6844903830442737671)
1. [redislock C++ sample](https://github.com/yuhanfang/redislock)
1. [Redis set command(note: NX)](https://redis.io/commands/set)
