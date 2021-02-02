---
title: Docker
date: 2021-02-02 18:29:14
categories:
- Tools
- Docker
tags:
- Docker
---

## Command
![一图胜千言](https://user-gold-cdn.xitu.io/2019/4/9/16a02cdbf14142a0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## Concept
Docker 包括三个基本概念:
1. 镜像（Image）
1. 容器（Container）
1. 仓库（Repository）
理解了这三个概念，就理解了 Docker 的整个生命周期。

### [Image](https://yeasy.gitbook.io/docker_practice/basic_concept/image)
1. Docker 镜像（Image），就相当于是一个 root 文件系统
1. Docker 镜像是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。镜像不包含任何动态数据，其内容在构建之后也不会被改变。

### [Container](https://yeasy.gitbook.io/docker_practice/basic_concept/container)
1. 镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的 类 和 实例 一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。

### [Repository](https://yeasy.gitbook.io/docker_practice/basic_concept/repository)
1. `Docker Registry`: 一个集中的存储、分发镜像的服务
1. 一个 Docker Registry 中可以包含多个 仓库（Repository）；每个仓库可以包含多个 标签（Tag）；每个标签对应一个镜像。
1. 通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本。我们可以通过 `<仓库名>:<标签>` 的格式来指定具体是这个软件哪个版本的镜像。如果不给出标签，将以 latest 作为默认标签。


## 传统虚拟化与docker虚拟化
![传统虚拟化](https://gblobscdn.gitbook.com/assets%2F-M5xTVjmK7ax94c8ZQcm%2F-M5xT_hHX2g5ldlyp9nm%2F-M5xTdXNYDmRWNH-Lqez%2Fvirtualization.png?alt=media)
![docker虚拟化](https://gblobscdn.gitbook.com/assets%2F-M5xTVjmK7ax94c8ZQcm%2F-M5xT_hHX2g5ldlyp9nm%2F-M5xTdXP2scg0hxytUHA%2Fdocker.png?alt=media)

## Links
1. [从入门到实践](https://yeasy.gitbook.io/docker_practice/introduction/why)
1. [30分钟快速入门](https://juejin.im/post/5cacbfd7e51d456e8833390c)
1. [资源整理](https://juejin.cn/post/6844903450203914253)
