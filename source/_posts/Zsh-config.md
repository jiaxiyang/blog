---
title: Zsh config
date: 2020-07-22 15:19:28
categories:
- Tools
- Zsh
tags:
- Zsh
---

## oh my zsh

``` shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## autosuggestions

 ``` shell
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
vi ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh 文件，修改 ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=blue'
# support colors: black, red, green; yellow; blue; magenta; cyan and white;
```

## zsh-syntax-highlighting

``` shell
git clone git://github.com/jimmijj/zsh-syntax-highlighting ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

## .zshrc config

``` shell
export PROMPT="%n@%m:%1~%# "
plugins=(rust rustup cargo zsh-autosuggestions zsh-syntax-highlighting)
```

## Othe config

``` shell
git config oh-my-zsh.hide-status 1 --global #close git status
```

## Powlevel9k theme

```
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
.zshrc：
export TERM="xterm-256color"
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(user dir)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(root_indicator background_jobs )
POWERLEVEL9K_MODE='awesome-fontconfig'
ZSH_THEME="powerlevel9k/powerlevel9k"
~/.oh-my-zsh/custom/themes/powerlevel9k/powerlevel9k.zsh-theme          修改  "CONTENT"             "jia@61" #"$(whoami)"
```

## awesome-terminal-fonts

``` shell
git clone https://github.com/gabrielelana/awesome-terminal-fonts
cp -R build/* ~/.fonts/
fc-cache -fv ~/.fonts
cp config/10-symbols.conf ~/.config/fontconfig/conf.d
source ~/.fonts/*.sh
```

## autojump

 ``` shell
git clone git://github.com/joelthelion/autojump.git
cd autojump
./install.py
 ```

## powerline(非必须）

``` shell
sudo apt-get install fonts-powerline
git clone https://github.com/powerline/fonts.git --depth=1
cd fonts
./install.sh
```

## Links
install oh my zsh :         sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
zsh autosuggestions     https://note.youdao.com/web/#/file/WEB35aa360d3643be282ab89890d39646cf/note/WEBa075b0a3e60cbde5f506563c3c14997a/
sudo apt-get install autojump  https://note.youdao.com/web/#/file/WEB35aa360d3643be282ab89890d39646cf/note/WEB1da9f35b71c3815439e1426116e7ecf9/
Powlevel9k  theme install     https://note.youdao.com/web/#/file/WEB35aa360d3643be282ab89890d39646cf/note/WEBfd1ecc9886dfcf108ee9bae6b586cab6/
Powerline      https://note.youdao.com/web/#/file/WEB35aa360d3643be282ab89890d39646cf/note/WEBac4ed9c8ab78bb09940458cfb9b1a397/
awesome-terminal-fonts   http://www.cnblogs.com/weixuqin/p/7029177.html
zsh-syntax-highlighting  https://note.youdao.com/web/#/file/WEB35aa360d3643be282ab89890d39646cf/note/WEBef4ca4fdaf7d36950545241429e3daee/
