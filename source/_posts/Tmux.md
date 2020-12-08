---
title: Tmux config
date: 2020-12-7 15:19:28
categories:
- Tools
- Tmux
tags:
- Tmux
---

## Tmux config

``` shell
# use mouse to scroll history
set -g mouse on        #For tmux version 2.1 and up
# set -g mode-mouse on   #For tmux versions < 2.1

# set history lenth
set -g history-limit 15000

# change prefix key
set -g prefix C-t
unbind C-b
bind C-t send-prefix
```

## Reload config

``` shell
tmux source-file ~/.tmux.conf
```
