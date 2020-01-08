# Network

## Failure Diagnosis

### Deepview: Virtual Disk Failure Diagnosis and Pattern Detection for Azure (NSDI 2018) (2020-01-08)

In modern data centers, the compute components and storage components are usually separated to different clusters, and connected by network. The storage components are called VHD. VHD failure is a major cause of VM failures, and VHD failures can be caused by storage component failures, network failures or compute component failures. Currently, when a VHD failure happens, it is hard to know its root cause and usually wastes a lot of time for developers to diagnose. In this paper, the author builds a graph of the components representing the topology of the system. Then for each path between the vm and the storage, it has a health probability which can be calculated by the monitored incidents. Then it converts the "path health probability" into the "component health probability".