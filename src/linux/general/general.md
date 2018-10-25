title: Linux General
description: Linux General how to, guides, examples, and simple usage

# Linux General

## Add Permanent Path to Application

First find the location of the Application/Service:

```bash
find / -name ApplicationName
```

Go to the path where the application is located

```bash
cd "../../../ApplicationName"
```

Run this command for ZSH:

```bash
echo 'export PATH="'$(pwd)':$PATH"' >> ~/.zshrc && source ~/.zshrc
```

Run this command for "Bash Profile":

```bash
echo 'export PATH="'$(pwd)':$PATH"' >> ~/.profile && source ~/.profile
```

Run this command for "Bash":

```bash
echo 'export PATH="'$(pwd)':$PATH"' >> ~/.bashrc && source ~/.bashrc
```

## Update Time Zone

```bash
sudo dpkg-reconfigure tzdata
```

## Disable IPv6

For current session:

```bash
echo 1 > /proc/sys/net/ipv6/conf/<interface-name>/disable_ipv6
echo 1 > /proc/sys/net/ipv6/conf/eth0/disable_ipv6
```

Permanent:

```bash
vi /etc/sysctl.conf
net.ipv6.conf.all.disable_ipv6 = 1
sudo sysctl -p /etc/sysctl.conf
```

## Max connections on Linux

Add to /etc/sysctl.conf:

```bash
fs.file-max = 70000
net.ipv4.tcp_tw_recycle=0
net.ipv4.tcp_fin_timeout = 10
net.ipv4.ip_local_port_range = 15000 61000
net.core.somaxconn = 1024
net.core.netdev_max_backlog = 2000
```

## Rescan drives

```bash
echo "- - -" > /sys/class/scsi_host/host0/scan
echo 1 > /sys/class/scsi_device/2\:0\:0\:0/device/rescan
```

## Find PTR owner - reversal

```bash
dig 0.168.192.in-addr.arpa. NS
```

## Fix Locales

For bash shell run:

```bash
echo "export LC_ALL=C" >> ~/.profile && source ~/.profile
```

For zsh shell run:

```bash
echo "export LC_ALL=C" >> ~/.zshrc && source ~/.zshrc
```

## Open last edited file

```bash
less `ls -dx1tr /usr/local/cpanel/logs/cpbackup/*|tail -1`
```

## Kill process that runs more than X time

Kill cgi after 30 secs:

```bash
for i in `ps -eo pid,etime,cmd|grep cgi|awk '$2 > "00:30" {print $1}'`; do kill $i; done
```

## Fix NFS mount on boot - Centos 7

Append text to the end of /usr/lib/systemd/system/nfs-idmap.service

```bash
[Install]
WantedBy=multi-user.target
```

Append text to the end of /usr/lib/systemd/system/nfs-lock.service

```bash
[Install]
WantedBy=nfs.target
```

Enable related services

```bash
systemctl enable nfs-idmapd.service
systemctl enable rpc-statd.service
systemctl enable rpcbind.socket
```

Reboot the server

## Update Date and Time on Linux Server

```bash
sudo ntpd -qg; sudo hwclock -w
```

## Clone Linux User

```bash
#!/bin/bash
SRC=$1
DEST=$2

SRC_GROUPS=$(id -Gn ${SRC} | sed "s/${SRC} //g" | sed "s/ ${SRC}//g" | sed "s/ /,/g")
SRC_SHELL=$(awk -F : -v name=${SRC} '(name == $1) { print $7 }' /etc/passwd)

useradd --groups ${SRC_GROUPS} --shell ${SRC_SHELL} --create-home ${DEST}
passwd ${DEST}
```

## Clear BOOT on Ubuntu when 100%

```bash
dpkg --purge `dpkg --list|grep "linux-"|grep -v \`uname -r|sed 's/-generic//g'\`|cut -d" " -f3|grep "[0-9]-"|paste -sd " " -`
```

## Find root of a site and CD to it

Replace domain.com with desired domain

```bash
cd `grep "domain.com" /etc/apache2/conf/httpd.conf -A7|grep Root|head -1|awk '{print $2}'`
```

## Generate CSR with OPENSSL

Generate key:

```bash
openssl genrsa -out private.key 2048
```

Generate CSR:

```bash
openssl req -new -sha256 -key private.key -out mycsr.csr
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->