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

#### Pods (wrapper for containers)
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
      env:
        - name: [key] # local declaration
          value: [value]
        - name: [key] # import one from config map
          valueFrom:
            configMapKeyref:
              name: [config map name]
              key: [config map key]
      envFrom: # import all from config map
        - configMapRef:
            name: [config map name]
```

#### Cluster IP (provides a stable IP for pods)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: [cluster IP name]
spec:
  type: ClusterIP
  selector:
    [key]: [value] # use labels as selector
  ports:
    - port: [external port]
      targetPort: [internal port]
```

#### Node Port (allows external communication) (works as a cluster IP)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: [node port name]
spec:
  type: NodePort
  selector:
    [key]: [value] # use labels as selector
  ports:
    - port: [external port (cluster)]
      targetPort: [internal port]
      nodePort: [external port (external)]
```

To get the IP
```bash
kubectl get nodes -o wide # INTERNAL-IP
```

#### Load balancer (allows external communication) (works as a cluster IP)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: [load balancer name]
spec:
  type: LoadBalancer
  selector:
    [key]: [value] # use labels as selector
  ports:
    - port: [external port (cluster)]
      targetPort: [internal port]
      nodePort: [external port (external)]
```

#### Config map (stores environment variables)
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: [config map name]
data:
  [key]: [value]
  [key]: [value]
```

### Minikube

```
minikube start
minikube start --driver=docker --container-runtime=containerd
minikube stop
minikube pause
minikube unpause
```
