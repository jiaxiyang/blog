---
title: Cargo
date: 2020-08-05 08:58:58
categories:
- Program
- Rust
tags:
- Rust
- Cargo
---

## Build Scripts
1. 有些库依赖第三方语言的库，例如需要C库，并且需要从源码编译，cargo目标并不是取代那些优化很好的第三方编译工具，所以cargo通过build脚本来集成其他工具。
1. 在crate包的根路径下创建一个名为`build.sh`的脚本，Cargo会在编译crate包之前先编译`build.sh`脚本然后执行该脚本。
1. 如果`build.sh`依赖的文件有任何改变，会被重新编译。
1. build脚本的输入是通过环境变量传递的。
1. 环境变量中的当前路径就是`build.sh`源码所在路径。
1. build脚本会将输出放入到`OUT_DIR`中的各个路径中。所以build脚本不应该改变这些输出路径中的文件。
1. Cargo会解析那些以`cargo:`开头的行，其他行被忽略。
1. build脚本的输出默认被隐藏，可以使用`-vv`(very verbose)来查看输出。如果依赖的文件没有被改变，什么都不会输出，因为不会重新执行编译脚本。
1. build脚本的编译输出都会存在类似于`target/debug/build/<pkg>/output`文件中。
1. ...
1. `build.sh`中依赖的crates需要在Cargo.toml中的`[build-dependencies]`中指定依赖，`build.sh`可用的依赖见[crates.io build-dependencies crates](https://crates.io/keywords/build-dependencies)
