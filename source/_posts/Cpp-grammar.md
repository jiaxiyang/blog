---
title: Cpp grammar
date: 2020-08-03 14:28:44
categories:
- Program
- Cpp
tags:
- Cpp
---

## C++ language features

## Lifetime

## Smart Pointers

## RALL

## Zero Cost Abstract

## Lambdas

## Move Semantics

## Template

## OOP

## Memory

## Multi Thread


## Small Module
### 值语义与引用语义
1. 值语义(value sematics)指的是对象的拷贝与原对象无关，就像拷贝int一样，拷贝之后与原对象脱离关系。
1. 引用语义(reference sematics)或者对象语义(object sematics)是指面向对象意义下的对象，对象是禁止拷贝的。因为拷贝对象是无意义的，如拷贝一个雇员不会变成两个雇员。
1. 值语义：复制（赋值操作）以后，两个数据对象拥有的存储空间是独立的，相互之间互不影响。
1. 引用语义：复制（赋值操作）以后，两个数据对象互为别名。操作其中一个会影响另一个。
1. 引用语义赋值操作是按位复制，有可能只复制了栈上的数据，为复制堆
1. 值语义的好处： 生命周期管理很简单，不用担心生命周期。
1. 引用语义的object由于不能拷贝，我们只能通过指针或引用来使用它。需要考虑生命周期来释放资源，避免悬垂指着等。
1. 使用指针和引用之后所有的赋值代表将有多个变量指向同一个对象，一旦其中一个变量释放了对象的资源，其他的变量的使用将是一个问题。
1. (zero abstract cost) C++的class的layout与C struct一样，没有额外开销。定义一个只包含一个int的class的对象和定义一个int一样。
1. 默认拷贝构造函数是最简单的浅拷贝。
1. 智能指针实际上是将对象语义转化为值语义。
1.


## basic
