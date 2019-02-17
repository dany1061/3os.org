title: Docker useful Containers 
description: Docker useful Containers 

# Docker Containers

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

```bash
docker run \
-d \
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
