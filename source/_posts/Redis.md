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
get foo bar

## change dump.rdb path
config set dir /home/xxx

# save data to dump.rdb
save
```

## hiredis (just a C client; not include server)

``` shell
git clone https://github.com/redis/hiredis.git
cd hiredis
mkdir build; cd build; cmake ..; make;
sudo make install
./hiredis-test

## NOTE: sample are easier than hiredis-test
```

## redis lock using hiredis
[redislock C++ sample](https://github.com/yuhanfang/redislock)
[Redis set command(note: NX)](https://redis.io/commands/set)
