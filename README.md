# docker-compose-files

## Guidelines

### How to use docker volume?

### How to use docker network?

1. Check if docker network exist. Ensure netowrk driver is `bridge`

```shell
docker network ls
```

2. if docker network doesn't exist, create docker network

```shell
# docer network create <network-name>
docker network create internal-net
```

This will create new docker network named `internal-net` with `bridge` driver which is default driver being used when creating docker network.

3. Following is example of how to use docker network within docker compose file

```yml
services:
  web:
    networks:
      - internal-net
networks:
  internal-net:
    name: internal-net
    external: true
```
