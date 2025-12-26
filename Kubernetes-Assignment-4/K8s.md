## Tasks To Be Performed
**1.Use the previous deployment**
```yaml
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-development-svc
spec:
  type: ClusterIP #Changed service type to ClusterIP
  ports:
  - port: 8080
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx-development
status:
  loadBalancer: {}
```
**2.Change the service type to ClusterIP**
```bash
kubectl apply -f service_nginx.yml

# Either edit the previous service_nginx.yml file in spec -> type to ClusterIP from NodePort as shown above and use the apply command or use the below patch command directly to change the service type.

kubectl patch svc nginx-development-svc -p '{"spec":{"type":"ClusterIP"}}'
service/nginx-development-svc patched
Kubernetes-Assignment-2 % kubectl get svc
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
kubernetes              ClusterIP   10.96.0.1        <none>        443/TCP    33d
nginx-development-svc   ClusterIP   10.105.233.241   <none>        8080/TCP   39m
```