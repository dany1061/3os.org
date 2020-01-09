title: Docker useful Containers
description: Docker useful Containers

# Docker Containers

## Watchtower - Automating Docker Updates Container

```docker
docker run \
-d \
--name watchtower \
--restart always \
-h watchtower \
-v /var/run/docker.sock:/var/run/docker.sock \
-e TZ=Asia/Jerusalem \
containrrr/watchtower:latest --cleanup --debug
```

## cloudflare-ddns

```docker
docker run \
-d \
-h cloudflare-ddns \
--restart always \
--name=cloudflare-ddns \
-v /volume1/docker/cloudflare-ddns/config.yaml:/app/config.yaml \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
joshava/cloudflare-ddns:latest
```

## cloudflared-dns-proxy

```bash
docker run \
--name=cloudflare-dns-proxy \
-h cloudflare-dns-proxy \
-d \
--restart always \
-p 11054:54/tcp \
-p 11054:54/udp \
-e DNS1=1.1.1.1 \
-e DNS2=8.8.8.8 \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
visibilityspots/cloudflared:latest
```

## Ubiquiti Unifi Controller On Synology NAS

```bash
docker run \
-d \
--restart always \
-e PUID=1000 \
-e PGID=1000 \
--name=unifi-controller \
-h unifi \
-e MEM_LIMIT=1024M  \
-v /volume1/docker/unifi:/config \
-p 8080:8080/tcp \
-p 8081:8081/tcp \
-p 8443:8443/tcp \
-p 8843:8843/tcp \
-p 8880:8880/tcp \
-p 3478:3478/udp \
-p 10001:10001/udp \
-p 6789:6789 \
-e TZ=Asia/Jerusalem \
linuxserver/unifi-controller:latest
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

## Zabbix Monitoring Container

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
-h calibre-web \
-p 11501:8083 \
-v /volume1/docker/calibre/config:/config \
-v /volume1/docker/calibre/books:/books \
-e DOCKER_MODS=linuxserver/calibre-web:calibre \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
linuxserver/calibre-web:latest
```

## Pi-Hole DNS Ad-Blocker

```docker
docker run \
-d \
--restart always \
--name pi-hole \
-h pi-hole \
-p 53:53/tcp \
-p 53:53/udp \
-p 11500:80 \
-v /volume1/docker/pihole/pihole/:/etc/pihole \
-v /volume1/docker/pihole/dnsmasq.d:/etc/dnsmasq.d \
-v /volume1/docker/pihole/lighttpd:/etc/lighttpd \
-e TZ=Asia/Jerusalem \
-e PUID=1000 \
-e PGID=1000 \
--dns=127.0.0.1 --dns=1.1.1.1 \
pihole/pihole:latest
```

Blocklists

-   https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
-   https://mirror1.malwaredomains.com/files/justdomains
-   http://sysctl.org/cameleon/hosts
-   https://zeustracker.abuse.ch/blocklist.php?download=domainblocklist
-   https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt
-   https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt
-   https://hosts-file.net/ad_servers.txt
-   https://smokingwheels.github.io/Pi-hole/allhosts
-   https://dbl.oisd.nl/
-   https://raw.githubusercontent.com/easylist/EasyListHebrew/master/EasyListHebrew.txt
-   https://raw.githubusercontent.com/anudeepND/blacklist/master/adservers.txt
-   https://filters.adtidy.org/extension/chromium/filters/14.txt
-   https://filters.adtidy.org/extension/chromium/filters/10.txt
-   https://filters.adtidy.org/extension/chromium/filters/11.txt

## Sonarr - Container to Auto Download TV Shows

```docker
docker run \
-d \
--restart always \
--name sonarr \
-h sonarr \
-e TZ=Asia/Jerusalem \
-p 5056:8989 \
-v /volume1/docker/sonarr:/config \
-v /volume1/activeShare/Media/TV\ Showes/:/tv \
-v /volume1/activeShare/Downloads/:/downloads \
linuxserver/sonarr:latest
```

## Radarr - Container to Auto Download Movies

```docker
docker run \
-d \
--restart always \
--name=radarr \
-h radarr \
-e TZ=Asia/Jerusalem \
-p 5057:7878 \
-v /volume1/docker/radarr:/config \
-v /volume1/activeShare/Media/Movies:/movies \
-v /volume1/activeShare/Downloads:/downloads \
linuxserver/radarr:latest
```

## Jackett - Container for Indexers for Radarr & Sonarr

```docker
docker run \
-d \
-h jackett \
--restart always \
--name=jackett \
-e TZ=Asia/Jerusalem \
-p 5058:9117 \
-v /volume1/docker/jackett:/config \
-v /volume1/activeShare/Downloads:/downloads \
linuxserver/jackett:latest
```

### Import Jackett Indexer In Sonarr

Add Custom Tornzab with API Path of:

```bash
/torznab/all/api
```

### Import Jackett Indexer In Radarr

Add Custom Tornzab with URL of:

```bash
<ADDRESS>:<PORT>/torznab/all/
```

## Bazarr - Container for Subtitles Auto Download

```docker
docker run \
-d \
--restart always \
--name=bazarr \
-h bazarr \
-e TZ=Asia/Jerusalem \
-p 5070:6767 \
-v /volume1/docker/bazarr:/config \
-v /volume1/activeShare/Media/Movies:/movies \
-v /volume1/activeShare/Media/TV\ Showes/:/tv \
linuxserver/bazarr:latest
```

## Ombi - Container for Requesting Movies & TV Shows Integrated with Sonarr & Radarr

```docker
docker run \
-d \
-h ombi \
--restart always \
--name=ombi \
-e TZ=Asia/Jerusalem \
-p 5059:3579 \
-v /volume1/docker/ombi:/config \
 linuxserver/ombi:latest
```

## Joal - Torrent Fake Seedings

docker run \
-d \
--name joal \
--restart always \
-h joal \
-e TZ=Asia/Jerusalem \
-e _JAVA_OPTIONS='-Djava.net.preferIPv6Addresses=true' \
-v /volume1/docker/joal:/joal/torrents/ \
--name="joal" s8n02/joal \
--joal-conf="/joal" \
--spring.main.web-environment=true \
--server.port="9000" \
--joal.ui.path.prefix="joal" \
--joal.ui.secret-token="joal123"


## HomeBridge - Container for Apple HomeKit Integration

```docker
docker run \
-d \
--net=host \
--restart always \
--name=homebridge \
-e TZ=Asia/Jerusalem \
-e HOMEBRIDGE_INSECURE=1 \
-e HOMEBRIDGE_DEBUG=1 \
-v /volume1/docker/homebridge:/homebridge \
-e HOMEBRIDGE_CONFIG_UI=1 \
-e HOMEBRIDGE_CONFIG_UI_PORT=5061 \
oznu/homebridge:latest
```
