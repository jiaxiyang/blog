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

# key bindings for horizontal and vertical panes
bind | split-window -h
bind \ split-window -h
bind - split-window -v

set -g base-index 1
set-window-option -g pane-base-index 1
set -g renumber-windows on

# reference C-t ?
bind-key -T prefix a select-window -t :=1
bind-key -T prefix s select-window -t :=2
bind-key -T prefix d select-window -t :=3
bind-key -T prefix f select-window -t :=4
bind-key -T prefix g select-window -t :=5
bind-key -T prefix h select-window -t :=6
bind-key -T prefix j select-window -t :=7
bind-key -T prefix k select-window -t :=8
```

## Reload config

``` shell
tmux source-file ~/.tmux.conf
```
