# NFS

## NFS server

On the NFS server (rpi4 in this case, see [docker-compose.yml](../nfs/docker-compose.yml?plain=1#L22)

**Mount point**

```bash
sudo mkdir -p /mnt/nfs
sudo chown pi:pi /mnt/nfs
```
**Start the NFS server**

See [docker-compose.yml](../nfs/docker-compose.yml?plain=1#L1)

```bash
cd nfs/
docker stack deploy -c docker-compose.yml nfs
```

## NFS clients

**Install NFS client**

On all PIs except the NFS server:

```bash
sudo apt install nfs-client -y
sudo mkdir -p /mnt/nfs
sudo chown pi:pi /mnt/nfs
sudo mount -v -o vers=4,loud 192.168.1.1X:/ /mnt/nfs
docker volume create --name nfs-portainer -o type=none -o device=/mnt/nfs/portainer -o o=bind
```

**/etc/fstab**

```conf
192.168.1.1X:/   /mnt   nfs4    _netdev,auto  0  0
```



