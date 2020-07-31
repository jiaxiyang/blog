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



## Project Manage
1. 包`packages`: Cargo的一个功能，允许你构建、测试和分享crate
1. `crates`: 一个模块的`树形`结构，它形成了库或二进制项目。
1. 模块`modules and use`: 允许你控制作用域和路径的私有性。
1. 路径`path`: 一个命名机结构体、函数或模块等项的方式。
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

## Ownership 所有权

## Error Handling 错误处理

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
1.

## Smart Pointers 智能指针

## Concurrency 并发

## Object Oriented 面向对象

## Macros 宏

## Program with C/C++
