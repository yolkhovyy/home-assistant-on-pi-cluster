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
docker compose up -d
```

## NFS clients

**Install NFS client**

On all PIs:

```bash
sudo apt install nfs-client -y
sudo mkdir -p /mnt/nfs
sudo chown pi:pi /mnt/nfs
sudo mount -v -o vers=4,loud 192.168.1.1X:/ /mnt/nfs
```

**/etc/fstab**

On all PIs:

```conf
192.168.1.1X:/   /mnt/nfs   nfs4    _netdev,auto  0  0
```



