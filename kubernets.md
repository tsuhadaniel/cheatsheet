## Kubernets

### Install

```
https://minikube.sigs.k8s.io/docs/start/
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
```

### Commands

```
kubectl get pods --watch
kubectl describe [pod]
kubectl run [pod] --image=[docker image]
kubectl edit pod [pod]
kubectl apply -f [file]
```

### File

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: [pod name]
spec:
  containers:
    - name: [container name]
      image: [docker image]
```

### Minikube

```
minikube start
minikube stop
minikube pause
minikube unpause
```
