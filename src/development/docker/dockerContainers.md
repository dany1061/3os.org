title: Docker useful Containers
description: Docker useful Containers

# Docker Containers

## Watchtower - automating Docker container base image updates

```docker
docker run \
-d \
--name watchtower \
--restart always \
-h watchtower \
-v /var/run/docker.sock:/var/run/docker.sock \
-e WATCHTOWER_NOTIFICATIONS=email \
-e WATCHTOWER_NOTIFICATION_EMAIL_FROM=Watchtower@gmail.com \
-e WATCHTOWER_NOTIFICATION_EMAIL_TO=toaddress@gmail.com \
-e WATCHTOWER_NOTIFICATION_EMAIL_SERVER=smtp.gmail.com \
-e WATCHTOWER_NOTIFICATION_EMAIL_SERVER_USER=fromaddress@gmail.com \
-e WATCHTOWER_NOTIFICATION_EMAIL_SERVER_PASSWORD=app_password \
containrrr/watchtower:latest --schedule "0 4 * * 0" --cleanup --debug
```

## cloudflare-ddns

### Parameters

* ZONE: Domain, e.g. example.com.
* HOST: DNS record to be updated, e.g. example.com, subdomain.example.com.
* EMAIL: Cloudflare Email.
* API: Cloudflare API key.
* TTL: (OPTIONAL) Time to live for DNS record. Value of 1 is 'automatic'. Min value:120; Max value:2147483647. Default: 1
* PROXY: (OPTIONAL) Whether the record is receiving the performance and security benefits of Cloudflare. true to enable; false to disable. Default: true
* FORCE_CREATE: (OPTIONAL) When set, a record will be created if one does not exist already.
* RUNONCE: (OPTIONAL) When set, only a single update is attempted, and the script exists without setting up a cron process.

### Running the Container

```docker
docker run \
-d \
-h cloudflareddns \
--restart always \
--name=cloudflare-ddns \
-e ZONE=example.com \
-e HOST=example.com \
-e EMAIL=example@example.com \
-e API=1111111111111111 \
-e TTL=1 \
-e PROXY=true \
-e TZ=Asia/Jerusalem \
joshuaavalon/cloudflare-ddns:latest
```

## Ubiquiti Unifi Controller On Synology NAS

based on _jacobalberty/unifi:latest_ image for Synology NAS

```docker
docker run \
-d \
--restart always \
--name=unifi-controller \
--net=host \
-h unifi \
-v /volume1/docker/unifi:/var/lib/unifi \
-p 8080:8080/tcp \
-p 8081:8081/tcp \
-p 8443:8443/tcp \
-p 8843:8843/tcp \
-p 8880:8880/tcp \
-p 3478:3478/udp \
-e TZ=Asia/Jerusalem \
jacobalberty/unifi:latest
```

## Ubiquiti UNMS Controller On Synology NAS

Based on _oznu/unms:latest_ image for Synology NAS

```docker
docker run \
-d \
--restart always \
--name=unms-controller \
-h unms \
-v /volume1/docker/unms:/config \
-p 9080:80 \
-p 9443:443 \
-p 2055:2055/udp \
-e PUBLIC_HTTPS_PORT=9443 \
-e PUBLIC_WS_PORT=9443 \
-e TZ=Asia/Jerusalem \
oznu/unms:latest
```

## Zabbix Monitoring Contianer

```docker
docker run \
-d \
--name zabbix-appliance \
--restart always \
-h zabbix \
-p 10051:10051 \
-p 5060:80 \
-v /volume1/docker/zabbix:/var/lib/zabbix \
-v /volume1/docker/zabbix/mysql:/var/lib/mysql \
-v /volume1/docker/zabbix/nginx:/etc/ssl/nginx \
-e ZBX_SERVER_NAME=zabbix.3os.re \
-e TZ=Asia/Jerusalem \
-e PHP_TZ=Asia/Jerusalem \
zabbix/zabbix-appliance:latest
```

## iperf3 Server Container

```docker
docker run \
-d \
--restart always \
--name=iperf3-server \
-h iperf \
-p 5201:5201 \
-e TZ=Asia/Jerusalem \
networkstatic/iperf3:latest -s
```

## Calibre-Web

```docker
docker run \
-d \
--restart always \
--name=calibre-web \
-h calibre \
-e TZ=Asia/Jerusalem \
-e DOCKER_MODS=linuxserver/calibre-web:calibre \
-e PUID=0 \
-e PGID=0 \
-p 5052:8083 \
-v /volume1/docker/calibre/config:/config \
-v /volume1/activeShare/CalibreBooks:/books \
linuxserver/calibre-web:latest
```

## pi-hole DNS Ad-Blocker

```docker
docker run \
-d \
--restart always \
--name pihole \
-h pihole \
-p 53:53/tcp -p 53:53/udp \
-p 5053:80 \
-e PUID=0 \
-e PGID=0 \
-e TZ=Asia/Jerusalem \
-v /volume1/docker/pihole/pihole/:/etc/pihole \
-v /volume1/docker/pihole/dnsmasq.d:/etc/dnsmasq.d \
-v /volume1/docker/pihole/lighttpd:/etc/lighttpd \
--dns=176.103.130.130 --dns=176.103.130.131 \
pihole/pihole:latest
```
