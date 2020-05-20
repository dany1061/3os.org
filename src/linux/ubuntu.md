title: Linux - Ubuntu Linux Guides, Examples and Usage
description: Ubuntu & Debian Linux - Guides, Examples and Usage

# Ubuntu Related Topics

## Disable Firewall Ubuntu

```bash
ufw disable
```

## Auto Upgrade and Cleanup Script

Source [Github](https://github.com/fire1ce/debianAutoUpdate)

Installation

```bash
wget https://raw.githubusercontent.com/fire1ce/debianAutoUpdate/master/debianAutoUpdate.sh
chmod +x debianAutoUpdate.sh
mv debianAutoUpdate.sh /usr/bin/autoupdate
```

run

```bash
autoupdate
```

### Install as Schedule at Crontab

```bash
crontab -e
```

Empale: this will run the script every day at 04:00

```bash
0 4 * * * /usr/bin/autoupdate
```

## Disable IPv6 Persistent

Disable IPv6 using GRUB
Perform the following steps with root privileges to disable IPv6 in Ubuntu 18.04/16.04 Permanently using grub method.

Edit:

```bash
/etc/default/grub
```

Modify _GRUB_CMDLINE_LINUX_ and _GRUB_CMDLINE_LINUX_DEFAULT_ to append ipv6.disable=1:

```bash
GRUB_CMDLINE_LINUX="ipv6.disable=1"
GRUB_CMDLINE_LINUX_DEFAULT="ipv6.disable=1"
```

Update the grub configuration:

```bash
update-grub
```

Reboot the server

## Clear BOOT Partition on Ubuntu when 100%

```bash
dpkg --purge `dpkg --list|grep "linux-"|grep -v \`uname -r|sed 's/-generic//g'\`|cut -d" " -f3|grep "[0-9]-"|paste -sd " " -`
```
