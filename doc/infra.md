# Infra

## Traefik

Traefik volumes, on rpiX with HDD/SDD:

```bash
mkdir -p /path/to/traefic/config
docker volume create --name traefik -o type=none -o device=/path/to/traefik/config -o o=bind

mkdir -p /path/to/traefik/letsencrypt
docker volume create --name letsencrypt -o type=none -o device=/path/to//traefik/letsencrypt -o o=bind

mkdir -p /path/to/traefik/log
docker volume create --name log -o type=none -o device=/path/to//traefik/log -o o=bind
```

## Portainer

Portainer volume, on all PIs:

```bash
mkdir /mnt/nfs/portainer
docker volume create --name nfs-portainer -o type=none -o device=/mnt/nfs/portainer -o o=bind
```

## Network

```bash
docker network create -d overlay --attachable proxy
```
