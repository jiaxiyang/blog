---
title: Clang-format-usage
date: 2020-07-01 13:16:38
categories:
- Tools
- Vim
tags:
- Clang format
- Vim
- Emacs
---

## Install clang
1. [Build clang from source](http://clang.llvm.org/get_started.html)
1. [Clang format doc](http://clang.llvm.org/docs/ClangFormat.html)

## Bash Command
1. Format one cpp file:
`clang-format --style=Google -i test.cpp`
2. Format all cpp files:
`fd ".cpp$" | xargs clang-format --style=Google -i`

## Vim Config
1. Find clang-format.py in your system and copy the file path.

``` shell
 ~ : find /usr -iname "clang-format.py"
/usr/local/share/clang/clang-format.py
```

2. Put the following config in your .vimrc. It will automaticly format the c++ file when the file is saved.

```
function! Formatonsave()
    let l:lines = 'all'
    let l:formatdiff = 1
    let g:clang_format_fallback_style = 'Google'
    " Remember to repalce the path of clang-format.py
    pyfile /usr/local/share/clang/clang-format.py
    " py3file /usr/local/share/clang/clang-format.py
endfunction
autocmd BufWritePre *.h, *.hpp, *.cc, *.cpp call Formatonsave()

```

## Emacs Config
1. use package config

``` emacs-lisp
(use-package clang-format
  :after (cc-mode)
  :config
  (set-default 'clang-format-fallback-style "Google")
  (add-hook 'c-mode-common-hook #'(lambda()
                                    (add-hook 'before-save-hook
                                              'clang-format-buffer t t))))
```
