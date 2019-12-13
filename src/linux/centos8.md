title: Linux - CentOS 8 Guides, Examples and Usage
description: CentOS 8 Guides, Examples and Usage

# CentOS 8

## Set Up Automatic Updates for CentOS 8

DNF-automatic RPM package. The package provides a DNF component that starts automatically.

```bash
dnf install -y dnf-automatic
```

Configuring the dnf-automatic updates.

```bash
nano /etc/dnf/automatic.conf
```

Configuration this setting:

```config
apply_updates = yes
```

Finally, you can now run dnf-automatic, execute the following command to schedule DNF automatic updates for your CentOS 8

```bash
systemctl enable --now dnf-automatic.timer
```

## Stop and Disable Firewall on CentOS 8

```bash
systemctl stop firewalld
systemctl disable firewalld
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

## Disable IPv6 on CentOS 8

Append below lines in /etc/sysctl.conf:

```bash
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```

To make the settings affective, execute :

```bash
sysctl -p
```

## Docker CE Installation on CentOS 8

```bash
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
dnf install -y docker-ce --nobest
systemctl start docker
systemctl enable docker
```

## Htop Installation CentOS 8

```bash
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
dnf update
dnf install htop
```
