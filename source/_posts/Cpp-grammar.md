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

## Cast

## RALL

## Zero Cost Abstract

## Lambdas

## Move Semantics

## Template
1. typename关键字用于引入一个模板参数
1. 使用typename标识嵌套类型名称。
1. 使用从属类型时要加typename。比如：`typename T::const_iterator iter()`不加typename会报错，因为编译器并不知道T::const_iterator是一个类型的名字还是摸个变量的名字。
1. 可变参数模板(c++11之前参数个数固定不可变)：`template<typename... Args> class test`表示Args个数不固定，使用时`void f(Args... args)`

## Macros

## Reflection

## OOP

## Memory
1. 内存分为host内存和device内存。需要管理device上需要大空间的对象，比如tensor，还需要在host和device内存中传输数据。输入的数据在host端处理后需要发送到device上使用，device上输出结果或dump的数据需要在host端显示或者保存。不同的设备管理方式不同，当设备段是直接通过物理地址管理内存的，可以在host端创建一个对象来管理设备端的内存。

### 内存分配方式
1. `栈` 函数参数，局部变量
1. `堆` malloc和free。堆上操作系统维护的一块内存
1. `自由存储区` new和delete。自由存储区是C++中通过new和delete动态分配和释放对象的抽象概念。有些编译器使用malloc和free实现new和delete。
1. `全局/静态存储区` 全局变量和static变量。
1. `常量存储区` 存放的是常量，不允许修改。

### 内存管理方式
1. `自动存储`
1. `静态存储`
1. `动态存储`
1. `线程存储`




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

### class和struct区别
1. C++中的struct对C中的struct进行了扩充，可以有成员函数，可以被京城，可以有多台。
1. struct和class最大的区别是访问权限，struct成员默认是public的，class默认是private，struct继承默认是public，class默认是private。
1. class可以定义模板参数，就像typename，而struct不行。

### template定义时的typename和class区别
1. 最早使用的class可能会造成概念上的混淆，后面加上了typename替代class。

### new/delete和malloc/free区别
1. malloc/free是c++/c标准库函数，new/delete是C++运算符，都可以用于动态内存申请和内存释放。
1. new一个对象时会调用构造函数，delete一个对象时会调用析构函数。
1. 对于非内部累来说，malloc/free无法满足在对象创建时执行构造函数，在对象销毁时调用析构函数。
1. 由于内部数据类型的对象没有构造和析构的过程，对他们而言malloc/free和new/delete是等价的。
1. 为什么需要malloc和free，因为C++中经常调用c函数，而c只能用malloc和free管理动态内存（堆上）。

### 函数调用的过程

### 左值和右值

### c中的const和c++中的const区别
1. c语言中只有enum能实现真正的常量

### macro和inline

### const关键字作用

### 虚函数中的delete，new，final

### 友元
1. 友元函数
2. 友元类
3. 友元成员函数

###


## basic
