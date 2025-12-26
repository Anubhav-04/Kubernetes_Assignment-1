## Tasks To Be Performed9
**1.Use the previous deployment**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx-development
  name: nginx-development
spec:
  replicas: 5 # replicas changed to 5
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
        ports:
        - containerPort: 80
          protocol: TCP
status: {}

```
**2.Change the replicas to 5 for the deployment**
```bash
kubectl apply -f nginx-development.yml
#Either edit the file nginx-development.yml as above and apply the above command or use scale command to scale the replicas

kubectl scale deployment nginx-development --replicas=5
deployment.apps/nginx-development scaled

kubectl get deployment
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
nginx-development   5/5     5            5           63m

kubectl get pods
NAME                                 READY   STATUS    RESTARTS   AGE
nginx-development-757dc888fb-cjmmq   1/1     Running   0          13m
nginx-development-757dc888fb-ddr5g   1/1     Running   0          13m
nginx-development-757dc888fb-jr58z   1/1     Running   0          33s
nginx-development-757dc888fb-jw6h9   1/1     Running   0          33s
nginx-development-757dc888fb-zh2gv   1/1     Running   0          14m
```