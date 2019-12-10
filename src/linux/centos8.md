title: Linux - CentOS 8 Guides, Examples and Usage
description: CentOS 8 Guides, Examples and Usage

# CentOS 8

## Set Up Automatic Updates for CentOS 8

DNF-automatic RPM package. The package provides a DNF component that starts automatically.

```bash
dnf install dnf-automatic
```

Configuring the dnf-automatic updates.

```bash
nano /etc/dnf/automatic.conf
```

Configuration this setting:

```config
apply_updates = no
```

Finally, you can now run dnf-automatic, execute the following command to schedule DNF automatic updates for your CentOS 8

```bash
systemctl enable --now dnf-automatic.timer
```
