## Azure IP Masq Agent

The Azure IP Masquerade Agent manages SNAT (Source Network Address Translation) rules for pods so that traffic leaving the cluster is translated correctly.

In Kubernetes Networking:

1. Pods have pod CIDR IP addresses.
2. External networks do not know these pod IPs.
3. Therefore iptables MASQUERADE rules translate the source IP to the node IP.

This component ensures that the traffic leaving from the pods reach-out to respective external entity or Outbound connectivity Management.

## Why It Exists in AKS

In AKS clusters, pod traffic leaving the cluster may go to:

1. Internet
2. Azure services
3. On-premises networks via VPN/ExpressRoute
4. Other VNets

The IP masquerade agent ensures:

| Scenario                 | Behavior                |
| ------------------------ | ----------------------- |
| Pod → Internet           | SNAT to Node IP         |
| Pod → Azure VNet         | No SNAT (if configured) |
| Pod → Pod (same cluster) | No SNAT                 |
| Pod → On-prem network    | Controlled via config   |

## If This Pod Is Missing

You may see issues like:

1. Pods cannot reach internet
2. SNAT problems
3. Connectivity failures to external networks

## Source IP and Node IP

1. Source IP = Pod IP (original packet source)
2. Node IP = The node's VNet IP used after SNAT when the pod traffic leaves the cluster.