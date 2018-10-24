title: Raspberry Pi - Tor-Pi Installation Guide
description: Raspberry Pi - Tor-Pi how to make Raspberry Pi Tor Wifi Access Point Guide

# Raspberry Pi 3 Tor Access Point <small>Tor-Pi</small>

## Network Flow

![Tor-Pi Network Flow](../assets/images/RasperryPi/raspberryPi3TorAccessPoint.png "Tor-Pi Network Flow")

## Preparation

- Download Rasbian Strech Lite from: [raspberrypi.org](https://www.raspberrypi.org/downloads/raspbian/)
- Burn Image to SD-Card.
- Boot Raspberry Pi 3.

```bash
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install git
sudo raspi-config
```

Change User Password within the Config Interface
Enable SSH In Interface Options

```bash
sudo reboot
```

## Wifi Hotspot Configuration

SSH TO Raspberry Pi 3

```bash
ssh pi@raspberry_host
git clone https://github.com/unixabg/RPI-Wireless-Hotspot.git
cd RPI-Wireless-Hotspot
sudo ./install
```

"Y" to agree to terms
"Y" to use preconfigured DNS
"Y" to use Unblock-Us DNS servers
"N" for WiFi defaults
Type in a new WiFi password (it will be checked)
Type in a new SSID
Type in your desired WiFi channel (1, 6, 11)
Type "N" when asked - "Are you using a rtl871x chipset?"
Type "N" for chromecast support (unless you plan to use a chromecast w/RasTor)

```bash
sudo reboot
sudo apt-get update && sudo apt-get upgrade
```

## Testing Wifi Hotspot

Connect to new SSID with a Phone and check if you have full Internet Connection.

## Installing Tor Service

```bash
sudo apt-get install tor
sudo nano /etc/tor/torrc
```

Add the following just below the first set of comments:

```bash
Log notice file /var/log/tor/notices.log
VirtualAddrNetwork 10.192.0.0/10
AutomapHostsSuffixes .onion,.exit
AutomapHostsOnResolve 1
TransPort 9040
TransListenAddress 192.168.42.1
DNSPort 53
DNSListenAddress 192.168.42.1
```

## Configure iptables

```bash
sudo iptables -F && sudo iptables -t nat -F
sudo iptables -t nat -A PREROUTING -i wlan0 -p udp --dport 53 -j REDIRECT --to-ports 53
sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --syn -j REDIRECT --to-ports 9040
```

Check iptables routes:

```bash
sudo iptables -t nat -L
```

if all routs looks like about run this command:

```bash
sudo sh -c "iptables-save > /etc/iptables.ipv4.nat"
```

## Create log file

```bash
sudo touch /var/log/tor/notices.log
sudo chown debian-tor /var/log/tor/notices.log && sudo chmod 644 /var/log/tor/notices.log
```

## Testing and finishes

Start TOR service:

```bash
sudo service tor start
```

Check to see if the service is running:

```bash
sudo service tor status
```

Run TOR Service at Boot:

```bash
sudo update-rc.d tor enable
sudo reboot
```

Test for TOR service is running after reboot, connect to the TOR WIFI.

## Optional: Install Monit Service to reload Tor Serivce if Down

```bash
sudo apt-get install monit
sudo nano /etc/monit/monitrc
```

Add those lines to the end of the config:

```bash
check process gdm with pidfile /var/run/tor/tor.pid
   start program = "/etc/init.d/tor start"
   stop program = "/etc/init.d/tor stop"
```

Reload and add Monit to startup:

```bash
sudo monit reload
sudo update-rc.d monit enable
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="220px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->