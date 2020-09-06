---
title: iOS 多线程
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
keywords: 多线程
description: 
passwords:
img:
abstract: 多线程GCD是异步执行任务的技术之一，定义了任务与队列。
---

# 1.多线程
什么是多线程（进程）？
本质可以认为是CPU分时调度某些任务，看起来是并行执行，其实是并发执行。而多线程还是多进程是技术实现层面。

多线程与多进程-依据使用场景定方案，没有最优
[推荐这篇](https://blog.csdn.net/leolinsheng/article/details/12979473)

# 2.GCD API
## 1.Dispatch Queue
串行队列
并发队列

## 2.dispath_queue_create
创建队列

## 3.主队列与全局并发队列

## 4.dispatch_get_target_queue
设置执行层次

## 5.dispatch_after
延迟执行

## 6.dispatch group
队列成组

## 7.dispatch_barrier_async
队列分隔

## 8.dispatch_sync
同步任务

## 9.dispatch_apply
group+sync

## 10.dispatch_suspend dispatch_resume
挂起与恢复

## 其他
dispatch_semaphore
dispatch_once
dispatch io

# 3.GCD本质
> 队列 + 排他控制的信号 + 管理线程的容器 + 内核（XNU）