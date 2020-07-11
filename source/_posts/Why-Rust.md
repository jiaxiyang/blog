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
1. Friendly compiler
1. An integrated package manager

## Why Name Rust?
1. It's a pun on "chrome". Rust was written by the engineer company Mozilla(firefox). And chrome is a metal.


## 内存错误类型
1. 引用空指针
1. 使用未初始化的内存
1. 释放后使用，也就是使用悬垂指针
1. 缓冲区溢出，比如数组越界
1. 非法释放已经释放过的或者未分配的指针

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
