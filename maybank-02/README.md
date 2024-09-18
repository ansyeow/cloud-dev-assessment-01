
```
eksctl create cluster -f cluster.yaml

eksctl create nodegroup --config-file=cluster.yaml
```

```
aws eks update-kubeconfig --name maybank-cloud-assessment-02
```

```
kubectl create -f 02-01-namespace.yaml
kubectl create -f 02-02-deployment.yaml
```
