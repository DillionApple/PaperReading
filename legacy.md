# Legacy

I read these papers before 2019-12-16.

## SOCK: Rapid Task Provisioning with Serverless-Optimized Containers

Slow cold-start time for serverless containers is a big problem in cloud computing systems. Optimizing slow cold-start time can benefit both tenants and providers. In this work, it first evaluates the influence of different isolation techniques used by docker to cold-start time of the container, and find out the most costly parts. It aims to optimize the container startup time by removing or replacing the time-consuming part in container initialization. It also analyzes the time cost of importing third-party packages in python programs. And It aims to optimize this part by caching and pre-loading these packages.

## Tributary: spot-dancing for elastic services with latency SLOs (ATC 2018)

This papers studies the billing strategy of AWS stop instances, to minimize user's cost while ensuring SLOs. Not interested in this topic so far.

## PostMan: Rapidly Mitigating Bursty Traffic by Offloading Packet Processing (ATC 2019)

Data-partitioning based load balancing faces "hot data" problem. When there is bursty traffic targeting hot data, the overhead introduced by networking can be very high, especially for some services in which the packet size is usually very small. This paper uses "packet batching" to address this problem. The idea of "packet batching" is not novel, but the its application to mitigating bursty traffics of hot data blocks is novel. The experiments are also very complete. I think that's the reasons why this paper is accepted.

## R2P2: Making RPCs first-class datacenter citizens (ATC 2019)

There are two basic claims in this paper: 1) TCP is not suitable for RPC, as it may cause unnecessary overhead. 2) The current load balancing way may lead to high fan-in and fan-out problem, and cause the load-balancer to be the bottleneck. And the strategy of load balancing, random in most cases, is inefficiency. Based on these two claims, it implements a new protocol to replace TCP in the network stack. This protocol is more light weight than TCP. And routers can balance the loads at this protocol layer, using a strategy proposed by the author.

The load balancing part of this paper inspires me. The replicas of a service are usually distributed in different host machines, so the capability of each replica maybe different. Nowadays, people usually use random\round-robin\resource-usage-based strategies. But this does not consider the capability of each replica. To this end, we can collect the performance from the replicas, and balance the loads among them in a SLO-based strategy.

## IASO: A Fail-Slow Detection and Mitigation Framework for Distributed Storage Services (ATC 2019)

This paper focuses on detecting and mitigating "fail-slow" faults in distributed systems. "Fail-slow" means a worker of a service still functions but its performance downgrades apparently. It calculates the "health score" of the service workers from their response timeout, using a linear-decrement and multiplicative-increase way. It is deployed in a real-world production environment and proved to be useful, as it has many true positive cases but only a few false positive cases. It also analyzes the root cause of the "fail-slow" faults in the production environment in detail. The Related Work part makes a classification of existing works related to "fail-slow" and it is helpful for further reading.

## An Empirical Study towards Characterizing Deep Learning Development and Deployment across Different Frameworks and Platforms (ASE 2019)

一篇 Empirical Study，主要探究不同DL框架上，所训练出的模型的差异（Performance, Accuracy, Robustness等），以及在不同平台上运行DL模型的差异（Performance，Accuracy等）。文章主要回答了四个问题，并针对这四个问题，提出今后相应的研究方向。文章的出发点非常好，并且实验非常全面。是一篇非常扎实的工作。今后可以沿着作者给的方向继续深挖。

## μTune: Auto-Tuned Threading for OLDI Microservices

微服务的性能要求（sub-ms）与传统 monolithic 的性能要求(>=100ms)不同，因此一些线程设计、并发控制对于微服务来说变得至关重要。本文研究不同的 thread model 对于微服务性能的影响。本文先举证，微服务在不同的负载下，使用不同的 thread model（如synchronized 和 unsynchronized）所能达到的性能（99th percentage tail latency）是不同的，而且没有一种 thread model 能够胜任所有负载情况。然后文章对thread model 的不同纬度进行了细分（Synchronous vs. asynchronous communication, In-line vs. dispatch-based RPC processing, Block- vs. poll-based RPC reception）且通过不同纬度，组合出八种Thread Model，并分别测量它们的性能，找到在不同负载下最优的Thread Model，并实现了一个自动根据负载切换Thread Model的框架。

很solid的工作，对 thread model 的建模很细，evaluation 很全面。对我的启发：1.微服务性能要求与传统软件不同 2.性能的不同表示方法（99th percentage tail latency）

## Iron: Isolating Network-based CPU in Container Environments （NSDI 2018）

Container现在普遍在云计算中使用。Container之间的Isolation保证每个Container能获得的资源，保证其运行效率。但是当前的设计中，Host操作系统会消耗Container的时间片来处理Network请求，打破了Isolation。这篇文章首先测量了一些Container对Network的使用会对同机器上其它Container运行效率产生的影响，验证了前面的猜想。然后基于Linux设计实现了一套系统，来记录Container对网络的消耗，并将这些消耗计算到Container占用的资源中去。

实现部分细节过多，没有太仔细看。很硬核的工作。

## Performance Modeling for Cloud Microservice Applications (ICPE 2019)

确定微服务的 Performance 有助于运维人员确认在某一SLO（Service Level Object）下，该如何部署这些微服务（Host Machine配置，Replica数目等）。但是不同微服务在不同VM配置、资源限制情况下，Performance是不同的。这篇文章提出 MSC（Micro Service Capability），即在某一特定配置下以及在不违反SLO的前提下，Microservice 的 Performance（单位时间内能处理的任务数最大值）。有了MSC，就能确定在给定的负载下，该服务需要多少个Replica，以及反过来，在给定 Replica 的情况下，能处理多大的负载。

文章写的比较乱。而且才发现ICPE竟然不在CCF列表里。

## Making Sense of Performance in Data Analytics Frameworks （NSDI 2015）

现有的对大数据框架性能的分析多集中在三个方面：Network，Disk 以及 Straggler tasks。但大都只关注某一个侧面。这篇文章则试图整体看待 Network，Disk、CPU 以及 Straggler tasks 对大数据框架性能的影响。通过测量Block Time（Network阻塞时间、Disk阻塞时间），来看 Network 和 Disk 对任务的影响（如果Network无限快、Disk无限快，能带来多大的性能收益）。

对于微服务来说呢？

## A Performance Study of Big Data Workloads in Cloud Datacenters with Network Variability (ICPE 2018) (2 pass)

在真实的Data Center中，网络的状况往往是多变的（云平台上的网络带宽会有较大的variance）。这个工作测量了在不同网络带宽分布下，不同类型的大数据任务的执行速度分布（但是在单一实验中，带宽不变），并对结果进行分析。

是一篇比较短的文章。而且实验结果其实也很显然。启发是：可以从 network variability 和 performance predictability 的角度来思考对 micro service 的性能做分析。

## Sharing the Data Center Network (NSDI 2011) (1 pass)

在Data Center中，虽然VM的CPU、内存等是隔离的，但是网络资源是共享的。如果网路资源的使用不受控制，那么一些VM对网络的异常使用行为（如遭受DDos攻击，或者恶意使用网络）会影响其它VM的网络性能。这个工作首先举证对网络的异常使用会对VM网络性能的影响，然后探究构建网络资源分配机制的一些trade off。最后设计实现了一套网络资源分配系统。

## Evaluating the Monolithic and the Microservice Architecture Pattern to Deploy Web Applications in the Cloud

这篇文章通过用 Monolithic 和 Microservice 分别实现一套服务，来对比二者在部署成本、性能（响应时间）上的差异。比较简单，一共就涉及到了两个服务，而且两个服务之间还没有调用关系。文章对微服务的描述比较全面，可以作为入门阅读。

## Performance Evaluation of Microservices Architectures using Containers

对比Bare-metal、container、nested-container、virtual machine之间的网络、CPU性能差异。

## Sustaining Runtime Performance while Incrementally Modernizing Transactional Monolithic Software towards Microservices (ICPE 2016)

在一个软件从monolithic演进到micro-service的过程中，往往会出现性能问题。如果这种问题出现在线上，就会很严重。这篇文章提出的方法可以提前预警可能出现的性能问题。(什么方法呢？)

## A Framework forWriting Trigger-Action Todo Comments in Executable Format (FSE 2019)

项目中的 TODO Comment 经常会被程序员忽略而忘记处理，带来软件维护上的问题。这篇文章提出了一种可以自动判断环境条件，触发 TODO 修改的方法。将 TODO 触发的条件（如Java版本、issue是否关闭，是否实现了某个类等）和行为用Java代码写出来并嵌入到原始 Java 代码中。在编译后，判断 TODO 条件是否满足，并对编译后的文件做相应的修改，或者给程序员警告。

感觉是一个有意思，但实用性不强的工作。反而会造成很多Unexpected Behavior。

## Exploring and Exploiting the Correlations between Bug-Inducing and Bug-Fixing Commits (FSE 2019)

对 Bug-Inducing 和 Bug Fixing Commits 之间的相关性进行统计，得到一个 Empirical Study。在这个统计的基础上，发现之前相关工作的假设存在的严重缺陷。最后根据这些发现，来指导Auto Debugging、Auto Program Repair工具的设计。

## Generating Effective Test Cases for Self-Driving Cars from Police Reports (FSE 2019)

通过 NLP 去分析警察提供的自动驾驶车辆事故报告，去模拟事故发生时候的场景（环境、道路，车辆、路径，事故地点，速度等），规划事故发生时车辆的行驶状况，通过模拟还原事故发生时的场景。用来测试自动驾驶

没太读明白。（Need further reading）

## Using Microservices for Non-intrusive Customization of Multi-tenant SaaS (FSE 2019 Industrial Track)

通过微服务来实现对SaaS的定制化。讨论了业界对SaaS服务定制化的需求，以及现在SaaS提供商的一些解决办法，然后印证用微服务的话可以带来的好处。本质上就是对 SaaS 的 Main Product 进行一个封装，通过微服务去访问 Main Product 来实现定制。具体的定制能力有赖于 Main Product 所能够提供的接口。讨论了在 SaaS 平台上实现这套机制的细节的问题。

## About Microservices, Containers and their Underestimated Impact on Network Performance

通过实验验证 Container 以及和 Container 相关的 软件定义虚拟网络（以及它所提供的加密功能）对网络性能带来的 Overhead 是非常大的。我觉得这个工作可以用来佐证相关微服务应尽可能被分配到同一台机器上，以减少网络 Overhead。

有点不理解为什么实验数据里的传输率那么低（几十K/s）

## Serverless Computing: An Investigation of Factors Influencing Microservice Performance (IC2E 2018)

测量影响 Serverless 程序性能的因素，主要针对 Amazon Lambda 和 Azure。

## Predicting Breakdowns in Cloud Services (with SPIKE) (FSE 2019 Industrial Track)

感觉是一篇比较水的Industrial Track，主要用数据来预测某一个服务的响应时间是否会出现较高的毛刺。收集与这个服务相关的各种数据（网络、其它服务、内存...），然后用几种模型进行训练，最后选一个最好的进行测试。（这样也可以发FSE啊）

## A Large-Scale Empirical Study of Compiler Errors in Continuous Integration

这篇文章主要在Github上收集了众多项目的CI数据，对其中的Compile Error进行统计分析：Frequency Analysis, Distribution Analysis, Fix Effort Analysis, Fix Pattern Analysis

## A Statistics-Based Performance Testing Methodology for Cloud Applications (FSE 2019)

这篇文章做的是程序的执行时间分布。对程序执行时间采样，得到执行时间的一个分布，然后再重复这个过程，直到新得到的分布和之前所有样本的分布达到稳定。文章对两个分布是否相似的判断是用的KL距离的一个变体。

论文整体比较直观，实验很丰富，但是对Motivation的描述太少。让我比较惊讶的是论文中竟然使用“一周”作为采样时间间隔。可能在Performance Estimation中这个时间间隔不算长。

## Predicting Pull Request Completion Time: A Case Study on Large Scale Cloud Services (FSE 2019, Industrial Track)

这是一篇来自微软的文章，通过从Azure Git系统的PR里抽取特征，来预测一个PR完成的时间。

感觉工作比较简单。亮点在于在MS的系统中的实际应用，并得到了用户的积极反馈以及PR处理效率的提升，并且对这部分的强调、分析很到位。

## Your IoTs Are (Not) Mine: On the Remote Binding Between IoT Devices and Users (DSN 2019)

这篇文章主要调研了现在市面上 IoT 设备在认证过程中的安全问题。所产生的一系列安全问题主要在于服务商使用静态DeviceId来对设备进行验证，而没有用动态Token的方法。一旦DeviceId泄漏，攻击者就可以从各个方面进行攻击。

这篇文章工作很完整，有对 IoT 设备认证机制现状的分类和建模，有对可能的攻击方式的分析，有对真实设备进行的攻击实验。实验用到了一些网络流量监控以及firmware分析，有一定的技术含量。

曾经也推测过 IoT 设备的认证机制，但是没有深入思考过。思考实践过就会发现现实中会存在很多漏洞。

## Tiresias: A GPU Cluster Manager for Distributed Deep Learning (NSDI 2019)

现在 GPU Cluster 对 DDL（分布式机器学习）任务的调度机制非常简单，且没有考虑 GPU 任务的特性。这篇文章提出了一种在 GPU Cluster 中使用的高效调度的方法，算法通过利用集群内历史的 GPU 任务执行时间分布，使用Gittins Index对任务进行调度。同时考虑到GPU任务 all-or-none 的特性以及任务切换的开销，该 Schedular 将不同种类的 DNN 分配到不同的机器上运行（这部分机制待确定）。

个人认为优势在于它非常efficiency，并且在大规模集群上进行实验证实了。用的都是已有的方法，然后结合 GPU 集群的特性进行一定的修改。

视频描述较简单，需要再仔细看看论文。

## Shuffling, Fast and Slow: Scalable Analytics on Serverless Infrastructure (NSDI 2019)

Serverless能够为服务扩展带来灵活性，同时增加系统资源使用率。但是如果用它来进行大规模数据处理（主要是MapReduce模型），会存在一些Challenge，比如Serverless的实例没有自己的存储，且生存周期较短。如果使用慢速存储，会带来性能上的损失；如果使用快速存储，花销过大。这篇文章通过结合快速存储、慢速存储，并将数据处理过程分成多个Round，每个Round并行地处理一部分数据，循环利用快速存储，来实现速度和花费的平衡。

感觉这篇文章中，用Serverless解决数据处理的问题的出发点站不住脚。Serverless自身存在一定的缺点，完全可以不使用Serverless，或者创建一种新的Service。而篇文章相当于自己给自己创建了一个限制，然后再解决。文章文笔也很差，很多地方逻辑很乱。

我觉得亮点在于它的实验结果：发挥Serverless的优势，拥有更高的资源利用率，并且在各种Benchmark下的性能非常好。同时其能够非常准确地预测出，如果用这个模型来进行数据处理的话，具体哪些存储该用多少。

