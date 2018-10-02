## [Home-Assistant.io](https://www.home-assistant.io/) Installation on Ubuntu 18.04

```bash
sudo apt-get update
sudo apt-get install -y python3-dev python3-pip python3-venv
sudo -H pip3 install --upgrade virtualenv
python3 --version
```

Make Shure Python >= 3.5.3

Create a user and group "homeassistant". Give the user access to serial lines (zwave, insteon, etc)

```bash
sudo adduser --system homeassistant
sudo addgroup homeassistant
sudo adduser homeassistant dialout
```

Create a directory to install Home-Assistant in and set it’s ownership and permissions.

```bash
sudo mkdir /sbin/homeassistant
cd /sbin/
sudo chown homeassistant:homeassistant homeassistant
```

Change to "homeassistant" user to do the installs.

```bash
sudo su -s /bin/bash homeassistant
```

Install a virtual env to sandbox the Home-Assistant software and dependencies and activate it so further installs are done here.

```bash
cd /sbin/homeassistant
python3 -m venv .
source bin/activate
python3 -m pip install wheel
```

Install Home-Assistant from pip.

```bash
pip3 install homeassistant
```

Change config files and logs tho the instal;ation directory (rather than having them in /home/homassistant).

```bash
mkdir config
/sbin/homeassistant/bin/hass -c /sbin/homeassistant/config --log-file /sbin/homeassistant/home-assistant.log
```

Home-Assistant should install a few things and make a default config file (let it run for a little while - it takes a bit on the first start up). Hit ctrl-c to stop it. The config directory now contains a bunch of sample config files for you to edit.

You should have those files and folders in the config folder:

- automations.yaml
- configuration.yaml
- customize.yaml
- deps groups.yaml
- home-assistant_v2.db
- scripts.yaml
- secrets.yaml
- tts

You also should have home-assistant.log at homeassistant folder

Now start Home-Assistant

```bash
/sbin/homeassistant/bin/hass -c /sbin/homeassistant/config --log-file /sbin/homeassistant/home-assistant.log
```

The Home-Assistant should be accessible at:
**`http://[ServerIP]:8123`**

Assuming it works, now make a service to start hass automatically. Create the following systemd init file. The serivce name ‘hass’ can be ‘homeassistant’ or whatever you want.

```bash
touch homeassistant.service
nano homeassistant.service
```

Copy and Save

```bash
[Unit]
Description=Home Assistant
After=network.target

[Service]
Type=simple
User=homeassistant
ExecStart=/sbin/homeassistant/bin/hass -c /sbin/homeassistant/config --log-file /sbin/homeassistant/home-assistant.log

[Install]
WantedBy=multi-user.target
```

Exit the homeassistant user, copy the service file to the system, and update systemd to run the service.

```bash
exit
```

```bash
cd /sbin/homeassistant/
sudo cp homeassistant.service /etc/systemd/system/
sudo systemctl --system daemon-reload
sudo systemctl enable homeassistant
sudo systemctl start homeassistant
```

check the logs for the service to start nad running:

```bash
sudo systemctl status homeassistant
```

Finally, to make it easier to edit config files and try out code changes, I gave my regular user write permissions in the HA directory. (I’m running ACL’s on my drives which makes this simple)

```bash
sudo setfacl -R -m u:"$USER":rwx /sbin/homeassistant
```

reboot the server and test for Home-Assistant running at **`http://[ServerIP]:8123`** after boot.

## Update [Home-Assistant.io](https://www.home-assistant.io/) (Based on Installation Above)

SSH to the ubuntu server

Stop the homeassistant service:

```bash
sudo systemctl stop homeassistant
```

Change User to homeassistant:

```bash
sudo su -s /bin/bash homeassistant
cd /sbin/homeassistant
```

Run the update

```bash
source bin/activate
pip3 install --upgrade homeassistant
```

When Update is done exit homeassistant user

```bash
exit
```

start homeassistant service and check for status:

```bash
sudo systemctl start homeassistant
sudo systemctl status homeassistant
```
