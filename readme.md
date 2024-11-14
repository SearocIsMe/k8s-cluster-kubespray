
# Deploy k8s cluster on Azure by Kubespray

## Background

This repo contains the intermediate configuration files in yaml, to be used in k8s cluster provisioning in Azure Cloud.


## Resources
KubeSpray Project:
- https://github.com/kubernetes-sigs/kubespray

## Steps

### To create resource in Azure

**1. bastion host**

**2. Apply Static IP**
This ip will be used as loadbalance IP being accessed from external, and point this IP to kubernet cluster.

**3. Create Compute Resource, VM**
5 Nodes in total, 3 of master node, 2 are worker node.
worker nodes can be added on demand.
Detail refers to [azure/inventory,ini](5 Nodes in total, 3 of master node, 2 are worker node.
worker nodes can be added on demand.dDetail refers to [azure/inventory,ini](./azure/inventory.ini)

```ini

master-0 ansible_ssh_host=13.67.64.69 ip=10.0.4.6
master-1 ansible_ssh_host=13.67.66.153 ip=10.0.4.4
master-2 ansible_ssh_host=13.67.66.200 ip=10.0.4.5
minion-0 ansible_ssh_host=52.187.13.164 ip=10.240.0.4
minion-1 ansible_ssh_host=52.187.13.194 ip=10.240.0.5

[kube-master]
master-0
master-1
master-2

[etcd]
master-0
master-1
master-2

[kube-node]
minion-0
minion-1

[k8s-cluster:children]
kube-node
kube-master
```

**4. apply the settings from mycluster folder**
