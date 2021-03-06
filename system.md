# System

## File System

### EROFS: A Compression-friendly Readonly File System for Resource-scarce Devices (ATC 2019) (2020-01-03)

Existing compression file system is I/O and memory inefficiency. This work designs and implements a compression-friendly readonly file system. It uses fix-sized output compression method, and uses several optimization methods, including using cache, using per-cpu buffer, using rolling-decompression.

The basic point of this paper is that compression-friendly readonly file system is usfule for low-level smartphonse. Its main contribution is the design and implementation of the file system in android. The idea is valuable, and the implementation needs complicated technical knowledge.

## Microservice

### An Open-Source Benchmark Suite for Microservices and Their Hardware-Software Implications for Cloud & Edge Systems (ASPLOS 2019) (2020-04-19)

一句话总结：这篇文章利用一个由四个精心设计的微服务系统组成的 Benchmark，分四个层次，从底向上地对影响微服务系统性能的要素逐一进行了分析。

这篇文章分四个层面来探究影响微服务系统性能的要素：

* 硬件：CPU 指令解析、主频、Cache等
* 网络和操作系统：内核、用户、库等的执行时间特点，网络开销与运行开销，将网络开销 Offload 到 FPGA 以得到提升
* 服务管理：服务 down-grade 的传递，现有服务 scaling 的局限性			 
* 应用及框架：语言的影响，serverless与EC2性能的区别

同时文章还探究了不同微服务规模对性能的影响要素。

优点：

* 四个精心设计的复杂的微服务系统所组成的 Benchmark 系统
* Offload 网络负载到 FPGA 获得的性能提升
* 提出来的现有 scaling 机制的局限性很有借鉴意义
* 时间 - 服务分层 - 性能的热力图对于理解服务 down-grade 传递非常直观，有借鉴意义
* 文章框架清晰，每个部分都有实验支撑与详尽的理论分析

缺点：

* 框架太大，每部分的分析只关注了这个部分的一个小侧面（比如硬件上，并没有关于内存、磁盘、网卡等的分析），不够完备，像是为了这个大框架而拼凑起来的。

### Seer: Leveraging Big Data to Navigate the Complexity of Performance Debugging in Cloud Microservices (ASPLOS 2019) (2020-04-19)

一句话总结：这篇文章通过给微服务系统插桩，来获取系统运行时信息，利用这些信息，再结合深度学习模型来预测 QoS Violation，同时结合其他的一些硬件信息，来为开发人员提供相关修复建议。

优点：

* 利用真实的微服务系统做实验
* 结合了真实的 Case Study 来对实验结果进行更具体的分析。在这个过程中展示出随着时间推移

缺点：

* 既然 Violation 被提前“预警”出来并“修复”了，那如何这个 Violation 是真的呢？这样的实验、Claim 合理么？
* 在文章前面 Claim 了对硬件数据的收集有利于为开发者提供 Debug 的有利信息，但是并没有具体说明