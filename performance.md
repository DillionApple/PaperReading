# Performance

## Big Data Platforms

### Dependency-Aware Network Adaptive Scheduling of Data-Intensive Parallel Jobs (TPDS 2019)

This paper utilizes the dependency graph (DAG) of big data tasks to raise the locality of the data and to reduce network cost of inter-rack traffics. One basic assumption of this paper is that inter-rack bandwidth is lower than intra-rack bandwidth.

## Cloud Computing

### Fast and Accurate Load Balancing for Geo-Distributed Storage Systems (SoCC 2018) (2019-12-23)

Some services are deployed in multi-datacenters distributed in different locations to make the service closer to customers. This paper propose a method to accurately balance the loads among different datacenters while considering the SLO violation rate. It first measures the SLO distributions of the service in different datacenters offline. And then measures the WAN RTT districution periodically. By combining these two distributions, it can estimate whether on request should be redirected to a remote datacenter while not violating the SLO. It models the problem as an optimization problem.

### Genetic Algorithm for Multi-Objective Optimization of Container Allocation in Cloud Architecture

In a container based microservice system, how to allocate the containers to the hosts in the cluster is challenging. Traditionally, like in Kubernetes, the allocator will allocate the container to a host according to the estimated resource usage in that host. It dose not consider the dependencies between the microservices (which may cause network cost), the actual resource consumption of the services (some machines maybe very busy while some are relatively free), the reliability of the system (like single point failure). This paper models the problem as a multi-objective optimization problem. It uses mathmatically parameters to represent different aspects of the system and uses genetic algorithm to do the optimization. It compares the performance under the optimized allocation with that of Kubernetes.

The host machine resource modeling and microservice character modeling is quiet easy. Seems it only considers the CPU consumption. And the parameters are measured by offline testing. The measurement supposes that all microservices cooperates to do one task so the workload for each microservice is the same with respect to user request. In real world, different microservices serving different kinds of user requets may co-exist in one cluster. The workload of different microservices may change at different time. We need an effective way to scale the microservices dynamically according to its workload, say to optimize elasticity strategy. Apparently, this work does not cover this topic.

Currently, in Kubernetes, the microservice (say pod) allocation method is quiet primitive. Optimization directions:

* Reduce cross rack communication cost (the network cost inside one rack (either same host or different hosts) is quiet small)
* Resource usage complement (CPU/IO bound services), avoid bottleneck caused by host machine resource usage.

### Fuzzy Reinforcement Learning based Microservice Allocation in Cloud Computing Environments (TENCON 2019) (2019-12-26) (bad, For reference)

Microservice allocation is NP hard. This paper uses refinforcement learning to solve the problem. State: CPU utilization, Actions: allocation, Reward: power comsumption.

### Open Issues in Scheduling Microservices in the Cloud (Journal 2019 IEEE Cloud Computing) (2019-12-26)

Open issues:

* Configuration Selection and Management: which resource configuration is suitable for this microservice considering it has different resource requirement and different SLO
* Application Topology Specification and Composition: how to describe the topology among different microservices and manage the microservice life cycle according to the topology
* Performance Characterization and Isolation: characterize microservice performance with different running environment settings (container on the VM or directly on the host machine, hardware based optimization, container live migration VS restarting, reduce container interference and contention)
* Microservice Monitoring: monitoring in microservice granularity to better understanding the system in different aspects
* Elastic Scheduling and Runtime Adaptation: how to optimize elasticity strategy (how to scale up the microservices efficiently)

### CAUS: An Elasticity Controller for a Containerized Microservice (ICPE 2018) (2019-12-27)

This paper analyzes the state of the art sacling strategy of Kubernetes and Amazone EC2. They are all based on a coarse-grained metrics and the scaling behavior have defects. This paper propose a method to scale the microservices in a more fine-grained way. It uses a control loop to collect the state of the system and decide what to do next. There are four basic conceptes in this work:

1. Container capacity: how many requests can the container handle in a specific period of time
2. Load intensity: how many new requets arrives in the last minute
3. React: based on load intensity and container capacity, we can decide how many more container are needed
4. Manage spare resources: to avoid cold start in scaling out, we need to preserve a certain number of spare containers.