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

Pods (wrapper for containers)
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: [pod name]
  labels:
    [key]: [value]
spec:
  containers:
    - name: [container name]
      image: [docker image]
      ports:
        - containerPort: [port]
```

Cluster IP (provides a stable IP for pods)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: [service cluster IP name]
spec:
  type: ClusterIP
  selector:
    [key]: [value] # use labels as selector
  ports:
    - port: [external port]
      targetPort: [internal port]
```

### Minikube

```
minikube start
minikube start --driver=docker --container-runtime=containerd
minikube stop
minikube pause
minikube unpause
```
