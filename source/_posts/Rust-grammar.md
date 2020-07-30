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

    ``` rust
    let foo = 5;  // immutable
    let mut bar = 5;  // mutable
    ```

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
