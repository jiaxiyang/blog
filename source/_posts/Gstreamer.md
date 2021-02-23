---
title: Gstreamer
date: 2021-02-23 08:43:01
categories:
- Program
- Gstreamer
tags:
- Gstreamer
---

## Why Gstreamer
1. 构建一个视频分析应用，需要考虑的内容有：视频流获取、视频流解码、预处理、算法推理、数据编码、数据显示、数据传输等。常常需要引入一些第三方的开发包，如OpenCV，FFmpeg，Caffe，TensorRT，OpenGL等。GStreamer是一个用于开发流式多媒体应用的跨平台开源框架，应用程序可以通过管道(Pipeline)的方式，`将多媒体处理的各个步骤串联起来`，达到预期的效果。

## Gstreamer
1. `核心`为`Pipeline`框架以及用于扩展功能的`Plugins`。
2. 原理：GStreamer的程序通过连接数字媒体处理的元素注入管道（pipeline）。每个元素(element)是由一个插件提供。元素可组合为箱（bins），箱可以进一步聚合，从而形成架构图。元素沟通是透过垫（pads）。来源垫（source pad）上一个元素可以被连接到一个接收垫（sink pad）在另一个。当管道是在播放状态，数据缓冲流（data buffers flow）从来源垫（source pad）流向接收垫（sink pad）。


## Links
1. [Gstreamer tutorials](https://gstreamer.freedesktop.org/documentation/tutorials/basic/index.html?gi-language=c)
1. [Gstreamer tutorials rust](https://github.com/sdroege/gstreamer-rs/tree/master/tutorials)
1. [由GStreamer到DeepStream](http://orangeamoy.com/2019/06/28/GStreamerAndDeepStream/)
