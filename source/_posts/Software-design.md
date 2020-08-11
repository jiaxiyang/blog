---
title: Software design
date: 2020-08-03 09:31:41
categories:
- Program
- Design
tags:
- Design
---

## System Architecture


## Design Patterns
### 原则
1. `开闭原则` 软件中的对象（类，模块，函数等等）应该对于扩展是开放的，但是对于修改是封闭的
1. `单一职责原则` 一个类只做一件事
1. `里氏替换原则` 子类应该可以完全替代父类，也就是说在使用继承时，只扩展新功能，不要破坏父类原有的功能。
1. `依赖倒置原则` 细节应该依赖与抽象，抽象不应该依赖于细节。把抽象层放在程序设计的高层，并保持稳定，程序的细节变化由低层的实现层来完成。
1. `迪米特法则/最少知道原则` 一个类不应该知道自己操作类的细节，换言之，只和朋友谈话，不和朋友的朋友谈话。
1. `接口隔离原则` 客户端不应该依赖它不需要的接口。如果一个接口在实现时，部分方法由于冗余被客户端空实现，则应该将该接口拆分，让实现类只依赖自己需要的接口。

### 工厂模式
### 单例模式


## Software Design



## Links
1. [程序设计语言分类](https://zh.wikipedia.org/wiki/Template:%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E8%AF%AD%E8%A8%80)
1. [计算机科学](https://zh.wikipedia.org/wiki/Template:%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)
1. [10 architectures](https://www.cnblogs.com/IcanFixIt/p/7518146.html)
1. [CS-Notes](https://github.com/CyC2018/CS-Notes/blob/master/notes/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%20-%20%E7%9B%AE%E5%BD%95.md)
1. [Ruanyifeng](http://ruanyifeng.com/blog/2016/09/software-architecture.html)
1. [Software architecture patterns](https://www.oreilly.com/programming/free/files/software-architecture-patterns.pdf)
