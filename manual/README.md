The goal of Kubernetes is to distribute the Pods across all the nodes, without you worrying about where your Pod will be placed.

Certainly, you can use nodeSelector to determine which nodes will be used, or you can use taint (and toleration) to prevent a certain Pod to be deployed to a certain node.

But do you know you can explicitly tell Kubernetes to schedule a Pod in a certain node?

## Installation of 'kind' cluster
https://kind.sigs.k8s.io/docs/user/quick-start/#installation

### Mac
```bash
brew install kind
```

### Linux
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

### start kind k8s cluster
```bash
kind create cluster
kubectl cluster-info
```

### Deploy regular 'busy box' pod and see where it will be scheduled

```bash
git clone git@github.com:warolv/advanced-k8s.git
cd manual
kubectl apply -f demo1.yaml
```


### Deploy a 'busy box' to spcific node using 'nodeName'

Let's find node name first
```bash
kubectl get nodes -o wide
```

Deploy 'myapp-pod' to node name found previously
```bash
kubectl apply -f demo2.yaml
```

