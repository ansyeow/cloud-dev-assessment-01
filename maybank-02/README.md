
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
kubectl apply -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/admission-service-account.yaml
kubectl apply -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/validating-webhook.yaml
kubectl apply -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/jobs.yaml
kubectl apply -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/ingress-service-account.yaml
kubectl apply -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/configmap.yaml
kubectl apply -f nginx-ingress-controller-main/manifests/services.yaml
kubectl apply -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/ingressclass.yaml
kubectl apply -f https://raw.githubusercontent.com/techiescamp/nginx-ingress-controller/refs/heads/main/manifests/deployment.yaml
```

# Dev

## Generate Self-Signed TLS Cert

* https://devopscube.com/create-self-signed-certificates-openssl/


## Setup Ingress TLS

```
kubectl create ns dev
kubectl apply -f 02-01a-hello-app.yaml
kubectl apply -f 02-01b-sinatra-app.yaml
kubectl apply -f 02-02-secret.yaml
kubectl apply -f 02-03-ingress.yaml
```

* https://devopscube.com/configure-ingress-tls-kubernetes/


# Refs

* https://devopscube.com/kubernetes-ingress-tutorial/
* https://aws.amazon.com/blogs/containers/exposing-kubernetes-applications-part-1-service-and-ingress-resources/
* https://aws.amazon.com/blogs/containers/exposing-kubernetes-applications-part-3-nginx-ingress-controller/

