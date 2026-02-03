# Kubernetes

## K3S

### Install

On rpiX

```bash
sudo su -
curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

**/root/.bashrc**

```conf
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

### Persistent volumes

```bash
mkdir -p /mnt/data/hass/manifests
cd /mnt/data/hass/manifests
kubectl apply -f pvc-influxdb.yaml
kubectl apply -f pvc-grafana.yaml
kubectl apply -f pvc-node-red.yaml
```


## Helm

### Install

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod +x get_helm.sh 
./get_helm.sh
```

### Repos

```bash
helm repo add k8s-at-home https://k8s-at-home.com/charts/
helm repo update
```

### Helm charts

```bash
mkdir -p /mnt/data/hass/helm-charts
cd /mnt/data/hass/helm-charts
helm pull k8s-at-home/home-assistant --untar=true
helm pull k8s-at-home/grafana --untar=true
helm pull k8s-at-home/node-red --untar=true
```

### Helm install

```bash
cd /mnt/data/hass/helm-charts
helm install home-assistant ./home-assistant
helm install node-red ./node-red
```
