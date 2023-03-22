Taints and Tolerations are used to set restrictions on what pods can be scheduled on a node.
Only pods which are tolerant to the particular taint on a node will get scheduled on that node.


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

### Use kubectl taint nodes command to taint a node.

Syntax
```bash
$ kubectl taint nodes <node-name> key=value:taint-effect
```

### Let's taint the node1 with app=blue:NoSchedule

```bash
$ kubectl taint nodes node1 app=blue:NoSchedule
```

### Adding the toleration

```yaml
apiVersion: v1
kind: Pod
metadata:
 name: myapp-pod
spec:
 containers:
 - name: nginx-container
   image: nginx
 tolerations:
 - key: "app"
   operator: "Equal"
   value: "blue"
   effect: "NoSchedule"
```

### Checking the pod scheduled on node with 'app=blue:NoSchedule' taint

```bash
$ kubectl describe pod myapp-pod
$ kubectl get pod myapp-pod -o wide
```

## Nodes with Special Hardware

What if you require special hardware for your nodes? For example, how can you prevent pods that don’t need GPU from monopolizing resources on an expensive virtual machine with specialized hardware? Taints and tolerations are the answer to this problem.


```bash
kubectl taint nodes nodename gpu=true:NoSchedule
```

The tolerations for this use case would look like this:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: gpupod
  labels:
    env: prod
spec:
  containers:
  - name: ai-handler
    image: nginx
    imagePullPolicy: IfNotPresent
  tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
```

