title: Linux - ubuntu Linux Guides, Examples and Usage
description: ubuntu Linux - Guides, Examples and Usage

# Ubuntu Related Topics

## Disable Firewall

```bash
ufw disable
```

## Clear BOOT Partition on Ubuntu when 100%

```bash
dpkg --purge `dpkg --list|grep "linux-"|grep -v \`uname -r|sed 's/-generic//g'\`|cut -d" " -f3|grep "[0-9]-"|paste -sd " " -`
```
