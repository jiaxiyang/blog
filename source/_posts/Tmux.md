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
# more intuitive keybindings for splitting and create window
bind \\ split-window -h -c "#{pane_current_path}"
bind - split-window -v -c "#{pane_current_path}"
bind c new-window -c "#{pane_current_path}"

# display
set -g base-index 1
set-window-option -g pane-base-index 1
set -g renumber-windows on

# set terminal title
set -g set-titles on

# redraw status line every 10 seconds
set -g status-interval 10

# right status: tmux show-options -g | grep status-right
set -g status-right "#{=21:host_short} "

# Remove delay when sending commands
# (default is 500 milliseconds)
set -sg escape-time 1

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

## Tmux Zsh CheatSheet
[https://github.com/ohmyzsh/ohmyzsh/wiki/Cheatsheet](https://github.com/ohmyzsh/ohmyzsh/wiki/Cheatsheet)

``` shell
ta	  : tmux attach -t
tad	  : tmux attach -d -t
ts	  : tmux new-session -s
tl	  : tmux list-sessions
tksv  : tmux kill-server
tkss  : tmux kill-session -t
```
