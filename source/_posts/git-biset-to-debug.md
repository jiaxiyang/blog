---
title: Git bisect to debug
date: 2021-03-05 09:51:13
categories:
- Tools
- Git
tags:
- Git
---

## Function
1. Use binary search to find the commit that introduced a bug

## Command

```
$ git bisect start
$ git bisect bad                 # Current version is bad
$ git bisect good v2.6.13-rc2    # v2.6.13-rc2 is known to be good
$ git bisect log
$ git bisect skip                 # Current version cannot be tested
$ git bisect reset

# run script
$ git bisect run my_script arguments
$ cat ~/test.sh
#!/bin/sh
make || exit 125                     # this skips broken builds
~/check_test_case.sh                 # does the test case pass?
$ git bisect start HEAD v1.3.1 --      # HEAD is bad, v1.2 is good
$ git bisect run ~/test.sh
# git bisect run sh -c "make || exit 125; ~/check_test_case.sh"
$ git bisect reset                   # quit the bisect session
```


## Links
1. [git bisect](https://git-scm.com/docs/git-bisect)
1. [Git 二分调试法，火速定位疑难Bug](https://juejin.cn/post/6844903537860673544)
