---
title: openstack 学习笔记
date: 2016-03-06 18:02:00
categories:
- openstack
tags:
- openstack
- 虚拟机
- 架构
---

Openstack架构研究以及第三方组件开发笔记。

## Overview

### OSI网络结构的七层模型

第七层：应用层     定义了用于在网络中进行通信和数据传输的接口 - 用户程式；提供标准服务，比如虚拟终端、文件以及任务的传输 和处理；

第六层：表示层     掩盖不同系统间的数据格式的不同性； 指定独立结构的数据传输格式； 数据的编码和解码；加密和解密；压缩和 解压缩

第五层：会话层     管理用户会话和对话； 控制用户间逻辑连接的建立和挂断；报告上一层发生的错误

第四层：传输层     管理网络中端到端的信息传送； 通过错误纠正和流控制机制提供可靠且有序的数据包传送； 提供面向无连接的数 据包的传送；

第三层：网络层     定义网络设备间如何传输数据； 根据唯一的网络设备地址路由数据包；提供流和拥塞控制以防止网络资源的损耗

第二层：数据链路层 定义操作通信连接的程序； 封装数据包为数据帧； 监测和纠正数据包传输错误

第一层：物理层      定义通过网络设备发送数据的物理方式； 作为网络媒介和设备间的接口；定义光学、电气以及机械特性。

### Message queue

消息队列（英语：Message queue）是一种进程间通信或同一进程的不同线程间的通信方式

MQ全称为Message Queue, 消息队列（MQ）是一种应用程序对应用程序的通信方法。应用程序通过读写出入队列的消息（针对应用程序的数据）来通信，而无需专用连接来链接它们。消 息传递指的是程序之间通过在消息中发送数据进行通信，而不是通过直接调用彼此来通信，直接调用通常是用于诸如远程过程调用的技术。排队指的是应用程序通过 队列来通信。队列的使用除去了接收和发送应用程序同时执行的要求。

## Message queue

### 为什么要使用消息队列

REST API的局限:
1).基于http协议，客户端与服务器之间传输消息仅限于文本。
2).采用同步机制，客户端需要等待服务器响应。
3).存在一定的耦合性，客户端发送请求必须知道服务器的地址.

 1）信息的发送者和接收者如何维持这个连接，如果一方的连接中断，这期间的数据如何方式丢失？
 2）如何降低发送者和接收者的耦合度？
 3）如何让Priority高的接收者先接到数据？
 4）如何做到load balance？有效均衡接收者的负载？
 5）如何有效的将数据发送到相关的接收者？也就是说将接收者subscribe 不同的数据，如何做有效的filter。
 6）如何做到可扩展，甚至将这个通信模块发到cluster上？
 7）如何保证接收者接收到了完整，正确的数据？
 
### AMQP

### RabbitMQ

RabbitMQ 是实现了高级消息队列协议（AMQP）的开源消息代理软件（亦称面向消息的中间件）。

ZeroMQ 高性能异步消息库。没有Server/Broker，消息发送者负责消息路由，消息接收者负责消息的入队出队，没有了集中式的管理，延迟低，带宽大，适合消息数量特别大的应用情景。

## Openstack

### 什么是openstack
