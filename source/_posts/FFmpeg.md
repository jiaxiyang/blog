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
1. `容器(封装)`：`ffmpeg-formats` 视频文件本身其实是一个容器（container），里面包括了视频和音频，也可能有字幕等其他内容。
1. `编码格式`：`ffmpeg-codecs` 视频和音频都需要经过编码，才能保存成文件。不同的编码格式（CODEC），有不同的压缩率，会导致文件大小和清晰度的差异。
2. `编码器`：`ffmpeg-encoders` 编码器（encoders）是实现某种编码格式的库文件。只有安装了某种格式的编码器，才能实现该格式视频/音频的编码和解码。

## 工作流程
1. ffmpeg的主要工作流程相对比较简单，具体如下。
  - 解封装（Demuxing）
  - 解码（Decoding）
  - 编码（Encoding）
  - 封装（Muxing）
1. 其中需要经过6个步骤，具体如下。
  - 读取输入源
  - 进行音视频的解封装
  - 解码每一帧音视频数据
  - 进行音视频的重新封装
  - 输出到目标
1. 
                _______              ______________
               |       |            |              |
               | input |  demuxer   | encoded data |   decoder
               | file  | ---------> | packets      | -----+
               |_______|            |______________|      |
                                                          v
                                                      _________
                                                     |         |
                                                     | decoded |
                                                     | frames  |
                                                     |_________|
                ________             ______________       |
               |        |           |              |      |
               | output | <-------- | encoded data | <----+
               | file   |   muxer   | packets      |   encoder
               |________|           |______________|

## ffmpeg
1. FFmpeg框架的基本组成包含AVFormat、AVCodec、AVFilter、AVDevice、AVUtil等模块库
1. 主要命令
  - ffmpeg主要用于音视频编解码
  - ffprobe主要用于音视频内容分析
  - ffplay主要用于音视频播放、可视化分析

### ffmpeg
1. 总共分为5部分：`ffmpeg {1} {2} -i {3} {4} {5}`

```
$ ffmpeg \
[全局参数] \
[输入文件参数] \
-i [输入文件] \
[输出文件参数] \
[输出文件]
```

### ffplay
1. FFmpeg不但可以提供转码、转封装等功能，同时还提供了播放器相关功能，使用FFmpeg的avformat与avcodec，可以播放各种媒体文件或者流。如果想要使用ffplay，那么系统首先需要有SDL来进行ffplay的基础支撑。

### ffprobe
1. ffprobe也是FFmpeg源码编译后生成的一个可执行程序。ffprobe是一个非常强大的多媒体分析工具，可以从媒体文件或者媒体流中获得你想要了解的媒体信息，比如音频的参数、视频的参数、媒体容器的参数信息等。
2. `./ffprobe –show_streams output.mp4`

## Links
1. [Official Documents](https://ffmpeg.org/documentation.html)
1. [FFmpeg从入门到精通（书）](http://jxz1.j9p.com/pc/dgsdfhghgh.pdf)
