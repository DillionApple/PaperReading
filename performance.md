# Performance

## Big Data Platforms

### Dependency-Aware Network Adaptive Scheduling of Data-Intensive Parallel Jobs (TPDS 2019)

This paper utilizes the dependency graph (DAG) of big data tasks to raise the locality of the data and to reduce network cost of inter-rack traffics. One basic assumption of this paper is that inter-rack bandwidth is lower than intra-rack bandwidth.

## Cloud Computing

### Fast and Accurate Load Balancing for Geo-Distributed Storage Systems (SoCC 2018) (2019-12-23)

Some services are deployed in multi-datacenters distributed in different locations to make the service closer to customers. This paper propose a method to accurately balance the loads among different datacenters while considering the SLO violation rate. It first measures the SLO distributions of the service in different datacenters offline. And then measures the WAN RTT districution periodically. By combining these two distributions, it can estimate whether on request should be redirected to a remote datacenter while not violating the SLO. It models the problem as an optimization problem.

### Genetic Algorithm for Multi-Objective Optimization of Container Allocation in Cloud Architecture

In a container based microservice system, how to allocate the containers to the hosts in the cluster is challenging. Traditionally, like in Kubernetes, the allocator will allocate the container to a host according to the estimated resource usage in that host. It dose not consider the dependencies between the microservices (which may cause network cost), the actual resource consumption of the services (some machines maybe very busy while some are relatively free), the reliability of the system (like single point failure). This paper models the problem as a multi-objective optimization problem. It uses mathmatically parameters to represent different aspects of the system and uses genetic algorithm to do the optimization. It compares the performance under the optimized allocation with that of Kubernetes.

Currently, in Kubernetes, the microservice (say pod) allocation method is quiet primitive. Optimization directions:

* Reduce cross rack communication cost (the network cost inside one rack (either same host or different hosts) is quiet small)
* Resource usage complement (CPU/IO bound services), avoid bottleneck caused by host machine resource usage.