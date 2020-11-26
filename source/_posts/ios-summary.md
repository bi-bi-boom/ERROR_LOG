---
title: iOS 基础总结
date: 2020-11-18 12:59:51
categories:
    - [iOS, 基础]
tags:
    - "author: cloxnu"
    - Swift
    - Objective-C
---


## GCD
* Grand Central Dispatch (GCD) 是异步执行任务的技术之一。开发者只需定义像执行的任务并追加到适当的 Dispatch Queue 中，GCD 就能生成必要的线程并计划执行任务。
* **为什么需要长时间处理的任务应该在其他线程进行？** 主线程是用来描绘用户界面、处理触摸屏幕的，如果在主线程执行长时间处理的任务，会妨碍主线程中被称为 RunLoop 的主循环的执行，从而导致不能更新用户界面、应用程序的画面长时间停滞。
<!-- More -->
* Serial Dispatch Queue 是等待现在执行中处理
* Concurrent Dispatch Queue 是不等待现在执行中处理
* Serial Dispatch Queue 虽然可以使用 `dispatch_queue_create` 生成无数个线程，就可以并行执行，但是大量生成会使系统响应性能大幅度降低，Serial Dispatch Queue 主要用来避免数据竞争
* Main Dispatch Queue 在主线程执行，更新用户界面必须在主线程执行，类型是 Serial Dispatch Queue
* Global Dispatch Queue 是所有应用程序都能够使用的 Concurrent Dispatch Queue，有高、默认、低、后台四个优先级
* `dispatch_after` 在指定时间追加处理到 Dispatch Queue
* Dispatch Group 可以用 `dispatch_group_notify` 或 `dispatch_group_wait` 等待 Dispatch Group 执行结束
* `dispatch_barrier_async` 会等待追加到 Concurrent Dispatch Queue 上的并行执行的处理全部结束后，再将指定的处理追加到该 CDQ 中。然后处理完后，再去处理后面的 CDQ
* `dispatch_apply` 用来按指定次数将指定的 block 追加到指定的 Dispatch Queue 中
* `dispatch_once` 保证只执行一次

## 内存管理
* 自动引用计数 ARC Automatic Reference Counting 内存管理中对引用采取自动计数的技术
	1. 自己生成的对象，自己所持有 `NSObject * __strong obj = [[NSObject alloc] init];`
	2. 非自己生成的对象，自己也能持有 `NSMutableArray * __strong array = [NSMutableArray array];`
	3. 不再需要自己持有的对象时释放
	4. 非自己持有的对象无法释放
> 生成并持有对象：`alloc/new/copy/mutablecopy` 等   
> 持有对象：`retain`  
> 释放对象：`release`  
> 废弃对象：`dealloc`  
*  「strong」对应所有权类型是 `__strong` 指向并持有对象，引用计数会+1，引用计数为 0 才会销毁，为 nil 会销毁
* 「weak」对应所有权类型是 `__weak` 指向但不持有对象，引用计数不会+1
* 「__unsafe_unretained」和 weak 类似，不同的是弱引用的对象废弃后此对象不会被赋值为 nil，为悬垂指针，继续方法可能会导致访问错误
* 「assign」对应所有权类型是 `__unsafe_unretained` 修饰基本数据类型，存储在栈中
* 「copy」对应所有权类型是 `__strong` 和 strong 类似，多用于修饰有可变类型的不可变对象
* 「__autoreleasing」与直接调用 autorelease 方法等价，前提是用 @autorelease 块替换 NSAutoreleasePool
* 「__strong」修饰符是 id 类型和对象类型默认的所有权修饰符，而「__autoreleasing」是 id 的指针或对象的指针默认的所有权修饰符
* `NSZone` 为了防止内存碎片化

