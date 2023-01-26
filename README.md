# Home Assistant on Pi Cluster Step by Step

Work in progress...
## Pi Cluster

How to prpeare Raspberry Pi cluster see in [HARDWARE.md](HARDWARE.md#Raspberry-Pi).

On all nodes:

```bash

/etc/hosts

```/etc/hosts
...
192.168.1.11 rpi1
192.168.1.12 rpi2
192.168.1.13 rpi3
192.168.1.14 rpi4
...
```


## Step 1: Install docker

On all nodes:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Step 2: Create docker swarm

On rpi1:

```bash
pi@rpi1:~ $ docker swarm init --advertise-addr 192.168.1.11
Swarm initialized: current node (janohby45qktb3aqg6vpdnv9c) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3m7ipjciqepm36pcxlg2qa71fl70gnbgw3tjl892r11medyxca-33bl8f6hrf59opplyhk65hfi1 192.168.1.11:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

pi@rpi1:~ $ docker swarm join-token manager
To add a manager to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3m7ipjciqepm36pcxlg2qa71fl70gnbgw3tjl892r11medyxca-88jw3c9tg5r3593vjthnd75y1 192.168.1.11:2377
```

On all other nodes:

```bash
docker swarm join --token SWMTKN-1-3m7ipjciqepm36pcxlg2qa71fl70gnbgw3tjl892r11medyxca-88jw3c9tg5r3593vjthnd75y1 192.168.1.11:2377
```

## Step 3: Create MQTT cluster

See [docker-compose.yml](emqx/docker-compose.yml).

```bash
cd emqx/
docker deploy -c docker-compose.yml emqx
```

## Step4: Zigbee2MQTT

CC2531 coordinator hardware installation see in [HARDWARE.md](HARDWARE.md#Zigbee).

See [docker-compose.yml](zigbee2mqtt/docker-compose.yml).

```bash
cd zigbee2mqtt/
docker compose up -d
```

To be continued...