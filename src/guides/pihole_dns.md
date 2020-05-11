title: Pi-hole on Ubuntu/Debian with DNS Over HTTP
description: Pi-hole, DNS ads, tracking blocking on Ubuntu with DNS over HTTP, list of blacklist

<link rel="stylesheet" href="/assets/CSS/roundedCorners.css">

# Pi-hole as DNS Server with DNS over HTTPS (DOH) Based on Ubuntu/Debian Server

You can read about Pi-hole at their [Official Website](https://pi-hole.net/ "pi-hole.net")

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/guides/pihole/webgui.png" alt="webgui">
</div>

Our setup fully depends on pi-hole dns server, that's why we use two servers one as primary DNS Server and the second as secondary DNS server.

We configured our router as a DNS server for all the DHCP clients. This way all the clients requests the router to resolve the DNS.

At the router we configured the primary and the secondary DNS as our pi-hole servers.


<div style="width:80%; margin:0 auto">
   <img src="/assets/images/guides/pihole/diagram.png" alt="network flow">
</div>

* __Virtual servers based on Ubuntu Server Release.__
* __All the installation was under Root User__

## Installing Pi-hole

Just follow the official [One-Step Automated Install](https://github.com/pi-hole/pi-hole/#one-step-automated-install "pi-hole One-Step Automated Install")

We used the "Method 1: Clone our repository and run"

```bash
git clone --depth 1 https://github.com/pi-hole/pi-hole.git Pi-hole
cd "Pi-hole/automated install/"
sudo bash basic-install.sh
```

## Installing DNS-Over-HTTPS (Cloudflared Daemon)

```bash
wget https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.deb
sudo apt-get install ./cloudflared-stable-linux-amd64.deb
cloudflared -v
```

Now we configure Cloudflared Daemon to run on port then 5053 and provide it the DNS servers for resolving. We use the primary DNS server of cloudflare and secondary of google for redundancy.

```bash
mkdir /etc/cloudflared/
nano /etc/cloudflared/config.yml
```

Copy the following configuration:

```bash
proxy-dns: true
proxy-dns-port: 5053
proxy-dns-upstream:
  - https://1.1.1.1/dns-query
  - https://8.8.8.8/dns-query
```

Now install the service via cloudflared's service command:

```bash
cloudflared service install
```

Start, Enable on boot and Test

```bash
systemctl start cloudflared
systemctl enable cloudflared
systemctl status cloudflared
```

Now test that it is working! Run the following dig command, a response should be returned similar to the one below:

```log
pi@raspberrypi:~ $ dig @127.0.0.1 -p 5053 google.com

; <<>> DiG 9.11.5-P4-5.1-Raspbian <<>> @127.0.0.1 -p 5053 google.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12157
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 22179adb227cd67b (echoed)
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             191     IN      A       172.217.22.14

;; Query time: 0 msec
;; SERVER: 127.0.0.1#5053(127.0.0.1)
;; WHEN: Wed Dec 04 09:29:50 EET 2019
;; MSG SIZE  rcvd: 77
```

## Configure Pi-Hole with DNS-Over-HTTPS

Finally, configure Pi-hole to use the local cloudflared service as the upstream DNS server by specifying 127.0.0.1#5053 as the Custom DNS (IPv4):

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/guides/pihole/dnsSettings.png" alt="dnsSettings">
</div>

Advanced DNS settings

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/guides/pihole/advSettings.png" alt="nadvSettings">
</div>

We use two blocklists that update daily they don't break any normal functionality and doing a good job for blocking ads

* https://raw.githubusercontent.com/ookangzheng/dbl-oisd-nl/master/dbl.txt
* https://raw.githubusercontent.com/kboghdady/youTube_ads_4_pi-hole/master/black.list

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/guides/pihole/blockList.png" alt="nadvSettings">
</div>

Since pi-hole now is the only dns server in our system, we want to update it on daily base. Which includes the Ubuntu OS, pi-hole, and the blocklists. For this case we will use this [Auto Update Script](https://github.com/fire1ce/debianAutoUpdate), to update our system and clean all unused packages.

```bash
wget https://raw.githubusercontent.com/fire1ce/debianAutoUpdate/master/debianAutoUpdate.sh
chmod +x debianAutoUpdate.sh
ln -s ${PWD}/debianAutoUpdate.sh /usr/bin/autoupdate
```

Last step is to use crontab jobs to run all the needed updates and reboot the server.
Since we will be using two servers the jobs will be executed in different time so one of the servers should be online and working while the other performs the update maintains.

```bash
crontab -e
```

Append this to the end of the file

```bash
0 2 * * *  /usr/bin/autoupdate
15 2 * * * /usr/local/bin/pihole -up
30 2 * * *  /usr/local/bin/pihole -g
45 2 * * *  /sbin/shutdown -r now
```

This will run all the following

* autoupdate __updates and cleanup the system at 2:00__
* pihole -up __updates all pihole components at 2:15__
* pihole -g __updates the blocklists at 2:30__
* shutdown -r now __reboot the server 2:45__

On the second pihole server we use this cron:

```bash
0 3 * * *  /usr/bin/autoupdate
15 3 * * * /usr/local/bin/pihole -up
30 3 * * *  /usr/local/bin/pihole -g
45 3 * * *  /sbin/shutdown -r now
```

The finial step is to configure your router to use your new pi-hole-doh servers as primary and secondary DNS servers.
