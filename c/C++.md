# 1.c++
[TOC]
# 一 概述
## 1 简介
### 1.1 c++和java的主要不同 
1. 内存管理方面:
    >java比C++更易用的重要原因。C++的用户自己管理 
    内存和灵活的指针用法往往让用户为了一个内存问题而调试好几天。让用户自己释放内 
    存使得用户必须非常小心，在程序有多个出口或指针被多个线程或被多个容器拥有的情 
    况下，何时能安全的释放内存都必须非常谨慎的，而且还要保证在程序的各个出口都保 
    证不内存泄露，这简直就是噩梦！智能指针能解决一些问题，但他带来的问题同样很多 
    。java的自动垃圾收集简直就是一大解脱！ 
2. 在网络编程方面:
    >在这方面我更喜欢java，java不愧是靠网络起家，网络编程在java下特别简单。而用C+ 
    +来写网络程序实在是太麻烦了。
3. 在多线程编程方面：
    >更推荐C++。java虽然更简单，但是还不够    
4. C++认为程序的执行效率是最重要的一个问题，所以对象的存储以及存在时间可在编写程序时决定
5. java是单根结构

### 1.4 他人评价
网友：
1. Jinhua Luo：大家都知道C++就是太学术化了，尤其最引工程人诟病的是，对泛型模板搞得太走火入魔了，开发起来首先就要去适应那些嵌套了一层又一层的模板。另外，C/C++的内存泄漏其实还好调试，但C/C++有一点很不好，很恐怖的事情，就是能直接对内存空间做写入，你能直接对某个地址段写入，这样带来的后果是不可预测的，也难以发现。C/C++真的不适合做偏向业务的应用，它的适用场合应该是底层组件，尤其是一些对性能要求高的组件，因为做应用，需要自底向上的概念统一和蓬勃的生态圈。

## 3 常识
### 3.1 关于《C＋＋Primer Plus》与《C++ Primer》
网友：C++ primer plus如果没学过其他的编程语言推荐先看.因为解释很详细.但是没有很深的东西...C++ primer 公认的经典,但是如果基础不行只会打击你的自信心(亲身体验过...)...等对C++有了一定认识的时候一定要看完...如果英文基础好当然是读英文版的比较好

# 二 安装配置

# 三 基础

# 五 经验
## 2 常用包和方法
### 2.1 容器相关
C++ 语言的容器通过标准库提供，如 vector 对应数组，list 对应双链表，map 对应映射等。

### 2.2 asio
asio功能很完备，既支持异步也支持同步

# 七 待整理
1. 记得某位大牛说过，能用c在1000行代码内实现的，不要用C++实现
2. stl模板
