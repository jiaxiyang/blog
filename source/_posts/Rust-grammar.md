---
title: Rust grammar
date: 2020-07-11 18:34:03
categories:
- Program
- Rust
tags:
- Rust
---

## Grammar
1. indent with four spaces, not a tab
1. Most lines of Rust code end with a semicolon(;)
1. `println!()` ! means call macro, not a function
1. Cargo is Rust's build system and package manager.
1. Cargo expects your source files to live inside the src directory. The top-level project directory is just for README files, license information, configuration files, and anything else not related to your code.
1. `cargo run` Compile the code and then run the resulting executable all in one command.
1. `cargo check` is much faster than `cargo build`
1. `cargo build --release` compile the project with optimizations. Run faster but compile slower.
1. The `main` function is the entry point into the program.
1. The `fn` syntax declares a new function, the parentheses, `()`, indicate there are no parameters, and the curly bracket, `{`, starts the body of the function.
1. `let` is used to create a variable. In Rust, variables are immutable by default.
1. `String::new()` An associated function is implemented on a type, in this case String, rather than on a particular instance of a String. Some languages call this a static method. This new function creates a new, empty string. You’ll find a new function on many types, because it’s a common name for a function that makes a new value of some kind.
1. `{}` is a place holder when using `println!`
1.  Crate is a coleection of Rust source code files.
1. Cargo.toml dependencies rand = "0.5.5";  In this case, we’ll specify the rand crate with the semantic version specifier 0.5.5. Cargo understands Semantic Versioning (sometimes called SemVer), which is a standard for writing version numbers. The number 0.5.5 is actually shorthand for ^0.5.5, which means “any version that has a public API compatible with version 0.5.5.”
1. `cargo doc --open` It will build documentation provided by all of your dependencies locally and open it in your browser.
1. `match` is like `switch` in C++
1. shallow copy, deep copy(clone), move(let s2 = s1; // s1 is invailid)
1. Differences Between Immutable Variables and Constants:
   - You declare constants using the const keyword instead of the let keyword, and the type of the value must be annotated.
   - Constants can be declared in any scope, including the global scope
   - Constants may be set only to a constant expression, not the result of a function call or any other value that could only be computed at runtime.
1. trait can add some useful functions for user's own struct.
1. trait 可以与泛型结合来将泛型限制为拥有特定行为的类型，而不是任意类型。
1. Rust编译时会将泛型代码单态化(monomorphization)来保证效率，单态化是指编译时用具体类型来填充泛型。
1. 用户会将重复代码泛化（抽象），编译器会将泛化代码具体化。
1. trait类似其他语言中接口(interfaces)功能，虽然有些不同。
1. 只有当trait或者要实现trait的类型位于crate的本地作用域时，才能为该类型实现trait。
1. 在 release 构建中，Rust 不检测溢出，相反会进行一种被称为二进制补码包装（two’s complement wrapping）的操作。当在 debug 模式编译时，Rust 检查这类问题并使程序 panic
1. Rust 的浮点数默认类型是 f64。数字类型默认是 i32。
1. Rust 的 char 类型的大小为四个字节(four bytes)，并代表了一个 Unicode 标量值（Unicode Scalar Value），这意味着它可以比 ASCII 表示更多内容。在 Rust 中，拼音字母（Accented letters），中文、日文、韩文等字符，emoji（绘文字）以及零长度的空白字符都是有效的 char 值。
1. Rust 有两个原生的复合类型：元组（tuple）和数组（array）。
1. 



## Project Manage
1. 包`packages`: Cargo的一个功能，允许你构建、测试和分享crate
1. `crates`: 一个模块的`树形`结构，它形成了库或二进制项目。
1. 模块`modules and use`: 允许你控制作用域和路径的私有性。
1. 路径`path`: 一个命名机结构体、函数或模块等项的方式。
1. 在Rust中，代码包也被称为crates
1. 一个包中可以包含多个二进制crate和一个可选的crate库。
1. 包中至少包含一个crate，无论是库还是二进制，至多包含一个库crate
1. `cargo new`会创建一个包。
1. Cargo准守一个约定： `src/main.rs`就是一个与包同名的二进制crate的crate根。同理，`src/lib.rs`是库crate的crate根。如果同时包含，则它有两个crate。
1. 通过将文件放在`src/bin`目录下，一个包可以拥有多个二进制crate：每个`src/bin`下的文件都会被编译成一个独立的二进制crate。
1. 模块让我们可以将一个crate中的代码进行分组，以提高重用性。
1. `模块的定义`是以`mod`(module)关键字为起始，然后指定模块的名字，并且用或花括号包围模块的主题。
1. `模块的声明`是以`mod`为起始，指定模块名字，以`;`结尾，不带有花括号。在与模块名同名的.rs文件中定义该模块。
1. 模块一般是在上一级文件声明，不是在本文件中声明，如可以在lib.rs中声明模块，然后在相应.rs文件中定义该模块。
1. crate的组织结构类似于文件系统的目录，被称为模块树(module tree)。
1. Rust通过路径来查找一个项的位置。
1. `绝对路径(absolute path)` 从crate根开始，以crate名或者字面值`crate`开头。
1. `相对路径(relative path)` 从当前模块开始，以`self`、`super`或当前模块的表示符开头。
1. 只有在同一crate中才能使用`crate::`关键字为起始的绝对路径。
1. 模块不仅对你组织代码很有用。它们还定义了Rust的私有性边界：这条界限不允许外部代码了解、调用和依赖被封装的实现细节。
1. Rust中默认所有项(函数、方法、结构体、枚举、模块、和常量）都是私有的。
1. 项是指：函数、方法、结构体、枚举、模块和常量。
1. 父模块中的项不能使用子模块中的私有项，但是子模块可以使用它们父模块中的项。
1. Rust通过这种方式来实现模块系统功能，因此隐藏内部实现细节，这样你就知道可以更改内部代码的哪部分而不会破坏外部代码。
1. 可以使用`super`开头来构建父模块开始的相对路径。类似于文件系统的`..`语法。
1. 如果请偶们将枚举设置为公有，则它的所有成员都将变为共有。
1. 在作用域中增加`use`类似于在文件系统中创建软连接。
1. 使用`use`引入结构体、枚举和其他项时，习惯是指定它们的完整路径。
1. 使用`use`将两个同名类型引入同意作用域的一个解决办法：在类型后面使用`as`指定一个新的本地名称或者别名。
1. `use std::{cmp::Ordering, io};`使用嵌套路径减少use的使用。
1. `use std::io:*` 将`std::io`中定义的所有公有项引入当前作用域。使用时要多加小心，常用于测试模块`tests`中。
1. Rust将package分成多个crate，将crate分成模块，通过绝对或相对路径从一个模块引用另一个模块。
1. Cargo提供了叫工作空间`workspaces`的功能，它可以帮助我们管理多个相关的协同开发的包。
1. 工作空间是一系列共享同样的cargo.lock和输出目录的包。
1. 工作空间顶级目录中的Cargo.toml中不包含`[package]`等信息，相反，它以`[workspace]`部分作为开始。
1. 工作空间在顶级目录有一个`target`目录，`member`并没有自己的target目录。通过共享的target目录，工作空间可以避免其他crate多余的重复构建。
1. cargo不假定工作空间中的crates包会相互依赖，所以需要明确表明工作空间中crate包的依赖关系。一个包用到了其他包，需要在该包的Cargo.toml文件`[dependencies]`域中加入依赖
1. 工作空间只在根目录有一个Cargo.lock，而不是在每一个crate（就当是packge)目录都有Cargo.lock。这确保了所有的crate都使用完全相同版本的依赖。也节省了空间，避免多个拷贝。
1. Cargo 有一个机制来确保任何人在任何时候重新构建代码，都会产生相同的结果：Cargo 只会使用你指定的依赖版本，除非你又手动指定了别的。

## Ownership 所有权
1. 当变量离开作用域，Rust 为我们调用一个特殊的函数drop。在 C++ 中，这种 item 在生命周期结束时释放资源的模式有时被称作 资源获取即初始化（Resource Acquisition Is Initialization (RAII)）。
1. `move:` `let s1 = String::from("hello"); let s2 = s1;`  这个操作被称为移动（move），而不是浅拷贝。Rust 则认为 s1 不再有效，因此 Rust 不需要在 s1 离开作用域后清理任何东西。
1. Rust 永远也不会自动创建数据的 “深拷贝”。因此，任何 自动 的复制可以被认为对运行时性能影响较小。
1. `clone:` 当出现 clone 调用时，你知道一些特定的代码被执行而且这些代码可能相当消耗资源
1. `copy:` `let x = 5; let y = x;` x在栈上，copy操作。Rust 有一个叫做 Copy trait 的特殊注解，可以用在类似整型这样的存储在栈上的类型上。如果一个类型拥有 Copy trait，一个旧的变量在将其赋值给其他变量后仍然可用。
1. Rust 不允许自身或其任何部分实现了 Drop trait 的类型使用 Copy trait。
1. 任何简单标量值的组合可以是 Copy 的，不需要分配内存或某种形式资源的类型是 Copy 的。

``` rust
fn main() {
    let s = String::from("hello");  // s 进入作用域

    takes_ownership(s);             // s 的值移动到函数里 ...
                                    // ... 所以到这里不再有效

    let x = 5;                      // x 进入作用域

    makes_copy(x);                  // x 应该移动函数里，
                                    // 但 i32 是 Copy 的，所以在后面可继续使用 x
} // 这里, x 先移出了作用域，然后是 s。但因为 s 的值已被移走，
  // 所以不会有特殊操作
  
fn takes_ownership(some_string: String) { // some_string 进入作用域
    println!("{}", some_string);
} // 这里，some_string 移出作用域并调用 `drop` 方法。占用的内存被释放

fn makes_copy(some_integer: i32) { // some_integer 进入作用域
    println!("{}", some_integer);
} // 这里，some_integer 移出作用域。不会有特殊操作
```

1. 变量的所有权总是遵循相同的模式：将值赋给另一个变量时移动它。当持有堆中数据值的变量离开作用域时，其值将通过 drop 被清理掉，除非数据被移动为另一个变量所有。
1. 将获取引用作为函数参数称为 借用（borrowing）。
1. 可变引用有一个很大的限制：在特定作用域中的特定数据只能有一个可变引用。
1. 也不能在拥有不可变引用的同时拥有可变引用。
1. Rust 中编译器确保引用永远也不会变成悬垂状态：当你拥有一些数据的引用，编译器确保数据不会在其引用之前离开作用域。
1. 在任意给定时间，要么 只能有一个可变引用，要么 只能有多个不可变引用。


## Error Handling 错误处理
1. Rust将错误组合成两个主要类别，可恢复错误和不可恢复错误。
1. 可恢复错误通常代表向用户报告错误和重试操作是合理的情况，比如未找到文件。
1. 不可恢复错误通常是Bug的同义词，比如访问超过数组结尾的位置。
1. 大部分语言并不区分这两类错误，并采用类似异常这样方式统一处理他们。
1. Rust没有异常，但是有可恢复错误`Result<T, E>`和不可恢复错误`panic!`
1. 执行Rust的`panic!`宏时，程序会打印出一个错误信息，展开并清理栈数据，然后接着退出。
1. 出现panic时，程序默认是`展开(unwinding)`，这意味着Rust会回溯栈并清理它遇到的每一个函数的数据。另一种选择是`终止(abort)`，这回不清理数据就退出程序。可以在Cargo.toml的[profile]部分增加`panic = 'abort'`，可以由展开切换为终止。
1. 使用`RUST_BACKTRACE`环境变量运行程序会得到一个backtrace，backtrace是一个执行到目前位置所有被调用的函数的列表。
1. Rust的backtrace跟其他语言一样：阅读backtrace的`关键`是`从头开始读直到发现你自己编写的代码`，这就是问题的根源。`这一行往上是你的代码所调用的代码，往下则是调用你的代码的代码(栈)`
1. 为了获取带有详细信息的backtrace，`必须是debug模式`
1. Result枚举的定义。`enum Result<T, E> { Ok(T), Err(E), }`，其中`T`代表返回的`Ok`成员中的`数据类型`，而`E`代表失败是返回`Err`成员中的错误的类型。
1. Result常与match进行联合使用

``` rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt"); // f值是Ok(file)或者是Err(error)

    let f = match f {
        Ok(file) => file,
        Err(error) => {
            panic!("Problem opening the file: {:?}", error)
        },
    };
}
```
1. `unwrap`函数作用于Result，如果Result的值是成员OK，unwrap会返回Ok中的值，如果是成员Err，unwrap会为我们调用`panic!`
1. `expect`与`unwrap`使用方式一样，`expect`用来调用`panic!`的错误信息将会作为参数传递给`expect`，而不像`unwrap`那样使用默认的`panic!`信息。`expect`更容易查找错误信息位置。
1. `?`运算符放在Result之后的含义：如果Result的值是Ok，这个表达式将会返回Ok中的值而程序继续执行，如果是Err，Err中的值将作为整个函数的返回值，就好像使用了return关键字一样，这样错误值就被传递给调用者。
1. 每一个Result都需要被处理，否则会出现警告。


## Traits

## Lifetimes 生命周期
1. 生命周期的目的是**避免悬垂指针**
1. `longest<'a>(x: &'a str, y: &'a str) ->&'a str` 它的实际含义是longest函数保证返回的引用的生命周期与传入该函数的引用的生命周期的较小者一致（x作用域和y作用域重叠的那一部分）。并没有改变传入值或返回值的生命周期，而是指出任何不满足这个约束条件的值都将被借用检查器拒绝。
1. `struct Test<'a> { part: &'a str, }` Test的实例不能比part字段中的引用存在的更久，Test实例应先离开作用域。（后定义的存在的应更短）
1. 每一个`引用`都有一个生命周期，我们需要为那些使用了引用的函数或者结构体指定生命周期。
1. 只有引用才需要指定生命周期。
1. 函数或方法的参数的生命周期被称为输入生命周期，二返回的生命周期被成为输出生命周期。
1. 函数或方法生命周期省略规则，需满足下面三条且无冲突
   - 每一个输入参数都有自己的生命周期参数
   - 如果只有一个输入周期，那么它将被赋予所有的输出生命周期参数
   - 如果有多个输入生命周期且其中一个是`&self`或者`&mut self`(说明是个对象的方法）；那么所有的输出生命周期参数将被赋予`self`的生命周期。
1. 生命周期省略简记：
   - 只有一个输入参数
   - 有多个输入且其中一个是`&self`
1. Rust中struct和其方法未封装到一起，C++相当于将struct和方法封装到类中。C也有struct和函数，但不具有trait或接口功能。
1. 方法签名中，`&self` 来替代 `rectangle: &Rectangle`，因为该方法位于`impl Rectangle`上下文中，所以Rust知道`self`类型是`Rectangle`
1. `impl`不以`self`作为参数的函数，被称为关联函数。是函数不是方法。(类似C++的静态函数）)
1. `self`是keyword. 方法中如果想改名字，可以这样传参`self1: &Rectangle`
1. 方法定义中的生命周期注解应用于关联函数，方法（含有`&self`)可省略。
1. 静态生命周期： `'static`，其生命周期能够存活于整个程序期间。所有的字符串字面值都拥有`'static`生命周期。
1. 生命周期也是泛型`test<'a, T>(x: &'a str, y: &'a str, ann: T) -> &'a str where T: Display` 因为生命周期也是泛型，所以`'a`和泛型参数`T`都位于函数名后的同一尖括号列表中。

## Generic Types 泛型

## Iterators and Closures 迭代器与闭包
1. 函数式编程：包含将函数作为参数值或其他函数的返回值，将函数赋值给变量以供之后执行等等。
1. 闭包：一个可以储存在变量里的类似函数的结构
1. 迭代器：一种处理元素序列的方式。
1. Rust的闭包是可以保存进变量或作为参数传递给其他函数的匿名函数（可以捕获环境的匿名函数）。可以在一个地方创建闭包，然后在不同的上下文中执行闭包运算。
1. 不同于函数，闭包允许捕获调用者作用域的值。
1. 在程序的一个位置指定某些代码，并只在程序的某处实际需要结果的时候执行这些代码。这正式闭包的用武之地。
1. 闭包通常很短，并只关联于小范围的上下文而非任意情境。在有限的上下文中，编译器能可靠的推断参数和返回值的类型。
1. 闭包语法：`let test = |num1, num2| { println("num1: {}",num1); num2 + 1 };` `|num1, num2|`是参数，`num2+1`是返回值。`let`表明`tet`是一个匿名函数的定义。不是调用匿名函数的返回值。`test`存储的是代码。
1. 带类型注解的闭包 `let test = |num1: u32, num2: u32| -> u32 { println("num1: {}",num1); num2 + 1 };`
1. 如果闭包体只有一行则大括号可以省略。例如： `let add_one = |x| x+1;`
1. 如果调用多次闭包，编译器会根据第一次使用时的参数类型，如果对同一闭包使用不同类型会得到类型错误。
1. ...
1.
1.
1. 迭代器负责遍历序列中的灭一项和决定序列何时结束的逻辑。
1. 迭代器是惰性的，在调用方法使用之前它都不会有效果。
1. 迭代器的实现方式提供了对多种不同的序列使用相同逻辑的灵活性，减少了重复代码并消除了潜在的混乱。
1. 迭代器都实现了定义于标准库的trait `Iterator`。包含`next`方法。
1. 迭代器的`sum`方法返回迭代的次数，会消费适配器。迭代器调用`sum`方法后不再允许使用迭代器，因为`sum`会获取迭代器所有权。
1. 迭代器的方法：`迭代器适配器(iterator adaptors)` 允许将迭代器变为不同类型的迭代器。
1. `v1.iter().map(|x| x+1);`迭代器适配器方法`map`使用闭包来调用每个元素以生成新的迭代器。这里的闭包创建了一个新的迭代器，对其中vector中的每个元素都被加1。因为迭代器适配器是惰性的，这里需要消费迭代器。
1. `collect`方法会消费迭代器并将结果收集到一个数据结构中。
1. 下面例子会调用`map`方法创建一个新的迭代器，接着调用`collect`方法消费新迭代器并创建一个vector。

``` rust
let v1: Vec<i32> = vec![1, 2, 3];
let v2: Vec<_> = v1.iter().map(|x| x + 1).collect();
assert_eq!(v2, vec![2, 3, 4]);
```

## Smart Pointers 智能指针
1. 指针是一个包含内存地址的变量的通用概念，这个地址指向一些其他数据。
1. Rust最常见的指针是引用，他们没有任何额外的开销，所以应用的最多。
1. `智能指针(smart pointers)`是一类数据结构，它们的表现类似指针，但是也拥有额外的元数据和功能。
1. `引用计数(reference counting)` 是智能指针类型，其允许数据有多个所有者。引用计数智能指针记录总共有多少个所有者，并当没有任何所有者时负责清理数据。
1. 在Rust中，普通引用和智能指针的一个额外的区别是引用是一类只借用数据的指针；相反，在大部分情况下，智能指针拥有他们指向的数据。
1. 智能指针通常使用结构体实现。
1. 智能指针区别于常规结构体的显著特性在于其实现了`Deref`和`Drop`trait。
1. `Deref` trait允许智能指针结构体实例表现的像引用一样，这样就可以编写既用于引用，又用于智能指针的代码。
1. `Drop` trait允许我们自定义当智能指针离开作用域时运行的代码。
1. 很多库都拥有自己的智能指针而你也可以编写属于你的智能指针。
1. `Box<T>`用于在堆上分配值。
1. `Rc<T>`一个引用计数类型，其数据可以有多个所有者。
1. `Ref<T>`和`RefMut<T>`通过`RefCell<T>`访问。
1. 最简单直接的智能指针是`box`，其类型是`Box<T>`，box允许你将一个值放在堆上而不是栈上，留在栈上的则是指向堆数据的指针。
1. 除了数据被存储在堆上而不是栈上之外，box没有性能损失，不过也没有很多额外的功能。多用于
   - 当有一个在编译时未知大小的类型，而又想要在需要确切大小的上下文中使用这个类型值的时候。（box作为链表的指针实现链表）
   - 当有大量数据并希望在确保数据不被拷贝的情况下转移所有权的时候。
   - 当希望拥有一个值并只关心它的类型是否实现了特定trait而不是具体类型的时候
1. `Box<T>`类型是一个只能智能指针，因为它实现了`Deref`trait，它允许`Box<T>`的值被当做引用对待。
1. 变量的所有权总是遵循相同的模式：将值赋给另一个变量时移动它。当持有堆中数据值的变量离开作用域时，其值将通过 drop 被清理掉，除非数据被移动为另一个变量所有。
1. & 符号就是 引用，允许你使用值但不获取其所有权。
1. 我们将获取引用作为函数参数称为 借用（borrowing）。


## Concurrency 并发

## Object Oriented 面向对象

## Macros 宏

## Program with C/C++
