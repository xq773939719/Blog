---
title: iOS 内存管理
categories: 
- [技术, 移动端]
tags: [iOS]
copyright: true
comments: true
top: false
author: XQ
mathjax: false
date: 2020-09-06 12:43:32
updated: 2020-09-06 12:43:36
keywords: 内存管理
description: 
passwords:
img:
abstract: 软件开发的重中之重-内存
---

引用计数的本质就是对象中保留的一个对使用者计数的区域而已。

# 1.引用计数

引用计数的思考方式：
①自己生成自己持有
②非自己生成，自己能持有
③不需要时释放
④非自己持有的的对象无法释放

# 2.自动引用计数
所有权修饰符
``` objective-c
__strong // 强引用
__weak // 弱引用 自动nil
__unsafe_unretained // 非安全的弱引用 非自动nil
__autoreleasing // 加入autoreleaspool
```
属性->修饰符
assign unsafe_unretained -> __unsafe_unretained

copy retain strong -> __strong

weak -> __weak