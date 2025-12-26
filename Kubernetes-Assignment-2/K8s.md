## Tasks To Be Performed
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
        ports:
        - containerPort: 80
          protocol: TCP
status: {}
```
**2.Create a service of type NodePort for NGINX deployment**
```yaml
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-development-svc
spec:
  type: NodePort
  ports:
  - port: 8080
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx-development
status:
  loadBalancer: {}
```
```bash
kubectl apply -f service_nginx.yml
service/nginx-development-svc configured
kubectl get svc                     
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes              ClusterIP   10.96.0.1        <none>        443/TCP          33d
nginx-development-svc   NodePort    10.105.233.241   <none>        8080:30284/TCP   17m
```
**3.Check the NodePort service on a browser to verify**
```bash
curl -i  http://127.0.0.1:30284
HTTP/1.1 200 OK
Server: nginx/1.29.4
Date: Thu, 25 Dec 2025 16:50:29 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Tue, 09 Dec 2025 18:28:10 GMT
Connection: keep-alive
ETag: "69386a3a-267"
Accept-Ranges: bytes

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
