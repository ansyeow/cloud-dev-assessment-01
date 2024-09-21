
# Setup EKS Cluster

```
eksctl create cluster -f cluster.yaml

eksctl create nodegroup --config-file=cluster.yaml
```

# Setup kubectl

```
aws eks update-kubeconfig --name maybank-cloud-assessment-02
```

# Install ingress-nginx

https://devopscube.com/setup-ingress-kubernetes-nginx-controller

Update `nginx-ingress-controller-main/manifests/services.yaml`

```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: external
    service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: instance
    service.beta.kubernetes.io/aws-load-balancer-scheme: internet-facing
```

```
kubectl create ns ingress-nginx
kubectl create -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/admission-service-account.yaml
kubectl create -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/validating-webhook.yaml
kubectl create -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/jobs.yaml
kubectl create -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/ingress-service-account.yaml
kubectl create -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/configmap.yaml
kubectl create -f nginx-ingress-controller-main/manifests/services.yaml
kubectl create -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/ingressclass.yaml
kubectl create -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/deployment.yaml
```


# Refs

* https://devopscube.com/kubernetes-ingress-tutorial/
* https://devopscube.com/configure-ingress-tls-kubernetes/
* https://aws.amazon.com/blogs/containers/exposing-kubernetes-applications-part-1-service-and-ingress-resources/
* https://aws.amazon.com/blogs/containers/exposing-kubernetes-applications-part-3-nginx-ingress-controller/
