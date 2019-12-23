# Performance

## Big Data Platforms

### Dependency-Aware Network Adaptive Scheduling of Data-Intensive Parallel Jobs (TPDS 2019)

This paper utilizes the dependency graph (DAG) of big data tasks to raise the locality of the data and to reduce network cost of inter-rack traffics. One basic assumption of this paper is that inter-rack bandwidth is lower than intra-rack bandwidth.

## Cloud Computing

### Fast and Accurate Load Balancing for Geo-Distributed Storage Systems (SoCC 2018)

Some services are deployed in multi-datacenters distributed in different locations to make the service closer to customers. This paper propose a method to accurately balance the loads among different datacenters while considering the SLO violation rate. It first measures the SLO distributions of the service in different datacenters offline. And then measures the WAN RTT districution periodically. By combining these two distributions, it can estimate whether on request should be redirected to a remote datacenter while not violating the SLO. It models the problem as an optimization problem.