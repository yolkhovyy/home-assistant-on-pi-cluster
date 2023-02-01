# MQTT cluster

EMQX MQTT broker is used in cluster mode.

EMQX [License](https://github.com/emqx/emqx/blob/master/lib-ee/BSL.txt)

## EMQX MQTT broker installation

Create network

```bash
docker network create --attachable  --scope swarm --driver bridge emqx
```

See [docker-compose.yml](../emqx/docker-compose.yml).

```bash
cd emqx/
docker deploy -c docker-compose.yml emqx
```
