# Install NGINX Ingress Controller 
```
kubectl apply -f https://raw.githubusercontent.com/rizwan141/KUBERNETES/main/Ingress/Nginx_Install/nginx-ingress-controller.yaml
```
```
# check ingress controller pod and svc
 k get all -n ingress-nginx 
 ```
 Note : ingress controller having two NodePorts of svc namely http and https
steps :
1. copy external ip address of worker node and use curl CMD (need to check connection from outside to the cluster through NP svc)
```
curl http://<ip addr>:<http nodeport of controller>

eg : curl http://54.172.43.254:31817
```
we can see 404 error that means its not an connection error , we can able to connect nginx ingress

# Create <a href="https://kubernetes.io/docs/concepts/services-networking/ingress/">Ingress</a> 
```
vi ingress.yaml
```

```yml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: secure-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - http:
      paths:
      - path: /service1
        pathType: Prefix
        backend:
          service:
            name: service1
            port:
              number: 80
      - path: /service2
        pathType: Prefix
        backend:
          service:
            name: service2
            port:
              number: 80        
```              

Let’s create 2 different pods and service 

```
k run pod1 --image nginx
k run pod2 --image httpd
```
```
k expose pod pod1 --port 80 --name service1
k expose pod pod2 --port 80 --name service2
```

now repeat the curl command and pass newly created service 
```
curl http://<ip addr>:<http nodeport of controller>/service1
curl http://<ip addr>:<http nodeport of controller>/service2
```
