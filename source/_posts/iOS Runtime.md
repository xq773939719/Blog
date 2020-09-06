---
title: iOS Runtime
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
keywords: Runtime
description: 
passwords:
img:
abstract: Runtime 又叫运行时，是一套底层的 C 语言 API，是 iOS 系统的核心之一。开发者在编码过程中，可以给任意一个对象发送消息，在编译阶段只是确定了要向接收者发送这条消息，而接受者将要如何响应和处理这条消息，那就要看运行时来决定了。
---

# 1.Runtime是什么
C语言中，在编译期，函数的调用就会决定调用哪个函数。
而OC的函数，属于动态调用过程，在编译期并不能决定真正调用哪个函数，只有在真正运行时才会根据函数的名称找到对应的函数来调用。

Objective-C 是一个动态语言，这意味着它不仅需要一个编译器，也需要一个运行时系统来动态得创建类和对象、进行消息传递和转发。

TODO
# 参考
[神经病院 Objective-C Runtime 入院第一天—— isa 和 Class](https://halfrost.com/objc_runtime_isa_class/)