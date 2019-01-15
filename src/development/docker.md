title: Docker useful commands tips
description: Docker useful commands tips
<!-- Meta Data for search engines - NOT Visible -->

# Docker

## Update All Downloaded Images

```bash
docker images |grep -v REPOSITORY|awk '{print $1}'|xargs -L1 docker pull
```

## Docker Images

### List All Images

```bash
docker images -a
```

### Remove All Unused Images

```bash
docker images purge
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




