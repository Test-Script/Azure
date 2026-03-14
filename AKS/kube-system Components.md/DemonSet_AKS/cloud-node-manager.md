## Azure Cloud Node Manager

It is used to manages the Cloud Provider resource through Azure API Calls via Cloud Node Manager, this pod is running on each node as a demonset.

## Node Labels Added

cloud-node-manager may ensure nodes have labels like:

1. kubernetes.azure.com/cluster
2. kubernetes.azure.com/node-image-version
3. topology.kubernetes.io/region
4. topology.kubernetes.io/zone

These labels are used for:

1. scheduling
2. topology-aware routing
3. zone balancing

## Final Statement

Azure Cloud Controller Manager allows Kubernetes to dynamically provision Azure infrastructure resources such as Load Balancers, route tables, and managed disks based on Kubernetes objects like Services, Routes, and PersistentVolumeClaims.