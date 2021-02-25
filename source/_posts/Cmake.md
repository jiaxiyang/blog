---
title: Modern Cmake
date: 2021-01-028 08:56:09
categories:
- Tools
- Cmake
tags:
- Cmake
---

## Concepts
1. CMake is not a build system. It's the build system generator.

## Target and Property
1. 现代化的CMake是围绕 Target 和 Property 来定义的，并且竭力避免出现变量variable的定义。Variable横行是典型CMake2.8时期的风格。现代版的CMake更像是在遵循OOP的规则，通过target来约束link、compile等相关属性的作用域。

### Target
1. 如果把一个Target想象成一个对象（Object），会发现两者的组织方式非常相似：

```
构造函数：
add_executable
add_library
成员函数：
get_target_property()
set_target_properties()
get_property(TARGET)
set_property(TARGET)
target_compile_definitions()
target_compile_features()
target_compile_options()
target_include_directories()
target_link_libraries()
target_sources()
成员变量
Target properties（太多）
```

### Properties
1. target_xxx命令PRIVATE/PUBLIC...后为property，例如

```
target_source(MyEXE PRIVATE "main.cpp")  ## main.cpp为source属性
target_link_library(MyEXE PRIVATE Poco::Net Poco::Util) ## Poco:Net Poco::Util为link属性
target_compile_definition(MyEXE PRIVATE std_cxx_14) ## std_cxx_14为编译属性
```

## Build-Requirements and Usage-Requirements
1. `Build-Requirements`： 包含了所有构建Target必须的材料。如源代码，include路径，预编译命令，链接依赖，编译/链接选项，编译/链接特性等。
1. `Usage-Requirements`：包含了所有使用Target必须的材料。如源代码，include路径，预编译命令，链接依赖，编译/链接选项，编译/链接特性等。这些往往是当另一个Target需要使用当前target时，必须包含的依赖

## PRIVATE/INTERFACE/PUBLIC
1. 定义了`Target属性`的传递范围。
1. `PRIVATE`: 表示Target的属性只定义在当前Target中，任何依赖当前Target的Target不共享PRIVATE关键字下定义的属性。
1. `INTERFACE`：表示Target的属性不适用于其自身，而只适用于依赖其的Target。
1. `PUBLIC`：表示Target的属性既是build-requirements也是usage-requirements。凡是依赖。凡是依赖于当前Target的Target都会共享本属性。

## Modern Cmake Using Steps
1. Always create targets with no sources first.
1. Use `target...` commands to add build-/usage-requirements
1. Use `IMPORTED` targets for external libraires. But, prefer `find_package` or `EXPORTED` targets ro creating them yourself.

## 3.13之默认生成绝对路径
1. 3.13之前

```
add_library( MyTarget SHARED )
target_sources ( MyTarget
    PRIVATE    src/A.cpp
               src/B.cpp
               headers/B.hpp
    PUBLIC     ${CMAKE_CURRENT_SOURCE_DIR}/headers/A.hpp
    INTERFACE  ${CMAKE_CURRENT_SOURCE_DIR}/headers/C.hpp
)
```

1. 3.13之后生成绝对路径

```
add_library( MyTarget SHARED )
target_sources ( MyTarget
    PRIVATE    src/A.cpp
               src/B.cpp
               headers/B.hpp
    PUBLIC     headers/A.hpp
    INTERFACE  headers/C.hpp
)
```

## CMakeLists.txt
1. top level CMakeLists.txt begining:

```
cmake_minimum_required( VERSION 3.15...3.17 )

set( CMAKE_PROJECT_INCLUDE_BEFORE
     "${CMAKE_CURRENT_LIST_DIR}/common-project-info.in" )
# include( "${CMAKE_CURRENT_LIST_DIR}/common-project-include.in" )

project (MyRootProject
    VERSION ${project_version}
    DESCRIPTION ${project_description}
    HOMEPAGE_URL ${project_homepage}
    LANGUAGES C CXX )

```

```
# common-project-info.in

set ( project_version 1.2.3 )
set ( project_description "test...." )
set ( project_homepage "https://www...." )
```

## find_package
1. find_package采用两种模式搜索库：
    - `Module模式`：搜索CMAKE_MODULE_PATH指定路径下的FindXXX.cmake文件，执行该文件从而找到XXX库。其中，具体查找库并给XXX_INCLUDE_DIRS和XXX_LIBRARIES两个变量赋值的操作由FindXXX.cmake模块完成。
    - `Config模式`：搜索XXX_DIR指定路径下的XXXConfig.cmake文件，执行该文件从而找到XXX库。其中具体查找库并给XXX_INCLUDE_DIRS和XXX_LIBRARIES两个变量赋值的操作由XXXConfig.cmake模块完成。
1. 两种模式看起来似乎差不多，不过cmake默认采取Module模式，如果Module模式未找到库，才会采取Config模式。如果XXX_DIR路径下找不到XXXConfig.cmake文件，则会找/usr/local/lib/cmake/XXX/中的XXXConfig.cmake文件。总之，Config模式是一个备选策略。通常，库安装时会拷贝一份XXXConfig.cmake到系统目录中，因此在没有显式指定搜索路径时也可以顺利找到。

## pkg-config
1. 如果find_package找不到库，如果系统中有库的.pc配置文件，可以使用pkg-config替代。

``` cmake
find_package(glog QUIET)
if (NOT glog_FOUND)
    find_package(PkgConfig)
    pkg_search_module(PKG_GLOG REQUIRED IMPORTED_TARGET GLOBAL libglog)
    add_library(glog::glog ALIAS PkgConfig::PKG_GLOG)
endif(NOT glog_found)
```

## [组件变量](https://docs.espressif.com/projects/esp-idf/zh_CN/v3.3/api-guides/build-system-cmake.html#preset-component-variables)
1. `COMPONENT_NAME`：组件名，与组件目录名相同。

## Links
1. [Cmake Tutorial](https://cmake.org/cmake/help/v3.19/guide/tutorial/)
2. [Cmake Forum](https://discourse.cmake.org/)
3. [Professional CMake pdf](https://github.com/jiaxiyang/documents/blob/master/pcmake.pdf)
4. [More Modern CMake](https://hsf-training.github.io/hsf-training-cmake-webpage/)
5. [Cmake Buildsystem](https://cmake.org/cmake/help/latest/manual/cmake-buildsystem.7.html)
6. [Effective Modern Cmake](https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1)
7. [Effective Modern Cmake video](https://www.youtube.com/watch?v=bsXLMQ6WgIk)
8. [Deniz Bahadir 2019](https://www.youtube.com/watch?v=y9kSr5enrSk)
9. [Deniz Bahadir 2018 traditional and modern camke](https://www.youtube.com/watch?v=y7ndUhdQuU8)
10. [Beniz Bahadir PPT](https://github.com/Bagira80/More-Modern-CMake)
11. [OO Cmake](https://zhuanlan.zhihu.com/p/76975231)
12. [Cmake Concept](https://ukabuer.me/blog/more-modern-cmake)
