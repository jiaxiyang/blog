---
title: Cpp-concurrency-in-action
date: 2020-08-20 09:05:48
categories:
- Program
- Cpp
tags:
- Cpp
- Concurrency
---

## 1. Hello, world of concurrency in C++
### 1.1 并发是什么
1. 多进程并发优点： 操作系统在进程间提供的保护操作和更高级别的通信机制，可以更容易编写安全的并发代码。还有一个优势，可以使用远程连接的方式，在不同的机器上运行独立的进程。

### 1.2 为什么使用并发
1. `分离程序`： 将相互独立的部分分开就行操作。如DVD用户界面和播放功能应分离。
1. `性能`：两种方式：任务并行（将单一任务分成几部分并行）和数据并行（每个线程在不同的数据块上执行相同的操作）

#### 1.2.1 什么时候不使用并发
1. 收益比不上成本，除非潜在性能足够大，否则不使用并发，需要脑力成本和维护成本，代码更复杂，难以理解。
1. 资源有限： 太多线程的会耗尽资源。可以使用线程池进行优化。太多的线程上下文切换导致的性能损耗可能比增加线程的收益更多。

### 1.3 并发和多线程
#### 1.3.1 C++多线程历史
1. C++98标准不支持多线程，没有内存模型。
1. 各种非标准多线程库：MFC，Boost，大部分使用的是RAII

#### 1.3.2 支持并发
1. C++11: `线程管理，共享数据保护，线程间同步操作，原子操作`
1. C++11之后，C++标准支持多线程，也就是说可以跨平台编写高效，可移植的代码。编译器可以搞定具体平台，用户无需担心。

#### 1.3.4 C++线程库的效率
1. 高级工具（使用高级API, 抽象高）和低级工具（使用低级API，抽象低)有开销差，即抽象代价（abstraction penalty)。C++标准库设计时尽量使得高级API和低级API具有相同的性能。
1. 低级工具：为了达到终极性能，需要提供给硬件打交道的低级API。为了这个目的，形成了原子操作库。
1. 高级工具：为了使得编写多线程代码更简单。因为有额外的代码需要执行，这些工具会带来性能开销。
1. 如果很看重性能或者高级工具开销过高，可以通过低层工具来实现。绝大多数情况，有过高的复杂度和过大的出错率，来交换小幅度的性能收益是不划算的。


## 2. Managing threads

### 2.5 线程标识
1. `std::this_thread::get_id()`获取当前线程的ID.


## 3. Sharing data between threads
1. 错误的数据共享是多线程产生bug的主要原因。
1. `data race`: the specific type of race condition that arises because of concurrent modification to a single object
1. 数据竞争时间敏感，Bug可能很难复现，很难查找。

### 3.2 使用互斥量
1. 访问共享数据前将数据锁住，访问结束将数据解锁。
1. 互斥量是C++保护数据最通用的机制。
1. 互斥量问题： 死锁，对数据保护太多。
1. 一个互斥量只能用于一个资源的互斥访问。
1. 互斥量(互斥锁)本质上是一把锁。

#### 3.2.1 互斥量
1. `std::mutex`创建互斥量，`lock`对互斥量上锁，unlock为解锁。
1. RAII管理互斥量：C++标准库为互斥量提供了RAII模板类`std::lock_guard`，在构造时提供已锁的互斥量（lock_guard对象在构造时对传进来的mutex上锁），并在析构时解锁，从而保证互斥量被正确的解锁。
1.  大多数情况下，互斥量通常会与需要保护的数据放在同一类中，而不是定义成全局变量。

#### 3.2.4 死锁
1. 死锁一般解决方法：按顺序上锁。要么将两个都锁住，要么一个都不锁。
1. C++17中的`std::scoped_lock<>`是一种新的RAII模板类型。能接受不定数量的互斥量类型作为模板参数。在构造scoped_lock对象时对传入的mutex上锁，析构时解锁。


## 4. Synchronizing concurrent operations on atomic types

## 5. The C++ memory model and operations on atomic types

## 6. Designing lock-based concurrent data structures.

## 7. Designing lock-free concurrent data structures

## 8. Designing concurrent code

## 9. Advanced thread managment

## 10. Parallel algorithms

## 11. Testing and debugging multithreaded applications
