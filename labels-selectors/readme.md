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

## Deploy nginx with 'environment: production' and 'app: nginx' labels
```bash
git clone git@github.com:warolv/advanced-k8s.git
cd labels-selectors
kubectl apply -f demo1.yaml
```



