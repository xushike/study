# windows
[TOC]
# 一 概述
## 1 简介
## 2 历史
## 3 常识
### 3.1 用户变量和系统变量  
如果电脑有多个人使用，那就配置用户变量，系统变量影响的是所有用户。

### 3.2 文件路径长度
windows文件路径长度最多只支持260个字符，所以太长的目录可能引起错误

### 3.3 命令行输出到剪切板
使用系统自带的clip命令,用法类似linux
1. 将字符hello放入剪切板:`echo hello | clip`
2. 将`dir`命令输出放入剪切板:`dir | clip`
3. 将readme.txt的内容放入剪切板:`clip < readme.txt`
4. 将空字符串放入剪切板,即清空剪切板:`echo | clip`

### 3.4 关于大小写
windows系统不区分大小写，但其他系统严格区分大小写

### 3.5 administrators和administrator
administrators是管理员用户组，你可以将想给予管理员权限的用户放到这个组里，而且这个组是WINNT/2000/XP中权限最大的一个组，组内的用户可以进行所有涉及权限的操作，如修改用户密码、创建新用户、提升用户权限、修改系统配置及添加硬件、文件备份。
administrator是NT系列操作系统内置的管理员帐户，是Windows安装完成以后系统自动生成的一个用户，通常需要通过这个用户来提升其它管理员。可在组策略管理(gpedit.msc）中将其改名。与administrator一样由系统内置的帐户还有guest。

### 3.6 自带的远程控制
似乎只对两种情况生效：使用公网的 IP 地址或者两者在同一个内网内。

### 3.7 Hyper-V
网友：最早支持Hyper-V的Windows是Windows Server 2008。说起Hyper-V的历史，也是有一定渊源的。最早有一家公司，名叫Connectix，它有一款产品就是大家熟悉的Connectix Virtual PC，一款硬件虚拟化产品，后来Connectix把Virtual PC产品卖给了微软，成为了Microsoft Virtual PC，之后Connectix于2003年宣布解体，微软把Virtual PC精神发扬光大，成就了现在的Hyper-V。从Windows 10开始，Professional/Enterprise版本的Windows 10都能够支持Hyper-V了。大家可以直接在Windows 10中创建虚拟机，而不需要额外安装vmware player、Oracle VirtualBox等这些第三方的虚拟机服务。

在开始菜单中输入Hyper-V作为关键字，Hyper-V Manager菜单项就会显示出来，点击Hyper-V Manager的菜单项，即可打开Hyper-V的管理界面。在Hyper-V Manager中，可以非常方便地创建并管理虚拟机，虚拟机的操作系统可以是Windows的，也可以是Linux的，用户只需要下载所需操作系统的ISO镜像即可完成安装，非常方便。可参考微软官网Hyper-V的教程。

### 3.8 有空格的目录
在终端进入带空格的目录有三种方式(和mac不太一样)，比如目录`Program Files`：
1. `cd 'Program Files'`
    1. 如果想直接进去更下面的Docker目录，可以写成`cd 'Program Files\Docker'`而不能写成`cd 'Program Files'\Docker`
1. `cd Program' 'Files`
2. `cd Program" "Files`

关于带根目录的目录：
1. 用`which`命令查看tool的路径的时候，得到的是`c/xxx/xxx`，而不是`c:/xxx/xxx`。而windows带根目录的跳转只能用`c:/xxx/xxx`的方式，所以不能直接使用`which`的结果来跳转

# 二 安装配置
# 三 基础
## 1 DOS
### 查看相关
### 文件操作相关
### 安全相关
### 网络相关
### 其他
1. TYPE

## 2 windows消息模型
它是事件驱动的编程模型，应用程序通过处理操作系统发送来的消息来响应事件。事件可能是用户的一次鼠标移动，键盘敲击，或者是系统要求窗口重绘的消息，程序员所需要做的事就是处理应用程序感兴趣的消息。

Windows的消息系统是由3个部分组成的：
1. 消息队列。Windows能够为所有的应用程序维护一个消息队列。应用程序必须从消息队列中获取消息，然后分派给某个窗口。
2. 消息循环。通过这个循环机制应用程序从消息队列中检索消息，再把它分派给适当的窗口，然后继续从消息队列中检索下一条消息，再分派给适当的窗口，一次进行。
3. 窗口过程。每个窗口都有一个窗口过程来接收传递给窗口的消息，它的任务就是获取消息然后响应它。窗口过程是一个回调函数，处理了一个消息后，它通常要返回一个值给Windows。

一个消息从产生到被一个窗口响应，其中有5个步骤：
1. 系统中发生了某个事件。
2. Windows把这个事件翻译为消息，然后把它放到消息队列中。
3. 应用程序从消息队列中接收到这个消息，把它存放在TMsg记录中。
4. 应用程序把消息传递给一个适当的窗口的窗口过程。
5. 窗口过程响应这个消息并进行处理。

其中步骤3和4构成了应用程序的消息循环。消息循环往往是Windows应用程序的核心，因为消息循环使一个应用程序能够响应外部的事件。消息循环的任务就是从消息队列中检索消息，然后把消息传递给适当的窗口。如果消息队列中没有消息，Windows就允许其他应用程序处理它们的消息。

windows是一个消息驱动的系统，它使用两种方式把各种事件通知给应用程序：
1. 把消息放在应用程序的消息队列中 
2. 向适当的窗口过程直接发消息

# 四 高级
## 1 快捷键
1. 调出程序最小化、最大化、移动(m，非全屏时可用)、关闭(c)等命令面板：`alt+空格`，而且可以在程序没有边框的时候使用

## 2 iocp(待整理)

# 五 经验
## 1 包管理
最热门的软件包管理工具就属Scoop和Chocolatey，不过两者的定位稍有不同

### scoop 
https://github.com/lukesampson/scoop

windows命令行包管理工具，简单执行`scoop install xxx`，它就会把软件检车、下载、安装、更新、配置等步骤全部帮你做完。它不仅轻量，还将软件默认安装到我们的用户目录下，安装过程不需要申请管理员权限（UAC）也不会污染系统环境变量。

使用：
1. 安装scoop的两种方法(详细见github)
        1. 实测出现了
    ```bash
    # 方法一
    # 先执行下面这句允许本地脚本运行，否则会出现错误:
    # 使用“1”个参数调用“DownloadString”时发生异常:“操作超时”
    # FullyQualifiedErrorId : WebException
    Set-ExecutionPolicy RemoteSigned -scope CurrentUser
    # 然后安装
    Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')

    # 方法二
    # 实测出现了DNS污染，需要修改hosts文件或者用梯子:
    # iwr : 未能解析此远程名称: 'raw.githubusercontent.com'
    xxx.xxx.xxx.xxx raw.githubusercontent.com
    
    # 然后执行
    iwr -useb get.scoop.sh | iex

    # 查看是否安装成功
    scoop help
    ```
2. scoop安装包的位置:用户安装的程序和scoop本身位于`C:\Users<user>\scoop`。全局安装的程序位于`C:\ProgramData\scoop`。可以通过环境变量更改这些设置。
3. bucket:Scoop的设计初衷是为了方便 Windows 开发者安装和配置开发工具，其默认软件仓库的收录条件也就很苛刻，导致了它默认软件仓库（main bucket）里软件数量有限。bucket可以理解为软件库，类似于brew的tap,我们可以通过添加“软件库”来找到自己想要的软件.
    1. 查看可以直接识别并添加的bucket:`scoop bucket known`，简单介绍如下
        1. `nirsoft`:是一个 NirSoft 开发的小工具的安装合集。NirSoft 制作了大量的（dozens and dozens）小工具，包括系统工具、网络工具、密码恢复等等，孜孜不倦、持续更新。
    2. 添加bucket，`scoop bucket add bucketnameA`
        1. 比如添加extras存储库(https://github.com/lukesampson/scoop-extras.git，类似于brew的cask)可以轻松添加对流行的Windows桌面程序的支持:`scoop bucket add extras`
4. 搜索:`scoop search xxx`
5. 安装,同理卸载是`uninstall`
    1. `scoop install xxx`
    2. `scoop install -g xxx`:安装到全局目录
6. 更新
    1. 更新scoop自身到最新版`scoop update`
    2. 更新某app`scoop update xxx`
7. 查看软件详情`scoop info xxx`
    1. `Manifest`:路径指向的文件是 Scoop 具体读取的配置文件
8. 查看软件状态`scoop status xxx`

### Chocolatey

## 2 Windows Terminal
主要功能包括多选项卡、窗格、Unicode/UTF-8字符支持、GPU加速文本渲染引擎，运行速度更快，Unicode、UTF-8字符的支持则方便在多种语言环境中使用，并显示表情符号，以及自定义主题、样式和配置等。

# 六 问题
## 1 已解决
1. 权限问题，按照网上说的方法设置还是不行，最后把网络高级设置里的共享等全部打开，最后重启居然好了（待补充）
    1. 你需要管理员权限才能删除此文件
    2. 将安全信息应用到以下对象时发生错误
    3. 无法设置新的所有者 拒绝访问
    4. ...
    5. 不知道是不是上面的这些设置有了部分效果,现在当删除的时候如果提示"需要权限...",就先删除文件夹里的文件,然后再删除文件夹就行了.

## 2 未解决
2. 显示"必须在两天内激活windows才能继续使用"
    不激活会怎么样？
3. sysinternals现在还有用吗

# 七 未整理
1. wintogo的实际体验效果如何,和在mac上装双系统相比呢?
