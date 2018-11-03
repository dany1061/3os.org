title: Raspberry Pi - Magic Mirror Installation Guide
description: LRaspberry Pi - Magic Mirror Installation how to, guides, examples, and simple usage

# Magic Mirror

## Change Display Rotation

```bash
sudo nano /boot/config.txt
```

Add one of those according to your setup to the config file:

| Code                   | Description     |
| ---------------------- | --------------- |
| display_rotate=0       | Normal          |
| display_rotate=1       | 90 degrees      |
| display_rotate=2       | 180 degrees     |
| display_rotate=3       | 270 degrees     |
| display_rotate=0x10000 | horizontal flip |
| display_rotate=0x20000 | vertical flip   |

`NOTE: You can rotate both the image and touch interface 180º by entering lcd_rotate=2 instead`

## Disabling the Screensaver

Change to OPEN GL Driver

```bash
sudo nano /boot/config.txt
```

add this:

```bash
dtoverlay=vc4-fkms-v3d
```

----
(Please note, you will need the x11-xserver-utils package installed.)

edit ~/.config/lxsession/LXDE-pi/autostart:

```bash
sudo nano ~/.config/lxsession/LXDE-pi/autostart
```

Add the following lines:

```bash
@xset s noblank
@xset s off
@xset -dpms
```

Edit /etc/lightdm/lightdm.conf:

```bash
sudo nano /etc/lightdm/lightdm.conf
```

Add the following line below [SeatDefaults]

```bash
xserver-command=X -s 0 -dpms
```

## OS UI Finishes

Make the Background Black:

`Right click the Desktop` -> `Desktop Preferences` and Change:
`Layout -> no image`
`Colour -> #000000`

Hit ok.

`Right click on the top panel` -> `Panel Preferences` -> `Appearance`

Select `Solid Color (With Opacity)` make sure `Opacity at 0`

## Disable WiFi Power Save

Edit /etc/modprobe.d/8192cu.conf

```bash
sudo nano /etc/modprobe.d/8192cu.conf
```

Add the following lines

```bash
# Disable power saving
options 8192cu rtw_power_mgnt=0 rtw_enusbss=1 rtw_ips_mode=1
```

For Raspberry Pi 3 (Jesse and below)
Edit /etc/network/interfaces

```bash
sudo nano /etc/network/interfaces
```

Add the following line under the wlan0 section

```bash
wireless-power off
```

Reboot your PI

```bash
sudo reboot
```

## Disable Cursor on Startup

```bash
sudo apt-get install unclutter

```

## Installation

first install node.js and npm

```bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

and then run:

```bash
sudo npm install -g npm@latest
```

If you need to remove node and npm run this:

```bash
sudo apt-get remove nodejs nodejs-legacy nodered
```

Installation:

```bash
bash -c "$(curl -sL https://raw.githubusercontent.com/MichMich/MagicMirror/master/installers/raspberry.sh)"
```

`say no to PM2 auto start - will be install manually`

To Start from SSH:

```bash
cd ~/MagicMirror && DISPLAY=:0 npm start
```

## pm2 auto start installation

```bash
sudo npm install -g pm2
cd ~
nano mm.sh
```

add this to mm.sh and save:

```bash
#!/bin/sh

cd ~/MagicMirror
DISPLAY=:0 npm start
```

```bash
chmod +x mm.sh
pm2 start mm.sh
pm2 save
pm2 startup
```

pm2 commands:

```bash
pm2 restart mm
pm2 stop mm
pm2 start mm
pm2 log
pm2 show mm
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->