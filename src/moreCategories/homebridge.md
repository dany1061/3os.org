# Homebridge

## Symlink for config file

```bash
ln -s /root/.homebridge /root/homebridge
```

## Run Homebridge as a service on boot (centos7)

```bash
nano /etc/default/homebridge
```

Pase the content:

```bash
# Defaults / Configuration options for homebridge
# The following settings tells homebridge where to find the config.json file and where to persist the data (i.e. pairing and others)
HOMEBRIDGE_OPTS=-U /root/homebridge

# If you uncomment the following line, homebridge will log more
# You can display this via systemd’s journalctl: journalctl -f -u homebridge
# DEBUG=*
```

Save and Exit

```bash
sudo nano /etc/systemd/system/homebridge.service
```

Pase the content:

```bash
[Unit]
Description=Node.js HomeKit Server
After=syslog.target network-online.target

[Service]
Type=simple
User=homebridge
ExecStart=/usr/local/bin/homebridge- I $HOMEBRIDGE_OPTS
Restart=on-failure
RestartSec=10
KillMode=process
User=root

[Install]
WantedBy=multi-user.target
```

I had to remove local from:  ExecStart=/usr/local/bin/homebridge $HOMEBRIDGE_OPTS  because my homebridge installed in /usr/bin/

This copies your current user’s config. This assumes you have already added accessories etc.

```bash
mkdir /var/homebridge
cp ~/.homebridge/config.json /root/homebridge
sudo cp -r ~/.homebridge/persist /root/homebridge

```

Enable Service at boot, start it, see the status of the homebridge service:

```bash
systemctl daemon-reload
systemctl enable homebridge
systemctl start homebridge
systemctl status homebridge
```

To view the logs:

```bash
journalctl -f -u homebridge
```
