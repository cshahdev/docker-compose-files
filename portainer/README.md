# Portainer

![portainer/portainer-ce:2.33.3-alpine](https://img.shields.io/badge/portainer/portainer--ce-2.33.3--alpine-blue)

| Image Tag | `portainer/portainer-ce:2.33.3-alpine` |
| --------- | -------------------------------------- |

## Prerequisite

### docker network

Given `docker-compose.yml` file expects network name **internal-net** to be already exist in your docker environment.

You can check if your network exist or not with following command

```bash
$ docker network ls
```

If your network doesn't exist, you can create one with following command

```bash
# this will create a bridge network
$ docker network create internal-net
```

### docker volume

> [!WARNING]
> This section is outdated

Given `docker-compose.yml` file expects directory called `/Users/admin/docker_volumes/portainer_data` to exist.

If you don't have that directory available, please create one directory for your docker volume and replace the path in `docker-compose.yml` file.

## Run your container

Following command will run your portainer container

```bash
$ docker compose up -d
```
