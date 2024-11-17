Create namespace

```
kubectl create namespace cloudflare
```

Create Secret
```
kubectl create secret generic cloudflare-api-key \
  --from-literal=apiKey=<your-api-key> \
  --from-literal=email=<your-email> \
  --namespace=cloudflare
```

```
kubectl create secret generic cloudflare-api-key \
  --from-literal=apiKey=0jdRjQU7INBDc3H4peYFdtXkYgub3GIyEgpkNlpD \
  --from-literal=email=chaya.phw@gmail.com \
  --namespace=cloudflare
```

install cloudflared
```
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared-linux-amd64.deb
```

Tunnel login

```
cloudflared tunnel login

```

Create Tunnel
```
cloudflared tunnel create workshop20
```

Create tunnel-credentials
```
kubectl create secret generic tunnel-credentials \
  --from-file=credentials.json=/home/workshop/.cloudflared/5ef64657-57dd-4e7b-9bd7-02303729fb47.json \
  --namespace=cloudflare
```

Deploy Cloudflared 

```
helm repo add cloudflare https://cloudflare.github.io/helm-charts
helm repo update
helm upgrade --install cloudflare cloudflare/cloudflare-tunnel \
  --namespace cloudflare \
  --values tunnel-values.yaml \
  --wait

```
Install external-dns

```
helm repo add kubernetes-sigs https://kubernetes-sigs.github.io/external-dns/
helm repo update
```
```
helm upgrade --install external-dns kubernetes-sigs/external-dns \
  --namespace cloudflare \
  -f external-dns-values.yaml \
  --wait
```

check running
```
kubectl get deploy -n cloudflare external-dns
```