---
title: HA（高可用）解决方案
date: 2017-02-26 22:10:18
categories:
- HA
tags:
- HA
- 高可用
- 双机互备
---

高可用系统搭建。

## High Avialible

### 简介

[cluster] – 簇，集群。集群就是由一些互相连接在一起的计算机构成的一个并行或分布式系统，从外部来看，它们仅仅是一个系统，对外提供统一的服务。

我们用到的集群系统主要就2种:

>1.高可用(High Availability)HA集群, 使用Heartbeat实现;也会称为”双机热备”, “双机互备”, “双机”。

>2.负载均衡群集(Load Balance Cluster)，使用Linux Virtual Server(LVS)实现;

---

2种不同机制的双机系统：

>*基于系统切换的双机系统(HA)*
特点是利用双机，将系统的数据（仅指硬盘数据）进行镜像，在主机失效的情况下从机将进行系统一级的切换。 性能价格比适中，但无法实现无缝切换。

>*基于系统镜像的双机系统(FT)*
特点是利用双机，将系统的数据和运行状态（包括内存中的数据）进行镜像，从而实现热备份的目的。 能够做到无缝切换，但因为采用软件控制，占用系统资源较大，而且由于两台机器需要完全一样的配置，所以性能价格比太低。

接下来是主要关于第一种 *基于系统切换的双机系统(HA)* 的实现方案：

[HeartBeat] - Heartbeat is a daemon that provides cluster infrastructure (communication and membership) services to its clients. This allows clients to know about the presence (or disappearance!) of peer processes on other machines and to easily exchange messages with them.

[DRBD] - The Distributed Replicated Block Device (DRBD) is a software-based, shared-nothing, replicated storage solution mirroring the content of block devices (hard disks, partitions, logical volumes etc.) between servers.

[VIP] - virtual IP

### DRDB

![DRDB 双机架构图](/images/ha/drbd.png)

#### **Recovery**
1. *After a node outage*
>After an outage of a node DRBD® automatically resynchronizes the temporarily unavailable node to the latest version of the data, in the background, without interfering with the service running. Of course this also works if the role of the surviving node was changed while the peer was down.
In case a complete power outage takes both nodes down, DRBD will detect which of the nodes was down longer, and will do the resynchronization in the right direction.

2. *After an outage of the replication network*
>DRBD will reestablish the connection and do the necessary resynchronization automatically.

3. *After an outage of a storage subsystem*
>DRBD can mask the failure of a disk on the active node, i.e., the service can continue to run there, without needing to failover the service. If the disk can be replaced without shutting down the machine, it can be reattached to DRBD. DRBD resynchronizes the data as needed to the replacement disk.

4. *After an outage of all network links*
>DRBD supports you with various automatic and manual recovery options in the event of split brain.
Split brain is a situation where, due to the temporary failure of all network links between cluster nodes, and possibly due to intervention by cluster management software or human error, both nodes switched to the primary role while disconnected. This is a potentially harmful state, as it implies that modifications to the data might have been made on either node, without having been replicated to the peer. Thus, it is likely in this situation that two diverging sets of data have been created that cannot be merged.

#### **DRBD mirrors data**
1. In real time. Replication occurs continuously, while applications modify the data on the device.
2. Transparently. The applications that store their data on the mirrored device are oblivious of the fact that the data is in fact stored on several computers.
3. Synchronously or asynchronously. With synchronous mirroring, a writing application is notified of write completion only after the write has been carried out on both computer systems. Asynchronous mirroring means the writing application is notified of write completion when the write has completed locally, but before the write has propagated to the peer system.

![DRDB第三节点容灾策略](/images/ha/drbd_three_node.png)

更多:
[DRBD官网](http://www.drbd.org/en/doc/users-guide-90)

### Heartbeat

**heartbeat （Linux-HA）的工作原理：**
>heartbeat最核心的包括两个部分，心跳监测部分和资源接管部分，心跳监测可以通过网络链路和串口进行，而且支持冗余链路，它们之间相互发送报文来告诉对方自己当前的状态，如果在指定的时间内未受到对方发送的报文，那么就认为对方失效，这时需启动资源接管模块来接管运 行在对方主机上的资源或者服务。

![Heatbeat架构图](/images/ha/ha.png)

更多: [Heartbeat官网](http://www.linux-ha.org/doc/users-guide/users-guide.html)

### 搭建过程

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)
