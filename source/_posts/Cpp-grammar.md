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
1. 用于定义和创建匿名函数。
1. 语法： `[capture list] (params list) mutable exception -> return type { function body}`

## Move Semantics

## Template
1. typename关键字用于引入一个模板参数
1. 使用typename标识嵌套类型名称。
1. 使用从属类型时要加typename。比如：`typename T::const_iterator iter()`不加typename会报错，因为编译器并不知道T::const_iterator是一个类型的名字还是摸个变量的名字。
1. 可变参数模板(c++11之前参数个数固定不可变)：`template<typename... Args> class test`表示Args个数不固定，使用时`void f(Args... args)`
1. `template <typename T> using xxx = T`

## Macros
### #define
### typedefine

## Reflection
1. 由于c++中的类结构可读性差，难以调试，协议升级困难等缺点，导致xml与json等自注释文本协议普及。但`文本协议`（文件里方便阅读理解）与`内存模型`（内存上）存在差异，需要有序列化与反序列化对象的操作。序列化：将文本转化为类对象，反序列化：将类对象转化为文本。开发者需要写大量重复代码去进行序列化与反序列化操作。Java为解决这个问题添加了反射机制:将类型信息编译到class文件中，并利用这些信息提供统一的序列化与反序列化功能。
1. 如何通过类的名称来生成新的对象？例：`ClassXX object = new "ClassXX"`, C++使用：`ClassXX object = new ClassXX(x)` 工厂函数是通过在工厂函数里指定tpye来生成，不是通过类名。`ClassXX object = ClassXX::create(x)`
1. 实现方法：
   - 每一个类都创建一个产生对象的函数
   - 设计一个总的工厂类，类中使用map保存(类名，函数)。通过共产类创建对象。因为全局只需要一个工厂类的对象，因此使用单例模式设计工厂类。
### Reference
1. [concept](https://zhuanlan.zhihu.com/p/70044481)
1. [sample](https://blog.csdn.net/K346K346/article/details/51698184)


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

### static
1. 局部static变量只被初始化一次，生命周期是从创建到程序结束。相比全局static变量只是作用域不是全局。
1. 如果全局变量仅在单个函数中使用，则可以将这个变量改为该函数的静态局部变量。
1. 全局变量，静态局部变量，静态全局变量都存在全局静态存储区。
1. 函数中必须要使用statci变量的情况：当某个函数返回值为指针类型时，则必须是static的局部变量的地址作为返回值，因为他的生命周期是整个程序运行期间。
1. static全局变量限定作用范围为定义该变量的文件。
1. 子类访问父类定义的static成员变量或函数`Son::Parent::xxx()`
1. static存储在全局静态存储区，因此父类中定义的static变量由所有子类父类对象共享。

### 作用域
1. `全局作用域`
1. `局部作用域`
1. `语句作用域`
1. `类作用域`
1. `命名空间作用域`
1. `文件作用域`

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

### 虚函数中的delete，override，final
1. `final`在基类中指定无法在派生类中重写的虚函数。还可以指定无法继承的类。

### explicit
1. explicit只能用来修饰类构造函数。作用是声明类构造函数是显示调用的，不能隐式调用。
1. 只能显示使用`ClassXX a(args)`来创建对象，不能使用`ClassXX a = args`来隐士调用构造函数。
1. 作为函数参数也必须使用`ClassXX(args)`，不能使用`args`隐式调用构造函数。
1. 能用就用。

### move

### 左值(lvalue) 右值(rvalue)
1. 左值：占据内存中某个可识别位置的对象
1. 如果表达式的结果是一个暂时的对象，那么这个表达式就是右值。

### && rvalue reference 右值引用
1. 只有左值才能给引用`int nine = 9; int& ref = nine;` 不能`int& ref = 9;`，也不能`int& ref = get_value()`
1. 右值引用用法：`int&& ref = 9`或`int&& ref = get_value()`

### 友元
1. 友元函数
2. 友元类
3. 友元成员函数

### decltype
1. 获取变量的类型。`int x; decltype(x) y; // y is int`
2. 可以用于匿名结构体。

### constexpr


### add pointer and is pointer remove_pointer
1. 都是类模板，定义在std中
1. `add_pointer<T>`：T可以是具体类型也可以是类型引用。获取类型的指针，保存在type成员变量里。一般和typede一起使用`typedef std::add_pointer<x>::type IntPtr; IntPtr i;`


## Design Patterns
### 工厂模式
### 单例模式
1. 目的： 保证一个类只有一个实例，并且提供一个访问它的全局访问点，该实例被所有程序模块共享
1. [reference](https://zhuanlan.zhihu.com/p/37469260)
1. code

``` c++
class Singleton
{
 private:
	Singleton() { };  // 私有构造函数，拷贝构造函数和赋值函数，防止创建对象。
	~Singleton() { };
	Singleton(const Singleton&);
	Singleton& operator=(const Singleton&);
 public:
	static Singleton& get_instance()
    {
		static Singleton instance;  // 使用local static对象，只在第一次访问get_instance才创建
		return instance;
	}
};
```
### 代理模式

## Program with C


## 接口实现分离
1. `Pimplldiom`(防火墙技术，代理模式？(未提供一个抽象接口)) 将实现细节隐藏于指针背后，比如：分成两个类，一个负责提供接口，一个负责提供实现。负责提供实现的类的对象作为负责提供接口类的私有成员。这种方式只能不能像工厂函数一样由多种实现，因为类中写死了一种实现方式。
2. `Object Inerface` 将接口定义为抽象类，派生类实现这些借口。类似工厂函数(创建型设计模式)。

### Reference
1. [reference](https://blog.csdn.net/TAOKONG1017/article/details/79561856)
