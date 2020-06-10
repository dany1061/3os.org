---
description: Proxmox Guides, Tips and modifications
---

# Proxmox

## Remove Proxmox 6.0/5.1+ Subscription Notice

To remove “You do not have a valid subscription for this server” run the command bellow. You will need to SSH to your Proxmox machine or use the node console through the PVE web interface.

SSH to the the proxmox host,
Run the following one line command

```bash
sed -i.bak "s/data.status !== 'Active'/false/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
```
