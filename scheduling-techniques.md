### <center>Table of Content</center>

- [Advanced Scheduling](#advanced-scheduling)
  - [1. Node Selectors](#1-node-selectors)
  - [2. Node Affinity and Anti-Affinity](#2-node-affinity-and-anti-affinity)
  - [3. Taints and Tolerations](#3-taints-and-tolerations)

<br><br>

# Advanced Scheduling
Here is a more detailed description of Pod scheduling concepts in kubernetes such as node selectors, node affinity/anti-affinity, and taints/tolerations, including examples to clarify each concept:

## 1. Node Selectors

- Node Selectors are the simplest way to ensure that a pod is scheduled on a node that matches specific criteria.
- Using nodeSelector, you specify key-value pairs as labels that must match the node’s labels for the pod to be placed there.
- However, node selectors offer a basic level of control without more complex scheduling options.

**Example: Node Selector**

Assume a Kubernetes node has the following labels:

```
"disktype": "ssd"
"region": "us-east"
```
To ensure your pod only runs on nodes with an SSD, you’d add a nodeSelector to the pod spec:

```
apiVersion: v1
kind: Pod
metadata:
  name: ssd-pod
spec:
  nodeSelector:
    disktype: ssd
  containers:
  - name: nginx
    image: nginx
```
In this example, Kubernetes will only schedule the ssd-pod on nodes with the label disktype: ssd. If no nodes with disktype: ssd are available, the pod will remain unscheduled.

## 2. Node Affinity and Anti-Affinity

- Node Affinity and Anti-Affinity provide more advanced control over pod placement. - While node selectors only support exact matches, node affinity can include preferred or required criteria and can specify soft or hard constraints.
- Anti-affinity allows you to specify which nodes to avoid based on similar labels.

Node affinity uses the following types:

- **RequiredDuringSchedulingIgnoredDuringExecution:** The pod must run on a node that matches this affinity rule.
- **PreferredDuringSchedulingIgnoredDuringExecution:** The pod will try to be placed on a matching node, but it's not strictly required.

**Example: Node Affinity**

Suppose you have nodes labeled by region (region=us-east and region=us-west) and want to ensure a pod runs in the us-east region.

```
apiVersion: v1
kind: Pod
metadata:
  name: preferred-east-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: region
            operator: In
            values:
            - us-east
  containers:
  - name: nginx
    image: nginx
```
This pod will only schedule on nodes labeled with region: us-east.

**Example: Node Anti-Affinity**

To prevent pods from scheduling on nodes with specific labels, anti-affinity can be used. In this example, if you don’t want a pod to run on nodes labeled as disktype: hdd, you can use anti-affinity:

```
apiVersion: v1
kind: Pod
metadata:
  name: no-hdd-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: NotIn
            values:
            - hdd
  containers:
  - name: nginx
    image: nginx
```
This pod will not schedule on any node with the label disktype: hdd.

## 3. Taints and Tolerations

Taints and Tolerations are used to prevent pods from being scheduled on certain nodes unless they explicitly tolerate the taint. Taints are applied to nodes, and tolerations are applied to pods. If a node has a taint, only pods with a matching toleration can be scheduled on it.

Taints have three possible effects:

**NoSchedule:** Pods without the matching toleration will not be scheduled on this node.
**PreferNoSchedule:** The scheduler will try to avoid placing pods without a matching toleration on this node, but it’s not strictly required.
**NoExecute:** Existing pods that don’t tolerate this taint are evicted.

**Example: Adding a Taint to a Node**

To add a taint to a node so that it repels certain pods, use the kubectl taint command. For example, to taint nodes with a key-value pair dedicated=production and the effect NoSchedule:

```
kubectl taint nodes node1 dedicated=production:NoSchedule
```
This taint prevents any pod without a toleration for dedicated=production from being scheduled on node1.

**Example: Toleration for a Pod**

To schedule a pod on a node with the taint dedicated=production:NoSchedule, the pod needs a toleration:

```
apiVersion: v1
kind: Pod
metadata:
  name: toleration-pod
spec:
  tolerations:
  - key: "dedicated"
    operator: "Equal"
    value: "production"
    effect: "NoSchedule"
  containers:
  - name: nginx
    image: nginx
```
In this configuration, the pod toleration-pod can be scheduled on nodes with the taint dedicated=production:NoSchedule. Pods without this toleration will not be scheduled on those nodes.

These strategies give you control over scheduling in Kubernetes clusters, allowing you to enforce resource availability, performance requirements, and other considerations for running applications.
