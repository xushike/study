# goroutine

# 一 概述
golang的goroutine笔记，因为内容复杂，所以单独弄一个笔记。

# 三 基础

## 1 线程的状态
阻塞

## 1 sync.WaitGroup
作用：它能够一直等到所有的goroutine执行完成，并且阻塞主线程的执行，直到所有的goroutine执行完成

# 四 高级
## 1 go的线程模型
三个核心元素支撑起了这个模型的主框架：
- M：machine的缩写。一个M代表一个内核线程，或者“工作线程”。
- P：processor的缩写。一个P代表执行一个Go代码片段所必需的资源（或称“上下文环境”）。
- G：goroutine的缩写。一个G代表一个Go代码片段。前者是对后者的一种封装。

## 2 go的CSP并发模型
CSP模型：是上个世纪七十年代提出的，用于描述两个独立的并发实体通过共享的通讯 channel(管道)进行通信的并发模型。 CSP中channel是第一类对象，它不关注发送消息的实体，而关注与发送消息时使用的channel

CSP

哲学：不要通过共享内存来通信， 应该通过通信来共享内存。

# 六 问题

# 七 未整理
1. 死锁，活锁，优先级反转
2. 基于内存共享和基于消息共享内存的对比