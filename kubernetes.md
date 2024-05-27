## Kubernetes

### Install

```
https://minikube.sigs.k8s.io/docs/start/
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
```

### Commands

```bash
kubectl get [resource type (pods|services|replicasets)] --watch
kubectl delete [resource type] [resource name]
kubectl describe [resource type] [resource name]
kubectl run [pod] --image=[docker image]
kubectl edit pod [pod]
kubectl logs [-f] [pod]

kubectl apply -f [file]
kubectl delete -f [file]

kubectl exec -it [pod] -- [command]
kubectl exec -it [pod] --container [container-name] -- [command]
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
      targetPort: [pod port]
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
```bash
# To get the IP
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

#### Replica set (manager replicas of the same pod)
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: [replica set name]
spec:
  template:
    metadata:
      name: [pod name (template)]
      labels:
        [key]: [value]
    spec:
      containers:
      - name: [container name]
        image: [docker image]
        ports:
        - containerPort: [external port (cluster)]
        envFrom:
        - configMapRef:
            name: [config map name]
  replicas: [number of replicas]
  selector:
    matchLabels:
      [key]: [value]
```

#### Deployment (same as a replica set, but with versioning controls)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: [deployment name]
spec:
  template:
    metadata:
      name: [pod name (template)]
      labels:
        [key]: [value]
    spec:
      containers:
      - name: [container name]
        image: [docker image]
        ports:
        - containerPort: [external port (cluster)]
        envFrom:
        - configMapRef:
            name: [config map name]
  replicas: [number of replicas]
  selector:
    matchLabels:
      [key]: [value]
```
```bash
# List versions
kubectl rollout history deployment [deployment name]

# Deploy and save history
kubectl apply -f [file] --record

# Edit change cause
kubectl annotate deployment [deployment name] kubernets.io/change-cause="[message]"

# Rollback to a specific version
kubectl rollout undo deployment [deployment name] --to-revision=[revision number]
```

#### Volume (share files among containers inside the same pod)
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: [volume-name]
spec:
  containers:
  - name: [container name 1]
    image: [docker image 1]
    volumeMounts:
    - name: [volume name]
     mountPath: [container path 1]
  - name: [container name 2]
    image: [docker image 2]
    volumeMounts:
    - name: [volume name]
     mountPath: [container path 2]
  volumes:
  - name: [volume name]
    hostPath:
      path: [volume path (inside minikube)] # Use 'minikube ssh' to access the cluster
      type: DirectoryOrCreate
```

To check the files inside the container

```bash
kubectl exec -it [pod name] --container [container name] -- bash
```

#### Persistent Volume (allocates space in disk)
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: [persistent volume name]
spec:
  capacity:
    storage: [1Gi | 2Mi]
  accessModes:
    - [ReadWriteOnce | ReadOnlyMany | ReadWriteMany]
  persistentVolumeReclaimPolicy: [Retain | Recycle | Delete]
  hostPath: # For local disk, check docs for cloud services
    path: [volume path]
    type: [DirectoryOrCreate | Directory | FileOrCreate | File]
  storageClassName: [storage class name]
```

#### Persistent Volume Claim (allocates space in a Persistent Volume)
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: [persistent volume claim name]
spec:
  accessModes:
    - [ReadWriteOnce | ReadOnlyMany | ReadWriteMany]
  resources:
    requests:
      storage: [1Gi | 2Mi]
  storageClassName: [storage class name]
```

To use a PVC
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: [pod name]
spec:
  containers:
    [pod definition]
  volumes:
    - name: [volume name]
      persistentVolumeClaim:
        claimName: [claim name]
```

### Minikube

```bash
minikube start
minikube start --driver=docker --container-runtime=containerd
minikube stop
minikube pause
minikube unpause
minikube ssh
minikube delete
minikube image ls --format table
```

#### Import image to Minikube
```bash
docker save -o [file name].tar [image]
minikube image load [file name].tar
```
