# Ingress

### How to expose applications in Kubernetes

Usually, we use the Service resource to expose an application internally or externally

Service resources are broken down by type for more versatile usage. The three most commonly used types are **ClusterIP**, **NodePort** and **LoadBalancer**. Each provides a different way of exposing the service and is useful in different situations.

`ClusterIP` : exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable within the cluster. 
This is the default ServiceType.

`NodePort`: exposes the Service on each Node’s IP at a static port. A ClusterIP Service towards the NodePort Service route is created automatically. We’ll be able to access the NodePort Service from outside the cluster by requesting <NodeIP>:<NodePort>.
  
`LoadBalancer`: exposes the Service externally using a cloud provider’s load balancer. NodePort and ClusterIP Services, towards the external load balancer routes are automatically created.


ClusterIP is typically used to expose services internally, NodePort and LoadBalancer to expose them externally. The Service resource essentially provides `Layer-4` TCP/UDP load balancing, simply exposing the application ports as they are.

A LoadBalancer-type service could also be used for `Layer-7` load balancing if the provider supports it through custom annotations.
```diff
+ The Ingress resource is the most commonly used way of getting more fine-grained Layer-7 load balancing for HTTP protocol-based applications.
```

## What is Ingress?
  
### In Kubernetes, an Ingress is an object that allows access to Kubernetes services from outside the Kubernetes cluster
![image](https://user-images.githubusercontent.com/103893307/209184994-c8f18e25-5c7d-4385-95ad-d75907343f46.png)

  
### Ingress Controllers
  
An <a href="https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/">Ingress controller</a> is responsible for fulfilling the Ingress, usually with a load balancer,
- Ingress controllers will usually track and communicate with endpoints behind services instead of using services directly
- Ingress controller is the entity which grants (or remove) access, based on the changes in the services, pods and Ingress resources.
- Ingress controllers are applications that watch Ingresses in the cluster and configure a balancer to apply those rules. You can configure any of the third party balancers like HAProxy, NGINX, Vulcand or Traefik to create your version of the Ingress controller.  Ingress controller should track the changes in ingress resources, services and pods and accordingly update configuration of the balancer.  
- In order to Ingress resource work, the cluster must have an ingress controller running.
- There are many different Ingress controllers, and there’s support for cloud-native load balancers (from GCP, AWS, and Azure).
e.g. Nginx, Ambassador, EnRoute, HAProxy, AWS ALB, AKS Application Gateway

### Ingress Resources
  
The Ingress resource is a set of rules that map to Kubernetes services. Ingress resources are defined purely within Kubernetes as an object that other entities can watch and respond to.

Ingress Supports defining following rules in beta stage:


- `host header` : Forward traffic based on domain names.
- `paths` : Looks for a match at the beginning of the path.
- `TLS` : If the ingress adds TLS, HTTPS and a certificate configured through a secret will be used.
  
When no host header rules are included at an Ingress, requests without a match will use that Ingress and be mapped to the backend service. You will usually do this to send a `404 page` to requests for sites/paths which are not sent to the other services. Ingress tries to match requests to rules, and forwards them to backends, which are composed of a service and a port.  
  
