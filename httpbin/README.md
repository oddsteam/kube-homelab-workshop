Create namespace

```
kubectl create namespace httpbin
```

Deploy
```
kubectl apply -n httpbin -f httpbin-deployment.yaml
```
Deploy ingress
```
kubectl apply -n httpbin -f httpbin-ingress.yaml
```