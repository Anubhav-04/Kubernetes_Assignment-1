## Tasks To Be Performed
**1.Deploy a Kubernetes cluster for 3 nodes**
```bash
minikube start --nodes 3 --driver=docker -p k3s-demo
kubectl get nodes 
NAME           STATUS   ROLES           AGE     VERSION
k3s-demo       Ready    control-plane   5m25s   v1.34.0
k3s-demo-m02   Ready    <none>          2m14s   v1.34.0
k3s-demo-m03   Ready    <none>          28s     v1.34.0
```
**2.Create a NGINX deployment of 3 replicas**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx-development
  name: nginx-development
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-development
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx-development
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

```bash
kubectl create deployment nginx-development --image=nginx --dry-run=client -o yaml > nginx-development.yml
kubectl apply -f ./nginx-development.yml

deployment.apps/nginx-development created

assar@Anubhavs-MacBook-Air Kubernetes-Assignment-1 % kubectl get deployment  
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
nginx-development   3/3     3            3           118s

assar@Anubhavs-MacBook-Air Kubernetes-Assignment-1 % kubectl get pods
NAME                                 READY   STATUS    RESTARTS   AGE
nginx-development-6b7666f999-5gqc9   1/1     Running   0          2m12s
nginx-development-6b7666f999-wcjd8   1/1     Running   0          2m13s
nginx-development-6b7666f999-xqshx   1/1     Running   0          2m13s
```