---
title: How to start writing blog
date: 2020-06-26 14:52:10
categories:
- tools
- blog
tags:
- blog
---

## Set up githubio
1. Follow [github pages guide](https://guides.github.com/features/pages/) to apply a web.

## Use hexo (or JylyII)
1. [ubuntu16.04 nodejs install](https://github.com/nodesource/distributions/blob/master/README.md)
   * Need sudo to use npm install packages.
   * [npm install error solve](https://www.jianshu.com/p/3fd7d90db01a)
2. [hexo tutorial](https://hexo.io/zh-cn/)
3. [hexo theme 3-hexo](https://github.com/yelog/hexo-theme-3-hexo)
4. [3-hexo tutorial](https://yelog.org/2017/03/23/3-hexo-instruction/)

## Write blog
1. [markdown tutorial](https://guides.github.com/features/mastering-markdown/)

## Push blog to githubio
1. [hexo tutorial](https://hexo.io/zh-cn/docs/one-command-deployment)

## Hexo basic comamnd
1. Create a new post
``` bash
$ hexo new "My New Post"
```

2. Run server
``` bash
$ hexo server
```

3. Generate static files
``` bash
$ hexo generate
```

4. Deploy to remote sites
``` bash
$ hexo clean && hexo deploy
```
5. shortcuts
``` bash
alias hs='hexo clean && hexo g && hexo s'
alias hd='hexo clean && hexo g && hexo d && git add . && git commit -m "update" && git push -f'
```
