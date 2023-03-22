The Kubernetes scheduler can deploy pods automatically to Kubernetes nodes, without further instructions. However, in many cases you might want to define that pods should run only on specific nodes in a cluster, or avoid running on specific nodes. For example:

* A pod might need specialized hardware such as an SSD drive or a GPU
* Pods that communicate frequently might need to be collocated with each other
* Pods that have high computational requirements might need to be confined to specific nodes


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

### Let's schedule a pod on node with a size of Large or Medium: First variant
```yaml
apiVersion: v1
kind: Pod
metadata:
 name: myapp-pod
spec:
 containers:
 - name: data-processor
   image: data-processor
 affinity:
   nodeAffinity:
     requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: In
            values: 
            - Large
            - Medium
```

### Second variant
```yaml
apiVersion: v1
kind: Pod
metadata:
 name: myapp-pod
spec:
 containers:
 - name: data-processor
   image: data-processor
 affinity:
   nodeAffinity:
     requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: NotIn
            values: 
            - Small
``` 