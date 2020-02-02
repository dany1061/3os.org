title: Linux - ubuntu Linux Guides, Examples and Usage
description: ubuntu Linux - Guides, Examples and Usage

# Ubuntu Related Topics

## Disable Firewall

```bash
ufw disable
```

## Disable IPv6

add to the end of /etc/sysctl.conf

```bash
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```

Run:

```bash
sudo sysctl -p
```

Reboot. To test run

```bash
cat /proc/sys/net/ipv6/conf/all/disable_ipv6
```

If it reports ‘1′ means you have disabled IPV6.

## Clear BOOT Partition on Ubuntu when 100%

```bash
dpkg --purge `dpkg --list|grep "linux-"|grep -v \`uname -r|sed 's/-generic//g'\`|cut -d" " -f3|grep "[0-9]-"|paste -sd " " -`
```
