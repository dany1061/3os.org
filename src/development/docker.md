title: Docker useful commands tips
description: Docker useful commands tips

<!-- Meta Data for search engines - NOT Visible -->

# Docker

## Update All Downloaded Images

```bash
docker images |grep -v REPOSITORY|awk '{print $1}'|xargs -L1 docker pull
```

## Purging All Unused or Dangling Images

Purging All Unused or Dangling Images, Containers, Volumes, and Networks
Docker provides a single command that will clean up any resources — images, containers, volumes, and networks — that are dangling (not associated with a container):

```bash
docker system prune
```

To additionally remove any stopped containers and all unused images (not just dangling images), add the -a flag to the command:

```bash
docker system prune -a
```

## Portainer.io Docker UI management

[Portainer.io](https://portainer.io/)

## Find Container IP

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id
```

## iperf3 Server Container

```bash
docker run \
-d \
--restart always \
--name=iperf3-server \
-h iperf \
-p 5201:5201 \
-e TZ=Asia/Jerusalem \
networkstatic/iperf3:latest -s
```
