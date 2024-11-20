
Run the installer:
```
  - curl -sfL https://get.rke2.io | sh -
```
Enable the rke2-server service:
```
 - systemctl enable rke2-server.service
```
Start the service
 ```
 - systemctl start rke2-server.service
 ```
Follow the logs, if you like
```
- journalctl -u rke2-server -f

```

```
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
export PATH="/var/lib/rancher/rke2/bin:$PATH"

```
