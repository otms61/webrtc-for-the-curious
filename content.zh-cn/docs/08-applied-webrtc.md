---
title: WebRTC应用场景
type: docs
weight: 9
---


# WebRTC应用场景

现在您已经知道WebRTC的工作原理，到了使用它的时候了。本章探讨人们使用WebRTC构建什么以及他们是如何实现的。您将学到基于WebRTC发生的所有有趣的事情。WebRTC的功能是有代价的。建立产品级的WebRTC服务相当有挑战性。本章将尝试解释这些挑战性的根源，这样您遇到问题时就能有所准备。

## 用例

WebRTC背后的技术并不仅用于视频聊天 -- 由于WebRTC是通用的实时框架，因此应用可用的用例是无限的。一些最常见的类别包括：

### 会议

会议是WebRTC最初设计的目标用例。您可以让两个用户直接相互连接。连接后，他们可以共享网络摄像头，也可以共享桌面。参与者可以发送和接收任意数量的流。他们还可以随时添加和删除这些流。

除了传输媒体，数据通道对于提升会议体验也非常有用。用户可以发送元数据或共享文档。您可以创建多个流，并同时进行多个对话。

随着更多用户加入呼叫，会议变得更加困难。如何扩展完全取决于您。WebRTC拓扑部分将对此作进一步介绍。

### 广播

WebRTC也可以用于以一对多方式广播视频流。

### 远程控制
### 文件传输

可以创建一个桌面应用程序来捕获屏幕截图。当设备A在剪贴板上获得截图后，它可以生成一个临时链接供其他设备访问。当设备B打开链接时，就可以与设备A建立PeerConnection，然后使用WebRTC的`数据通道`对数据进行流传输。一旦传输成功，连接就可以断开。这是一种通过Internet传输文件的安全有效的方式。

### 分布式CDN
### 物联网

当视频门铃检测到移动时，它可以向摄像机提供RTP流，并通过中央服务器启动一个新的`PeerConnection`以进行记录，或者向移动设备推送通知以要求其作为peer连接。这将在门铃和移动应用之间建立实时通信。该移动应用可以将实时音频发送回门铃，也可以通过WebRTC启动安全的远程控制。

### 协议桥接


## WebRTC拓扑

无论您是使用WebRTC的语音，视频还是DataChannel功能，一切都是从`PeerConnection`开始的。在任何WebRTC应用程序中，peer如何相互连接是关键的设计考虑因素，现在已有许多验证过的方法。

### 客户端-服务器

WebRTC协议的低延迟特性非常适合通话，通常会看到以p2p网状配置（低延迟）安排会议，或者连接到SFU（选择性转发单元）以提高通话质量。由于编解码器支持因浏览器而异，因此许多会议服务器允许浏览器使用h264之类的专有或非免费编解码器进行广播，然后在服务器级别将其重新编码为VP8等开放标准。当SFU不仅执行转发数据包时执行编码任务时，它被称为MCU（多点会议单元）。尽管众所周知，SFU快速高效，非常适合举办会议，而MCU可能会占用大量资源！一些会议服务器甚至会执行更繁重的任务，例如为每个呼叫者定制的合成（组合）A/V流，以通过仅发送所有其他呼叫者的单个流来最大程度地减少客户端带宽的使用。

#### SFU (选择性转发单元)
#### MCU (多点会议单元)

### Peer-To-Peer
#### One-To-One
#### P2P Mesh