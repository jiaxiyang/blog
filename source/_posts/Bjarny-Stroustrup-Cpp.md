---
title: Bjarny Stroustrup talk about cpp
date: 2020-08-18 09:34:33
categories:
- Program
- Cpp
tags:
- Cpp
---

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
