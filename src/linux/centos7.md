title: Linux - Centos 7
description: Linux - Centos 7 how to, guides, examples, and simple usage

# Centos 7

## Service Control

In the following examples we will use ^^httpd^^ as a service

### Check Service Status

```bash
systemctl status httpd
```

### Start Service

```bash
systemctl start httpd
```

### Stop Service

```Bash
systemctl stop httpd
```

### Enabling A Service On Boot

```bash
 systemctl enable httpd
```

### Check If The Service Starts On Boot

```Bash
systemctl status httpd
```

for ^^enabled^^ service should be printed:

```bash
httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled)
```

for ^^disabled^^ service should be printed:

```bash
httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled)
```

### Check Which Services Failed To Start On Boot

```bash
systemctl --failed
```

exmaple:

```bash
$ systemctl --failed
UNIT            LOAD   ACTIVE SUB    DESCRIPTION
kdump.service   loaded failed failed Crash recovery kernel arming
php-fpm.service loaded failed failed The PHP FastCGI Process Manager

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.
```

## Installing Network Tools

```bash
yum install net-tools -y
```

## Disable and stop Firewall on Centos 7

```bash
Disable Firewalld
systemctl stop firewalld
```

## Change Default Port for SSH with SElinux Enabled

you will need semanage, find what package contains it:

```bash
yum whatprovides /usr/sbin/semanage
```

Usually it's _policycoreutils-python_

```bash
yum install policycoreutils-python
```

Add new allowed port for SSH for SElinux

```bash
semanage port -a -t ftp_port_t -p tcp <YOUR PORT>
```

## Disable SELinux on CentOS 7

change __SELINUX=enforcing__ to __SELINUX=disabled__

```bash
sudo nano /etc/selinux/config
```

reboot.

Check status

```bash
sestatus
```

## Enabling Automatic Updates In Centos 7 & rhel 7

### Install yum-cron

The package that allows us to do automatic updates via yum is yum-cron, to do this just open a terminal as root and run the command:

```bash
yum -y install yum-cron
```

This will install the yum-cron package, now it’s time to configure it, the default configuration file it’s /etc/yum/yum-cron.conf.

### Configure yum-cron for auto-update

As you can see the default it’s to upgrade all your packages, the same you’d obtain with the command yum upgrade, but there are also other options and now you can decide to just do security upgrade or even just the most critical security, this add a lot of flexibility and options.

```config
#  What kind of update to use:
# default                            = yum upgrade
# security                           = yum --security upgrade
# security-severity:Critical         = yum --sec-severity=Critical upgrade
# minimal                            = yum --bugfix upgrade-minimal
# minimal-security                   = yum --security upgrade-minimal
# minimal-security-severity:Critical =  --sec-severity=Critical upgrade-minimal
update_cmd = default

# Whether a message should be emitted when updates are available,
# were downloaded, or applied.
update_messages = yes

# Whether updates should be downloaded when they are available.
download_updates = yes

# Whether updates should be applied when they are available.  Note
# that download_updates must also be yes for the update to be applied.
apply_updates = no

# Maximum amount of time to randomly sleep, in minutes.  The program
# will sleep for a random amount of time between 0 and random_sleep
# minutes before running.  This is useful for e.g. staggering the
# times that multiple systems will access update servers.  If
# random_sleep is 0 or negative, the program will run immediately.
# 6*60 = 360
random_sleep = 360
```

### Yum-Cron Service: Start/Stop/Status/Enable on Boot

Follow [Service Control](#service_control) for more details. Use service `yum-cron.service`  
For example:

```bash
systemctl enable yum-cron.service
```

## Fix Locals Error In Bash

Error :"bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory"

add these lines to _/etc/environment_ (create it, if it doesn't exist):

```bash
LANG=en_US.UTF-8
LC_ALL=en_US.UTF-8
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->