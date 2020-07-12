---
title: Why Rust
date: 2020-07-10 21:45:08
categories:
- Program
- Rust
tags:
- Rust
---

## Why Rust?
### Performance
1. It's **`fast`** and memory efficient: with no runtime or garbage collector.
1. It can easily integrate with other languages.

### Reliability
1. It's rich type system and ownership model guarantee <font color='red'>**memory-safety**</font> and <font color='red'>**thread-safety**</font>.

### Productivity
1. Great documentation
1. Friendly compiler, find most errors when compiling
1. An integrated package manager
1. Doc system: `cargo doc --open`

## Why Name Rust?
1. It's a pun on "chrome". Rust was written by the engineer company Mozilla(firefox). And chrome is a metal.

## Rust 目的
1. 创建这个新语言的目的是为了解决一个顽疾：软件的演进速度大大低于硬件的演进，软件在语言级别上无法真正利用多核计算带来的性能提升。Rust是针对多核体系提出的语言，并且吸收一些其他动态语言的重要特性，比如不需要管理内存，比如不会出现Null指针等

## 内存(堆栈)错误类型
1. 引用空指针
1. 使用未初始化的内存
1. 释放后使用，也就是使用悬垂指针
1. 缓冲区溢出，比如数组越界
1. 非法释放已经释放过的或者未分配的指针

## 内存管理方式
1. 垃圾回收机制，在程序运行时不断的寻找不再使用的内存
1. 程序员亲自分配内存和释放内存
1. Rust通过所有权系统管理内存，编译器在编译时会根据一系列规则进行检查，拥有数据所有者在离开作用域后自动清除其数据

## Rust类型系统借鉴Haskell特性
1. 没有空指针
1. 类型默认不可变
1. 表达式
1. 高阶函数
1. 代数数据类型
1. 模式匹配
1. 泛型
1. trait和关联类型
1. 本地类型推导

## Rust相比Haskell独有特点
1. 仿射变换(Affine Type)
1. 借用，生命周期
