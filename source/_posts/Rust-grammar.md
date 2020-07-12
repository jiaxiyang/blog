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
