---
title: Kalman Filters
date: 2021-01-30 11:43:37
categories:
- Algorithm
- Kalman
tags:
- Filters
---

## Concept
1. 卡尔曼滤波是一个递归的`估计`，只要获知`上一时刻的状态估计`和`当前状态的观测`就可以计算`当前状态的估计`。
1. 卡尔曼滤波器不需要观测/估计的历史记录。
1. 卡尔曼滤波器是一个纯粹的`时域滤波器`，而不像低通滤波器那样，需要在频率设计，然后转到时域应用。
1. 两个阶段：
   - `预测`：由上一状态的估计做出对当前状态的估计
   - `更新`：利用当前状态的观测值`优化`预测阶段的估计值，以获取一个`更精确的当前状态估计`
1. 两种数据：
   - `估计值`
   - `观测值`：传感器测量值，如GPS位置。
1. 线性系统与非线性系统：
   - 判断标准：能不能通过上一次系统估计状态直接乘以某个矩阵得到预测状态？ 矩阵都是具体的值，与估计状态相乘后只是估计状态的线性变换。（还是测量状态不能直接与估计状态求差？）
   - `线性系统`： 预测状态 = F * 上一次估计状态。例如：预测汽车位置，传感器获得位置值，假设很短时间内，系统是匀速运动或匀加速运动（对应两种模型）。可以通过上一时刻状态乘以矩阵得到预测值。
   - `非线性系统`：预测状态不能直接由上一次估计状态乘以一个矩阵得到。 如雷达跟踪飞机，估计状态为(x, y). 测量状态为径向距离r和夹脚。

## Formulas
1. ![5 basic formulas](/images/kalman/formulas.jpg)

## links
1. [Kalman-and-Bayesian-Filters-in-Python](https://github.com/rlabbe/Kalman-and-Bayesian-Filters-in-Python)
1. [Using in car](https://blog.csdn.net/codesamer/article/details/81191487)
1. [基于Kalman滤波器的进行物体的跟踪](https://www.jianshu.com/p/d51a3a7736ca)
1. [图说卡尔曼滤波](https://zhuanlan.zhihu.com/p/39912633)
1. [Youtube Matlab tutorial](https://www.youtube.com/watch?v=VFXf1lIZ3p8)
