
# Admin

## Setup EKS Cluster

```
eksctl create cluster -f cluster.yaml

eksctl create nodegroup --config-file=cluster.yaml
```

## Setup kubectl

```
aws eks update-kubeconfig --name maybank-cloud-assessment-02
```

## Setup ingress-nginx

https://devopscube.com/setup-ingress-kubernetes-nginx-controller

Update `nginx-ingress-controller-main/manifests/services.yaml`

```yaml
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

# Dev

## Generate Self-Signed TLS Cert

* https://devopscube.com/create-self-signed-certificates-openssl/


## Setup Ingress TLS

```
kubectl create -f 02-01-hello-app.yaml
kubectl create -f 02-02-secret.yaml
kubectl create -f 02-03-ingress.yaml
```

* https://devopscube.com/configure-ingress-tls-kubernetes/


# Refs

* https://devopscube.com/kubernetes-ingress-tutorial/
* https://aws.amazon.com/blogs/containers/exposing-kubernetes-applications-part-1-service-and-ingress-resources/
* https://aws.amazon.com/blogs/containers/exposing-kubernetes-applications-part-3-nginx-ingress-controller/

