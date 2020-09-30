---
title: Emacs on Windows10
date: 2020-09-30 08:05:00
categories:
- Tools
- Emacs
tags:
- Emacs
---

## Install msys2 on windindows
1. [Tsing hua source](https://mirrors.tuna.tsinghua.edu.cn/msys2/distrib/x86_64/)
1. [Official web](https://www.msys2.org/)

## Config msys2
1. Theme: dracula
1. Font: Consolas 14
1. Transparency: Medium
1. Right mouse: paste
1. Terminal Type: xterm-256color
1. Cursor: bold, not blinking

## Install git vim oh-my-zsh emacs
1. [Tutorial](https://blog.csdn.net/u013938484/article/details/83539008)
1. Note: Change package source. No vim at first, you can edit the file on windows
1. Emacs install: `pacman -S mingw-w64-x86_64-emacs`
1. Libs install: `pacman -S mingw-w64-x86_64-libpng && pacman -S mingw-w64-x86_64-libjpeg-turbo`
1. Config .bashrc and .zshrc

## Build emacs plugins in Ubuntu on VMvare
1. [100ms emacs](https://github.com/jiaxiyang/100ms_dot_emacs)
1. build and copy the tar package to msys2
1. install package on msys2
