# Create EKS cluster using single CMD

```
eksctl create cluster --name demo-cluster --version 1.23 --region us-east-1 --nodegroup-name demo-ng --node-type t3.medium --nodes 2 --managed
```
