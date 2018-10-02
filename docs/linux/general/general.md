# Linux General

## SSH Login With RSA Keys

ssh to the host (`do not close this connaction`)

```bash
mkdir -p ~/.ssh && touch .ssh/authorized_keys
```

copy your public key usually located at `~/.ssh/id_rsa.pub`

```bash
echo PUCLICK_Key_STRING >> ~/.ssh/authorized_keys
```

edit `/etc/ssh/sshd_config`
change:

```bash
#PasswordAuthentication yes
```

to

```bash
PasswordAuthentication no
```

save&exit

restart ssh service:

```bash
sudo systemctl restart ssh
```

`Open New SSH Season and Test RSA Login`

---

### Optional: change ssh port

edit `/etc/ssh/sshd_config`
change the port to a disaired one

```bash
port 1337
```

save&exit

restart ssh service:

```bash
sudo systemctl restart ssh
```

## Add Privet id_rsa key to Server

copy the id_rsa key to ~/.ssh folder

```bash
cd ~/.ssh
sudo ssh-agent bash
ssh-add id_rsa
```

**Open New SSH Season and Test RSA Login**

```bash
ssh root@HOSTNAME.local -p <port>
```

exmaple:

```bash
ssh exmaple@192.168.1.99 -p 1337
```

## Add Permanent Path to Application

First find the location of the Aplication/Service:

```bash
find / -name AplicationName
```

Go to the path wehere the application is located

```bash
cd "../../../AplicationName"
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

## Most accessed sites in the last minute

```bash
cat <<'SCRIPT' >>/root/sitesLoad.sh

#!/bin/bash
if [[ `netstat -ntalp | grep :80 | awk '$4 ~ /:80/ {print $0;exit}' | grep -q httpd; echo $?` -ne 0 ]]; then echo "Main web server is not Apache. Exiting..."; exit 1; fi

log=/tmp/hostPop
i=0
find /usr/local/apache/domlogs/ -type f -mmin -1 ! -group root -exec ls -l {} \+ | awk '{print $4, $9}' | column -t>$log

while read line; do
((++i))
       arr[$i]=$i
       arr[$i*1000]=$(printf "$line" | awk '{print $1}')
       arr[$i*1001]=$(printf "$line" | awk '{print $2}')
       arr[$i*1002]=$(wc -l `echo $line | awk '{print $NF}'` | cut -d' ' -f 1)
done < <(cat $log)

echo "Analyzing apache logs in realtime for 1 minute..."; sleep 60

for (( var=1 ; var<=$i ; var++ ))
do
       printf "${arr[$var*1000]} ${arr[$var*1001]} "
       echo $((`wc -l $(echo ${arr[$var*1001]}) | cut -d' ' -f 1` - ${arr[$var*1002]}));
done | sed -e 's/\/usr\/local\/apache\/domlogs\///g' | sort -nrk 3 | column -t

SCRIPT
chmod 700 /root/sitesLoad.sh && /root/sitesLoad.sh
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

## Virtual box boot from USB

```bash
VBoxManage internalcommands createrawvmdk -filename C:\usb.vmdk -rawdisk \\.\PhysicalDrive#
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

## Update date and time on Linux server

```bash
sudo ntpd -qg; sudo hwclock -w
```

## Clone Linux user

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

## Fix Installatron - error 500 or missing list/install

```bash
/usr/local/installatron/repair -f --release --quick
```

[Installatron FIX](https://installatron.com/docs/admin/troubleshooting#missinginstalls)

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

Gemnerate CSR:

```bash
openssl req -new -sha256 -key private.key -out mycsr.csr
```
