---
title: iOS Runloop
categories: 
- [技术, 移动端]
tags: [iOS]
copyright: true
comments: true
top: false
author: XQ
mathjax: false
date: 2020-09-06 00:34:03
updated: 2020-09-06 00:34:06
keywords: Runloop
description: 
passwords:
img:
abstract: 理解Runloop就是理解了多线程模型
---

# 1.Runloop基本概念
本质是一种循环，只是这种循环包含了事件响应与智能休眠。
Runloop与线程是一一对应的的，不能创建，但可以获取当前线程的Runloop对象。
主线程默认启动Runloop对象。

# 2.事件源 + Observer
input source + timer source
对观察者的状态通知

# 3.Runloop Mode
是事件源与观察者的集合，Runloop可以包含多个Mode，但是同一时刻只能跑一个Mode，处理Mode内的source、timer、observer
iOS 中公开暴露出来的只有 NSDefaultRunLoopMode 和 NSRunLoopCommonModes。 NSRunLoopCommonModes 实际上是一个 Mode 的集合，默认包括 NSDefaultRunLoopMode 和 NSEventTrackingRunLoopMode。


# 参考
[Runloop](https://hit-alibaba.github.io/interview/iOS/ObjC-Basic/Runloop.html)
[深入理解RunLoop](https://blog.ibireme.com/2015/05/18/runloop/)