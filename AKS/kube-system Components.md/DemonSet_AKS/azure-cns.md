## Azure CNS (Container Networking Service)

It is responsible for allocating, managing, and tracking IP addresses for containers/pods when the cluster uses Azure CNI networking.

## Purpose of the Azure CNS:

1. Allocate IPs from subnet.
2. Track used/free IPs.
3. Assign IPs to pods.
4. Release IPs when pods terminate.

## Workflow:

When a pod is created:

1. Kubernetes scheduler assigns pod to a node.

2. kubelet calls the Azure CNI plugin.

3. Azure CNI asks Azure CNS for an available IP.

4. CNS:

    checks its IP pool

    assigns a free IP from the subnet

5. Pod gets an IP from the VNet subnet.

## Difference: Azure CNI vs Kubenet:

| Feature              | Azure CNI (Uses CNS) | Kubenet         |
| -------------------- | -------------------- | --------------- |
| Pod IP Source        | Azure VNet subnet    | Overlay network |
| Pod routable in VNet | Yes                  | No              |
| CNS used             | Yes                  | No              |
| Network performance  | Higher               | Lower           |
| IP consumption       | High                 | Low             |

## Checking CNS in AKS Node

If you SSH into an AKS node:

    ps aux | grep cns

or check logs:

    /var/log/azure-vnet.log
    /var/log/azure-cns.log

These logs show:

    IP allocation
    Pod networking events
    failures

## Common CNS Issues in AKS

| Issue                            | Reason             |
| -------------------------------- | ------------------ |
| Pod stuck in `ContainerCreating` | No available IPs   |
| Node network failure             | CNS crash          |
| Pod networking timeout           | subnet exhausted   |
| CNI errors                       | CNS not responding |

