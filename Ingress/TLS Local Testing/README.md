# secure our ingress with HTTPS

- if you look nginx controller svc , https port is already available it means when you secured ingress with https then traffic will come through secure network to the cluster
- now copy the external ip of node and https port of controller and test it
```
https://<external ip of node>:<https port no>/service1
```
error : cant verified the certificate (SSL/TLS required certificate)
```
https://<external ip of node>:<https port no>/service1 -kv
```
`-k` : use self sign certificate \
`-v` : verbose (i.e. get more data/output)

Note : see the CN : k8s ingress controller fake certificate ( if you dont configured ant tls certificate from ourself then, nginx ingress by default creaded any self sign certificate )

self sign certificate its not a valid certificate \
will create our self sign certificate (created a cert and key )
```
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
```
**use CN : riz-ingress.com**

go to ingress tls docs and create a secret 

using above certificate and key will create a secret 
```
k create secret tls secure-ingress --cert cert.pem --key key.pem
```
verified secret and ing using below CMD
```
k get secret,ing
```
now edit ingress and add tls property 

```yml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: secure-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx 
  tls:                           # Add this
  - hosts:                       # Add this
      - riz-ingress.com       # Add this
    secretName: secure-ingress   # Add this
  rules:
  - host: riz-ingress.com     # Add this
    http:
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

now run again curl command with domain name instead of ip , because we created self sign certificate for our domain , if you use ip address then you will see eariler CN which is :  k8s ingress controller fake certificate
```
curl https://riz-ingress.com:<https_port>/service1 -kv --resolve riz-ingress.com:<https_port>:<external ip of node>
```
note: for this domain we dont have an host entry in /etc/hosts that’s why we used `--resolve` flag

now in server certificate you can see CN has changed , as now we are using our own created self sign certificate i.e. ingress is using our self sign certificate 
