# Create AWS EKS clsuster

```sh
eksctl create cluster --name demo --node-type t2.large --nodes 1 --nodes-min 1 --nodes-max 2 --region us-east-1 --zones=us-east-1a,us-east-1b,us-east-1c

```

# Get EKS Cluster service


```sh
eksctl get cluster --name demo --region us-east-1
```

# Update Kubeconfig 

```sh
aws eks update-kubeconfig --name demo
```



# Create your IAM OIDC Identity Provider for your cluster

```sh
eksctl utils associate-iam-oidc-provider --cluster demo --approve
```


# Create the service account for cloudwatch logs 

 ```sh
   eksctl create iamserviceaccount --name fluentd --namespace kube-system --cluster demo --attach-policy-arn arn:aws:iam::aws:policy/CloudWatchAgentServerPolicy --approve --override-existing-serviceaccounts
```

# Create a cluster role,cluster rolebinding,configmap,daemonset,sampleapp to push the logs to clouwatch log groups

```sh
kubectl apply -f .\clusterRole_rolebinding.yaml

kubectl apply -f .\K8S_configmap.yaml

kubectl apply -f .\config_daemonset.yaml

kubectl get ds -n kube-system

kubectl apply -f .\deploy.yaml
```
