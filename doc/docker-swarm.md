# Docker Swarm

## Docker installation

On all nodes:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Docker swarm

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

Add all other nodes as managers too:

```bash
docker swarm join --token SWMTKN-1-3m7ipjciqepm36pcxlg2qa71fl70gnbgw3tjl892r11medyxca-88jw3c9tg5r3593vjthnd75y1 192.168.1.11:2377
```
