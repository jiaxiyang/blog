---
title: Cpp grammar
date: 2020-08-03 14:28:44
categories:
- Program
- Cpp
tags:
- Cpp
---

## ideas
1. 记录语法时最好能举个例子
1. `why?`。模块`存在的目的？解决了什么问题？特点特性？优缺点？适用范围？概念？架构？设计思路？具体实现方式？`等方面学习？
1. 模块的存在的目的，功能作用，实现方式
1. 按照Bjarny Stroustrup列的特性重新进行分类。

## 原则
1. `开闭原则` 软件中的对象（类，模块，函数等等）应该对于扩展是开放的，但是对于修改是封闭的
1. `单一职责原则` 一个类只做一件事
1. `里氏替换原则` 子类应该可以完全替代父类，也就是说在使用继承时，只扩展新功能，不要破坏父类原有的功能。
1. `依赖倒置原则` 细节应该依赖与抽象，抽象不应该依赖于细节。把抽象层放在程序设计的高层，并保持稳定，程序的细节变化由低层的实现层来完成。
1. `迪米特法则/最少知道原则` 一个类不应该知道自己操作类的细节，换言之，只和朋友谈话，不和朋友的朋友谈话。
1. `接口隔离原则` 客户端不应该依赖它不需要的接口。如果一个接口在实现时，部分方法由于冗余被客户端空实现，则应该将该接口拆分，让实现类只依赖自己需要的接口。

## C++ language features

## OOP
1. Object-Oriented Programming
1. base class: defines the API
1. derived classes: provide different implementaions

## RAII Resource Acquisition Is Initalization
1. 资源获取初始化：`使用局部对象来管理资源的技术`被称为资源获取初始化。`局部对象`(有生命周期)是指存储在`栈`上的对象，它的生命周期由操作系统管理，无需人工介入。
1. 利用： C++保证了所有栈对象在生命周期结束时会被销毁(调用析构函数)。
   - `A a;` 在栈上分配a
   - `A* a = new A()` 在堆上分配a，并在栈上保存a的指针，生命周期结束后只释放栈上的指针变量，需要delete释放资源。。
   - `unique_ptr<A> a = make_unique<A>(new A())` 在栈上分配a，在堆上分配A的对象，a中保存了A对象的指针，a用来管理A对象，当a生命周期结束，会调用a的析构函数，释放A对象资源。
1. RAII用来自动管理对象，例如smart pointers，用栈来管理资源。
1. RAII流程：设计一个类封装资源，构造函数初始化，析构函数释放资源。
1. RAII可以极大地简化资源管理，并有效的保证程序的正确和代码的简洁。
1. The slogan is about initialization, but its meaning is ready about cleanup.
1. `resource`: anything that requires specail(manual) management.
   - Allocated memory(molloc/free, new/delete)
   - POSIX file handles(open/close)
   - C FILE handles(fopen/fclose)
   - Mutex locks(pthread_mutex_lock/pthread_mutex_unlock)
   - C++ threads(spawn/join)
   - objective-c resource-counted objects(retain/release)
1. resource管理涉及到的操作： 资源释放（destructor)，资源复制(copy constructor)，释放原来资源并复制其他资源(copy assignement operator)，资源所有权转移(move operator)，释放原来资源并转移其他资源(move assignment operator)。
1. RRID(Resource Release Is Destruction)


### 构造函数，析构函数，copy构造函数，copy赋值构造函数，move构造函数，move赋值构造函数
1. 全局对象的构造函数在程序进入 main() 函数之前执行
1. Initialization is not assignment.
1. `T w = v;` This is an initialization(construction) of a new object. It calls a copy constructor.
1. `T w; w = v;` This is an assignment to the existing object w. It calls an assignment operator.
1. 使得函数default可能提醒他人调用default是可以正常工作的。
1. 资源释放应该放到析构函数中，避免资源泄露。
1. 赋值构造函数最好使用copy-and-swap.这样可以解决self-copy等问题。
1. 析构函数的调用与构造函数反序。

``` c++
// copy assignment constructor
T& T::operator=(const T& rhs) {
    T copy(rhs);  // 调用copy构造函数
    copy.swap(*this);  // good
    return *this;
}  // copy will be destruct

// move assignment constructor
T& T::operatr=(T&& rhs) {
    T copy(std::move(rhs));  // rhs现在是左值？
    copy.swap(*this);
    return *this;
}

```

###  The Rule of Three or Five(after c++11)
1. 含义：如果类里面需要管理resource，例如rall pointer，那么你需要手写3个functions.否则会调用默认函数，可能会出现多个指针副本，引起悬垂指针等问题。（可以delete这些函数，使non-copyalble)
   - A destructor to free the resource
   - A copy constructor to copy the resource
   - A copy assignment operator to free the left-hand resource and copy the right-hand one.
   - A move constructor to transfer owenership of resource (after c++11)
   - A move assignment operator to free the left-hand resource and transfer ownership of the right-hand one(after c++11)

### The Rule of Zero
1. 含义：如果你的类没有管理任何资源，但是使用了库中的vector，string等，那么你应该避免写特殊的函数，使用默认函数。
   - Let the compiler implicitly generate a default destructor
   - Let the compiler generate the copy constructor
   - Let the compiler generate the copy assignment operator
   - (But your own swap might improve performance)

### 两种设计良好的value-semantic C++类
1. Bussiness-logic classes: 不管理资源，follow the Rule of Zero
1. Resource-management classes(small, single purpose)： 管理资源(最好使用RAII)，follow the Rule of Three or Five.

### move
1. move does not move anything. （只是所有权移动，为物理移动任何东西）
1. move unconditionally casts its input into an rvalue reference(无变量保存的数据)，会将输入变为右值。
1. move constructor `ClassXX(ClassXX&& w) = default` w是右值引用
1. move assignment operator `ClassXX& operator=(ClassXX&& w) = default`
1. 类成员最好用智能指针。原始指针不能使用默认move构造函数。需要自己写move构造函数， 分两步： member-wise move and reset。
1. move asignment operator分3步： cleanup, member-wise move and reset
1. make move operations(constructor) noexcept
1. Don't return a T&&.
1. 使用move后，原来的变量不再进行资源释放，它已经将所有权转移给新的变量，由新变量进行资源管理。

### forward
1. `& & = &`, `& && = &`, `&& & = &`, `&& && = &&`  变量，是lvalue
1. `void f(T&& x); auto&& var = var1;` 其中T&&和auto&&是forward reference(T类型不确定，T&&类型要通过推导（模板），如果T是确定的，那么是右值引用，如类的move构造函数T就是类名称)。转发引用。被称为universal reference.
1. forward reference作为参数能接受左值也能接受右值。
1. 应用: `make_unique`可以传左值和右值。`auto i = make_unique<int>(1); auto s1_ptr = make_unique<string>(s1)`
1. std::forward（不是forward reference, 是标准库函数）作用： 如果输入是lvalue，将其转化为lvalue reference，如果是rvalue，将其转化为rvalue reference。使用原因：当一个函数输入参数是右值，并且需要用到该参数调用其他函数，调用时会将右值转化为左值，因为有了名字。在调用的函数中被当做左值来处理。如果希望是右值，则实现不了。在调用其他函数时，将参数通过std::forward转化一下
1. std::forward does not forward anything。
1. 问题：forward reference作为模板的参数时能接收任何参数，容易与其他函数冲突。

### 左值(lvalue) 右值(rvalue)
1. 左值：占据内存中某个可识别位置（有变量保存）的对象
1. 右值：临时存储，没有变量标识。
1. 如果表达式的结果是一个暂时的对象，那么这个表达式就是右值。
1. 如果函数能直接返回，不要起名字。return右值，否则要使用move。(RVO)

### && rvalue reference 右值引用
1. 只有左值才能给引用`int nine = 9; int& ref = nine;` 不能`int& ref = 9;`，也不能`int& ref = get_value()`
1. 右值引用用法：`int&& ref = 9`或`int&& ref = get_value()`

## Lifetime

## Smart Pointers
1. 用来管理raw pointer，属于资源管理类。

### unique_ptr
1. 防止内存泄露，使所有权清晰。
1. 唯一所有权， 不能复制，只能move
1. 有一个Deleter成员变量
1. 有两个参数，Deleter有默认
1. 智能指针传参和返回值应该`按值传递`，这样更简单，而且只会消耗很小的资源(8字节)，栈上传递，很快.
1. 不要通过引用传递指针

``` c++
template<class T, class Deleter = std::default_delete<T>>
class unique_ptr {
    T* p_= nullptr;
    Deleter d_;

    ~unique_ptr() {
        if (p_) d_(p_);
    }
}

template<class T>
struct default_delete {
    void operator()(T* p) const {
        delete p;
    }
}

```

1. 需要调用free, close等地方，可以封装为unique_ptr, sample:

``` c++
struct FileClose {
    void operator()(File *fp) const {
        assert(fp != nullptr);
        fclose(fp);
    }
}

File *fp = fopen("input.txt", "r");
std::unique_ptr<File, FileClose> uptr(fp);
```


### shared_ptr
1. 避免悬垂指针。
1. shared mean reference counting引用计数
1. "Will the last person out of the room please turn out the lights." 最后一个离开房间的人请关灯，人数就相当于引用计数，灯相当于共享的资源。最后一个释放资源。如果房间里还有人就把灯关了，剩下的人就相当于悬垂指针。
1. 栈上有两部分ptr to T and ptr to control block。分别指向堆上数据。
1. uniqe_ptr可以转化为shared_ptr，反之不成立。

### make_shared and make_unique
1. 现代的c++应该避免使用raw new and delete，智能指针可以避免使用delete，我们也应该避免使用new，工厂函数能够避免new。
1. make_shared and make_unique都是`工厂函数`。make_shared能够产生一个shared_ptr，make_unique能够产生一个unique_ptr
1. `最好不要使用rall pointer`，。如果不用rall pointer，就不用担心内存泄露。

### weak_ptr
2. weak_ptr可以告诉你xuan
1. weak_ptr has the same physical layout ad shared_ptr
1. weak_ptr不是智能指针。不能对weak_ptr解引用
1. weak_ptr可以看作是获取shared_ptr的 ticket，如果拥有weak_ptr就有权获得shared_ptr。
1.

### std::enable_shared_from_this

## Cast

## Zero Cost Abstract

## Lambdas
1. 用于定义和创建匿名函数。
1. 语法： `[capture list] (params list) mutable exception -> return type { function body}`

## Generic Programming
1. 泛型编程是为算法流程编写的，不是为数据结构，使算法通用化，可以适应不同的数据结构。
1. 可以先写一个具体的例子，抽象出算法，屏蔽数据结构（类型）。
1. `A type: specifies the set of operations that can be applied to an object and specifies how an object is laid out in memory` 类型不仅规定对象的操作集合，还规定对象在内存中的排布
1. `A concept: Specifies the set of operations that can be applied to an object and says nothing about the layout of the object` Concept只规定对象的操作集合，不规定对象在内存中的排布。
### Template
1. typename关键字用于引入一个模板参数
1. 使用typename标识嵌套类型名称。
1. 使用从属类型时要加typename。比如：`typename T::const_iterator iter()`不加typename会报错，因为编译器并不知道T::const_iterator是一个类型的名字还是摸个变量的名字。
1. 可变参数模板(c++11之前参数个数固定不可变)：`template<typename... Args> class test`表示Args个数不固定，使用时`void f(Args... args)`
1. `template <typename T> using xxx = T`

### 模板嵌套

## Macros
### #define

## Reflection
1. 反射字面意思：由类型名映射到类型对象？
1. 反射技术以其明确分离描述系统自身结构、行为的信息与系统所处理的信息，建立可动态操纵的因果关联以动态调整系统行为的良好特征，已经从理论和技术研究走向实用化，使得动态获取和调整系统行为具备了坚实的基础。当需要编写扩展性较强的代码、处理在程序设计时并不确定的对象时，反射机制会展示其威力，反射技术以其明确分离描述系统自身结构、行为的信息与系统所处理的信息，建立可动态操纵的因果关联以动态调整系统行为的良好特征，已经从理论和技术研究走向实用化，使得动态获取和调整系统行为具备了坚实的基础。当需要编写扩展性较强的代码、处理在程序设计时并不确定的对象时，反射机制会展示其威力，这样的场合主要有：
   - 序列化（Serialization）和数据绑定（Data Binding）
   - 远程方法调用（Remote Method Invocation RMI）
   - 对象/关系数据映射（O/R Mapping）。
1. 由于c++中的类结构可读性差，难以调试，协议升级困难等缺点，导致xml与json等自注释文本协议普及。但`文本协议`（文件里方便阅读理解）与`内存模型`（内存上）存在差异，需要有序列化与反序列化对象的操作。序列化：将文本转化为类对象，反序列化：将类对象转化为文本。开发者需要写大量重复代码去进行序列化与反序列化操作。Java为解决这个问题添加了反射机制:将类型信息编译到class文件中，并利用这些信息提供统一的序列化与反序列化功能。
1. 反射基本功能之一：如何通过类的名称来生成新的对象？例：`ClassXX object = new "ClassXX"`, C++使用：`ClassXX object = new ClassXX(x)` 工厂函数是通过在工厂函数里指定tpye来生成，不是通过类名。`ClassXX object = ClassXX::create(x)`
1. 实现方法：
   - 每一个类都创建一个产生对象的函数
   - 设计一个总的工厂类，类中使用map保存(类名，函数)。通过共产类创建对象。因为全局只需要一个工厂类的对象，因此使用单例模式设计工厂类。
1. 编程语言的反射机制所能实现的功能还有通过类名称字符串获取类中属性和方法，修改属性和方法的`访问权限`等，系统运行起来之后可修改类属性方法权限，厉害。

### Reference
1. [concept](https://zhuanlan.zhihu.com/p/70044481)
1. [sample](https://blog.csdn.net/K346K346/article/details/51698184)

## Dependency Injection (DI)依赖注入  Inversion of Contol (IOC)控制反转
1. 解决依赖类之间的紧耦合问题，假设a依赖b（b的实例可能是a的成员变量），实现了b类实例的创建与a无关。
1. 通常由调用者创建被调用者的实例（调用者依赖被调用者，调用者会在自己函数体内创建被调用者），当创建被调用者不再由调用者来完成，而是通过容器来创建被调用者实例，然后注入调用者。因此被成为依赖注入。
1. a依赖b，但a不控制b的创建和销毁，仅使用b，那么b的控制权交给a之外处理，这叫`控制反转`，而a要依赖b，必然要使用b的instance，那么通过a的接口把b传入，或通过a的构造把b传入，或通过设置a的属性把b传入，这个过程叫做`依赖注入`。
1. 随着DI的频繁使用，要实现IOC(相当于工厂模式中总的工厂)，会有很多重复代码，有人将实现IOC的代码打包成组件或框架，来避免人么重复造轮子。所以实现IOC组件或框架，我们可以叫它`IOC Container`。
1. DI是IOC实现方法之一。
1. 构造方法注入： a构造函数中将b作为参数传递。
1. 工厂模式注入： 将b的工厂传递给a。


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

### 操作符重载

### 作用域
1. `全局作用域`
1. `局部作用域`
1. `语句作用域`
1. `类作用域`
1. `命名空间作用域`
1. `文件作用域`

### 函数指针

1. 声明

``` c++
double cal(int);   // prototype
double (*pf)(int);   // 指针pf指向的函数， 输入参数为int,返回值为double
pf = cal;    // 指针赋值
```

1. 作为函数参数

``` c++
void estimate(int lines, double (*pf)(int));  // 函数指针作为参数传递
double y = (*pf)(5);   // 通过指针调用， 推荐的写法
double y = pf(5);     // 这样也对， 但是不推荐这样写
```

### typedef
1.  任何声明变量的语句前面加上typedef之后，原来是变量的都变成一种类型。不管这个声明中的标识符号出现在中间还是最后。
1. 作用：
   - 促进跨平台开发
   - 定义易于记忆的类型名
1. 使用：
   - `typedef int* IntPtr; int x = 5; IntPtr = &x; *IntPtr = 1;`
   - `typedef void (*call_back)(int)； void add_one(int i) {return i+1}; call_back = add_one; call_back(2);` call_back声明为函数指针



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

### for each any_of

### rang-based for loop

### std::tie
1. 创建tuple的左值引用
1. 可以用来解tuple
1. c++17之后可以被structured bindings替代

### Structured Bindings c++17
1. `const auto &[elem1, elme2] = some_thing;`
1. 类似引用，结构化绑定是既存对象的别名。不同于引用的是，结构化绑定的类型不必为引用类型。
1. [reference](https://zh.cppreference.com/w/cpp/language/structured_binding)

### concepts c++20

### modules c++20

### string_view c++17

### std::format c++20

### ranges c++20

### fold expressions

### std::exchange()

### const


### c中的const和c++中的const区别
1. c语言中只有enum能实现真正的常量

### macro和inline

### const关键字作用

### default， delete，override，final，noexcept
1. `final`在基类中指定无法在派生类中重写的虚函数。还可以指定无法继承的类。
1. 当使用default或者delete定义构造，析构，复制构造，赋值，move...其中一个时，也需要定义其他的。

### explicit
1. explicit只能用来修饰类构造函数。作用是声明类构造函数是显示调用的，不能隐式调用。
1. 只能显示使用`ClassXX a(args)`来创建对象，不能使用`ClassXX a = args`来隐士调用构造函数。
1. 作为函数参数也必须使用`ClassXX(args)`，不能使用`args`隐式调用构造函数。
1. 能用就用。

### virtual
1. 接口类(基类)的析构函数需要为virtual,这样才能正常调用子类的析构函数，如果不为virtual，那么只会调用基类的析构函数，不会调用子类的。


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

### std::function
1. std::function是通用多态函数封装器。
1. 定义：`template < class R, class... Args> class function<R(Args...)` R为返回类型，Args为参数。
1. 例子：`void p(int i) { cout << i;};  std::fuction<void<int>> f = p; f(i);`
1. 可用来实现函数回调

### std::atomic


## Design Patterns
### 工厂模式
1. 目的：将对象的创建与对象的使用解耦。
1. `简单工厂函数` 将对象的创建放入到统一工厂函数中，根据类型判断具体创建哪一种类型对象。相当于将耦合问题从使用中转移到工厂函数。扩展性差，每增加一个产品就要修改工厂函数。
1. `工厂方法模式` 每个产品都有一个工厂函数，相当于将耦合从总的工厂函数中转移到各个产品的工厂函数中，问题：使用时需要包含各个工厂头文件。
1. `抽象工厂模式` 同工厂方法模式，只不过每一个具体工厂可以可以调不同接口（不是同一个接口传参数）创建不同的产品。
1. `反射，依赖注入` 由类名来创建对象。相当于工厂方法模式+单例模式。全局有一个总的工厂，工厂里有保存产品类型及其工厂函数的map表(使用到函数指针)，每个产品都要有一个工厂，并且需要注册（依赖注入）到总的工厂map表中。解决了工厂方法模式中使用问题。map可以使用全局变量，注册函数写成类的静态函数，就不需要专门设计一个总的工厂类。总工厂生产的产品不由总工厂控制，而是交给子工厂控制，这叫`控制反转`，将子工厂通过注册接口传入到总工厂中，这叫`依赖注入`
1. `模板工厂模式`

#### Reference
1. [factory method](https://www.cnblogs.com/xiaolincoding/p/11524401.html)
1. [reflection](https://blog.csdn.net/K346K346/article/details/51698184)


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
