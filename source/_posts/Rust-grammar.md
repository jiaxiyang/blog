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
