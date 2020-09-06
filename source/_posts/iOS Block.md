---
title: iOS Block
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
keywords: Block
description: 
passwords:
img:
abstract: Block 本质是结构体对象，通过生成指定结构体实现变量捕获与函数调用
---
Block是C语言的扩充，是带有自动变量的匿名函数。类似于指针函数。

# 1.定义方式
返回值类型 (^Block名称)(参数列表) = ^ 返回值类型 (参数列表) {}
int (^blockName)(...) = ^(...) {}

为了方便使用 typedef int (^BlockName)(...)

# 2.变量捕获
一般是值的捕获，在block结构体中形成一个值，无法更改
添加_block修饰符后，是地址的获取，在block结构体形成了一个指向另一个结构体的指针，可以修改

# 3.Block本质
objc->c

未添加__block
``` c
#import <Foundation/Foundation.h>

int main(int argc, char *argv[]) {
	@autoreleasepool {
		int a = 10;
		void (^block)(void) = ^(void){printf("%d", a);};
		block();
		return 0;
	}
}


#ifndef BLOCK_IMPL
#define BLOCK_IMPL
struct __block_impl {
  void *isa;
  int Flags;
  int Reserved;
  void *FuncPtr;
};


struct __main_block_impl_0 {
  struct __block_impl impl;
  struct __main_block_desc_0* Desc;
  int a;
  __main_block_impl_0(void *fp, struct __main_block_desc_0 *desc, int _a, int flags=0) : a(_a) {
    impl.isa = &_NSConcreteStackBlock;
    impl.Flags = flags;
    impl.FuncPtr = fp;
    Desc = desc;
  }
};
static void __main_block_func_0(struct __main_block_impl_0 *__cself) {
  int a = __cself->a; // bound by copy
printf("%d", a);}

static struct __main_block_desc_0 {
  size_t reserved;
  size_t Block_size;
} __main_block_desc_0_DATA = { 0, sizeof(struct __main_block_impl_0)};
int main(int argc, char *argv[]) {
 /* @autoreleasepool */ { __AtAutoreleasePool __autoreleasepool; 
  int a = 10;

  void (*block)(void) = ((void (*)())&__main_block_impl_0((void *)__main_block_func_0, &__main_block_desc_0_DATA, a));

  ((void (*)(__block_impl *))((__block_impl *)block)->FuncPtr)((__block_impl *)block);

  return 0;
 }
}

```
添加__block
``` c
#import <Foundation/Foundation.h>

int main(int argc, char *argv[]) {
	@autoreleasepool {
		__block int a = 10;
		void (^block)(void) = ^(void){printf("%d", a);};
        block();
		return 0;
	}
}

#ifndef BLOCK_IMPL
#define BLOCK_IMPL
struct __block_impl {
  void *isa;
  int Flags;
  int Reserved;
  void *FuncPtr;
};


struct __Block_byref_a_0 {
  void *__isa;
__Block_byref_a_0 *__forwarding;
 int __flags;
 int __size;
 int a;
};

struct __main_block_impl_0 {
  struct __block_impl impl;
  struct __main_block_desc_0* Desc;
  __Block_byref_a_0 *a; // by ref
  __main_block_impl_0(void *fp, struct __main_block_desc_0 *desc, __Block_byref_a_0 *_a, int flags=0) : a(_a->__forwarding) {
    impl.isa = &_NSConcreteStackBlock;
    impl.Flags = flags;
    impl.FuncPtr = fp;
    Desc = desc;
  }
};
static void __main_block_func_0(struct __main_block_impl_0 *__cself) {
  __Block_byref_a_0 *a = __cself->a; // bound by ref
printf("%d", (a->__forwarding->a));}
static void __main_block_copy_0(struct __main_block_impl_0*dst, struct __main_block_impl_0*src) {_Block_object_assign((void*)&dst->a, (void*)src->a, 8/*BLOCK_FIELD_IS_BYREF*/);}

static void __main_block_dispose_0(struct __main_block_impl_0*src) {_Block_object_dispose((void*)src->a, 8/*BLOCK_FIELD_IS_BYREF*/);}

static struct __main_block_desc_0 {
  size_t reserved;
  size_t Block_size;
  void (*copy)(struct __main_block_impl_0*, struct __main_block_impl_0*);
  void (*dispose)(struct __main_block_impl_0*);
} __main_block_desc_0_DATA = { 0, sizeof(struct __main_block_impl_0), __main_block_copy_0, __main_block_dispose_0};
int main(int argc, char *argv[]) {
 /* @autoreleasepool */ { __AtAutoreleasePool __autoreleasepool; 
  __attribute__((__blocks__(byref))) __Block_byref_a_0 a = {(void*)0,(__Block_byref_a_0 *)&a, 0, sizeof(__Block_byref_a_0), 10};

  void (*block)(void) = ((void (*)())&__main_block_impl_0((void *)__main_block_func_0, &__main_block_desc_0_DATA, (__Block_byref_a_0 *)&a, 570425344));

  ((void (*)(__block_impl *))((__block_impl *)block)->FuncPtr)((__block_impl *)block);

  return 0;
 }
}


```
