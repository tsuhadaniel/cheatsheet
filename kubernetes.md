## Kubernetes

### Install

```
https://minikube.sigs.k8s.io/docs/start/
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
```

### Commands

```
kubectl get [resource type (pods|service)] --watch
kubectl describe [resource type] [pod]
kubectl run [pod] --image=[docker image]
kubectl edit pod [pod]

kubectl apply -f [file]
kubectl delete -f [file]

kubectl exec -it [pod] -- [command]
```

### Files

Pods
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: [pod name]
spec:
  containers:
    - name: [container name]
      image: [docker image]
      ports:
        - containerPort: [port]
```

### Minikube

```
minikube start
minikube stop
minikube pause
minikube unpause
```
