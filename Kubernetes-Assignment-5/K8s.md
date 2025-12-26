## Tasks To Be Performed
**1.Use the previous deployment**
**2.Deploy an NGINX deployment of 3 replica1**
```bash
kubectl scale deployment nginx-development --replicas=3
kubectl get deployment
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
nginx-development   3/3     3            3           80m

kubectl get pods      
NAME                                 READY   STATUS    RESTARTS   AGE
nginx-development-757dc888fb-48qt8   1/1     Running   0          41s
nginx-development-757dc888fb-cjmmq   1/1     Running   0          31m
nginx-development-757dc888fb-xsmkk   1/1     Running   0          41s
```
**3.Create an NGINX service of type ClusterIP**
```bash
Kubernetes-Assignment-2 % kubectl get svc
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
kubernetes              ClusterIP   10.96.0.1        <none>        443/TCP    33d
nginx-development-svc   ClusterIP   10.105.233.241   <none>        8080/TCP   39m
```
**4.Create an ingress service/ Apache to Apache service/ NGINX to NGINX service**

```bash

kubectl apply -f ingress-nginx.yml
kubectl apply -f apache-service-ingress.yml

kubectl get ingress
NAME            CLASS   HOSTS          ADDRESS     PORTS   AGE
app-ingress     nginx   apache.local   localhost   80      4m44s
nginx-ingress   nginx   nginx.local    localhost   80      13m

echo "127.0.0.1 nginx.local" | sudo tee -a /etc/hosts
echo "127.0.0.1 apache.local" | sudo tee -a /etc/hosts

curl http://apache.local
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
<title>It works! Apache httpd</title>
</head>
<body>
<p>It works!</p>
</body>
</html>
#-----------------------------------------------------------------------------
curl http://nginx.local
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
#-------------------------------------------
```