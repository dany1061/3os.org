title: Docker useful commands tips
description: Docker useful commands tips
<!-- Meta Data for search engines - NOT Visible -->

# Docker

## Update All Downloaded Images

```bash
docker images |grep -v REPOSITORY|awk '{print $1}'|xargs -L1 docker pull
```

## List all Images

```bash
docker images -a
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



<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->
