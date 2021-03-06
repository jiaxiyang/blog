---
title: Memory concept and issues
date: 2020-07-26 15:34:35
categories:
- Program
- Basic
tags:
- Memory
- C++
- Rust
---

## 内存概念
1. 栈和堆都是代码在运行时可供使用的内存。
1. 栈中的所有数据都必须占用已知且固定大小。
1. 栈的读写比堆要快。
1. 当代码调用一个函数时，传递给函数的值和数据的局部变量被压入栈中，当函数结束时，这些值被移除栈。
1. Rust所有权的存在是为了管理堆数据。
1. 数据在堆上才需要释放
1. 数据在堆上赋值时无指出是浅拷贝(C++)或移动(Rust，原来的变量不在有效)，而不是深拷贝。
1. Rust数据在栈上，赋值是都是拷贝，原来的变量依旧有效。在堆上，赋值都是移动，原来变量无效。
1. Rust String由三部分组成，ptr，len，capacity，这一组数据在栈上，ptr是指向在堆上数据的指针。（数据结构的固定长度数据在栈上，可变数据在堆上）

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
