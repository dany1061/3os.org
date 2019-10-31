title: Linux - Centos 7 Related Topics
description: Linux - Centos 7 how to, guides, examples, and simple usage

# Ubuntu Related Topics

## Clear BOOT Partition on Ubuntu when 100%

```bash
dpkg --purge `dpkg --list|grep "linux-"|grep -v \`uname -r|sed 's/-generic//g'\`|cut -d" " -f3|grep "[0-9]-"|paste -sd " " -`
```
