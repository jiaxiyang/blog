---
title: FFmpeg
date: 2021-02-23 20:21:13
categories:
- Program
- FFmpeg
tags:
- FFmpeg
---

## [视频处理基本概念](https://www.ruanyifeng.com/blog/2020/01/ffmpeg.html)
1. `容器`：`ffmpeg -formats` 视频文件本身其实是一个容器（container），里面包括了视频和音频，也可能有字幕等其他内容。
1. `编码格式`：`ffmpeg -codecs` 视频和音频都需要经过编码，才能保存成文件。不同的编码格式（CODEC），有不同的压缩率，会导致文件大小和清晰度的差异。
2. `编码器`：`ffmpeg -encoders` 编码器（encoders）是实现某种编码格式的库文件。只有安装了某种格式的编码器，才能实现该格式视频/音频的编码和解码。

## ffmpeg命令
1. 总共分为5部分：`ffmpeg {1} {2} -i {3} {4} {5}`

```
$ ffmpeg \
[全局参数] \
[输入文件参数] \
-i [输入文件] \
[输出文件参数] \
[输出文件]
```


## Links
1. [Official Documents](https://ffmpeg.org/documentation.html)
1. [FFmpeg从入门到精通（书）](http://jxz1.j9p.com/pc/dgsdfhghgh.pdf)
