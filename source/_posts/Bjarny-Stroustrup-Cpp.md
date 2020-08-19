---
title: Bjarny Stroustrup talk about cpp
date: 2020-08-18 09:34:33
categories:
- Program
- Cpp
tags:
- Cpp
---

## What is C++20?
1. The best approximation of C++'s ideals so far.
1. As big an improvement over C++11 as C++11 was over C++98: A major "release"
1. Lots of useful features
   - Simpler, more expressive, faster code that compiles faster
   - Modeles
   - Concepts
   - Coroutines
   - Ranges
   - Dates
   - Span
   - Better compile-time programing support
   - Many "minor features"
1. C++23 and C++26 is better than C++20, not the major "release".
1. Diretly learn C++20. It's the outside layer of the onion.
1. C++23:
   - "Completes C++20"
   - Plus: standard modules, library support for coroutines, executors & networking
   - Maybe: static reflection, pattern matching

## Keys C++ "Rules of Thumb"
1. `A static type system` with equal support for build-in and user-defined types
   - A type: specifies the set of operations that can be applied to an object and specifies how an object is laid out in memory
   - A static type system: the base of all
   - static mean compile time will determine all the type(not the run-time).
   - compile-time error detection
   - performance
   - flexibility through compile-time resolution(overloading, generic programming, metaprogramming...)
1. `Value and reference semantics`
   - value types: Inegers, characters, strings, containers,...
   - Pointers/references: T*, T&, unique_ptr<T>, Forward_iterator
1. `Direct use` of machine and operating system resources
   - bitset and span(modern c++)
   - the onion principle: the more layers you peel off, the more control, the more error.
1. Systematic and general `resource management`(RALL)
   - manage heap, file...
   - every resource must have an owner: responsible for its cleanup.
   - control the complete object life cycle: creation, copy, move, destruction
1. Support `composition` of software from separately developed parts.
   - modules
   - all major features support composition: moduls, classes, concepts, templates, functions, aliases
1. Support for `object-oriented programming`
1. Support for `generic programming`
   - concepts
1. Support `compile-time programming`
   - Move computation from run-time to compile-time(performace, do once)
   - It's everywhere: overloading and virtual functions, templates, variadic templates, constexp functions...
1. `Concurency` through libraries supported by intrinsics
1. `Libraries`
   - A user shouldn't have to care whether a feature is implemented in the language or in a library

## Philosophy (CppCoreGuidelines)
1. Express ideas directly in code
1. Write in ISO Stardard C++
1. Express intent
1. Ideally, a program should be statically type safe.
1. Prefer compile-time checking to run-time checking.
1. What cannot be checked at compile time should be checkable at run time
1. Catch run-time errors early.
1. Don't leak any resources.
1. Don't waste time or space.
1. Prefer immutable data to mutable data
1. Encapsulate messy constructs, rather than spreading through the code.
1. Use supporting tools as appropriate
1. Use support libraries as appropriate

## Lower levels of abstaction
1. Samples:
   - Sizes
   - Raw pointers
   - Allocation and deallocation
   - Loop-control variables
   - Casts
   - Macros
1. Except as implementation details and asides
1. Don't go to lower level if you have to.

## What really matters?
1. People
1. A programming language is a tool, not an end goal: peopeo want great systems, not programming languages.
1. Software developers want great tools: not just programming language features.

## Abstraction
1. Often, the software is more complicated than the hardware.
1. abstraction in code:
   - resource mangement: vector
   - generic programing: concepts: compile-time predicates.

## The onion principle
1. Mangagement of complexity: make simple thing simple.
1. Layers of abstraction: the more layers you peel off, the more you cry.

## An engineering approach
1. Design c++ is not pure math.
1. Principled and pragmatic design
1. Progress gradually guided by feedback
1. There are always many tradeoffs: choosing is hard
1. Design decisions have consequences

## C++ in two lines
1. Direct map to hardware
   - of instructions and fundamental data types
   - initially from C
   - Future: use novel hardware better(caches, multicores, GPUs, FPGAs, SIMD, ...)
1. Zero-overhead abstraction
   - classes, inheritance, generic programming, ...
   - initially from Simula(where it wasn't zero-overhead)
   - Future: Type- and resouce-safety, concepts, modules, concurrency, ...

## C++'s role
1. A language for
   - writing elegant and efficiaent programs
   - for definning and using light-weight abstractions
   - a language for resource-constrained applications
   - building software infrastructure
1. Offers
   - a direct map to hardware
   - Zero-overhead abstraction
1. No language is perfect
   - for everthing
   - for everyone

## C++ is tunable
1. Make simple things simple
   - Don't make complicated tasks impossible
   - Don't make complicated tasks unreasonable hard to do
   - The onion principle
1. Don't drop to lower levels of abstraction
   - Unless you really, really need to
   - Hide messy code behind clean interfaces
1. Alwasy measure

## Write better code
1. Cleaner
2. Simpler
3. More readable
4. More maintainable
5. Faster
6. Less clever
7. More general
8. More usable and re-usable
9. Type safe
