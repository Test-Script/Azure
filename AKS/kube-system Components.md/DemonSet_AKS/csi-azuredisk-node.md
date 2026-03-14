## Azure Disk CSI Driver

csi-azuredisk-node is the node component of the Azure Disk CSI Driver running in an AKS Kubernetes cluster.

It is deployed as a DaemonSet in the kube-system namespace and runs one pod on every node.

Its responsibility is to attach, mount, and manage Azure Managed Disks on the node where a Pod is scheduled.

## Why It Runs as DaemonSet

Because disk mounting happens on the node OS.

Every node must be able to:

1. Attach disk
2. Mount disk
3. Expose disk to pod

So Kubernetes ensures:

1 node = 1 csi-azuredisk-node pod