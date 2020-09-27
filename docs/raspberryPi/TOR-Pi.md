---
description: Raspberry Pi - Raspberry Pi Tor Access Point Guide, Tor proxy, Raspberry Pi 2, Raspberry Pi 3, Raspberry Pi 4
---

# TorPi - Raspberry Pi Tor Access Point

## Intro

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/torPi.jpg" alt="TorPi - Raspberry Pi Tor Access Point">
</div>

<!-- prettier-ignore-start -->
!!! note "Totally Wireless TorPi :point_up_2:"
      Raspberry 2 Model B  
      2x [Edimax N150 WiFi USB Adapters](https://www.edimax.com/edimax/merchandise/merchandise_detail/data/edimax/global/wireless_adapters_n150/ew-7811un){target=_blank}  
      Miracase 5x 5000mAh Power Bank  

<!-- prettier-ignore-end -->

**Hardware Support List:**

| **Raspberry Model** | **Cable to WiFi**   | **Cable/WiFi to WiFi** |
|---------------------|---------------------|------------------------|
| Raspberry 1         | 1 WiFi USB Adapters | 2x WiFi USB Adapters   |
| Raspberry 2         | 1 WiFi USB Adapters | 2x WiFi USB Adapters   |
| Raspberry 3         | ---                 | 1 WiFi USB Adapters    |
| Raspberry 4         | ---                 | 1 WiFi USB Adapters    |

-   **Native Wifi Chipset Support**
    -   Realtek 8188 (rtl8188cus)
    -   MediaTek RT5370

## Network Flow

<div style="margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/networkDiagram.png" alt="Tor-Pi Network Flow">
</div>

## Installing Headless Minimal Raspberry Pi OS

Download **Raspberry Pi OS Minimal** image from: [raspberrypi.org](https://www.raspberrypi.org/downloads/raspberry-pi-os/ 'Raspberry Pi OS Download'){target=\_blank}
It's a headless os - **Without GUI**

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/rasberryPiOsMinimal.png" alt="TorPi">
</div>

Burn **Raspberry Pi OS Minimal** image to SD-Card that will be used in this project for TorPi.  
Since we don't won't to use external screen or keyboard, we need to allow an SSH access to the Raspberry Pi OS on the first boot.

After we created our bootable SD card we need to mount it and add a file called **“ssh”** inside a boot partition.  
This will enable and start ssh daemon on pi at boot.

<div style="width:40%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/ssh_file.png" alt="TorPi">
</div>

To continue the setup we will need a Ethernet Cable with DHCP and Internet Connection.  
Insert the SD card and the Ethernet cable and boot your pi by connecting power.  
At this point the pi should boot the new OS from the SD card and get a DHCP address.  
Find the new address your pi just got from your dhcp server. You can do it inside your router's ui or use nmap tp find it on the network.  
If you can't find the new address you can allows connect it to external screen and keyboard - use default credentials to login and 'ip addr' command

SSH to the Raspberry Pi
Default credentials:

-   User: **pi**
-   Password: **raspberry**

```bash
ssh pi@192.168.1.111
```

Change the default password for the Pi user

```bash
passwd
```

Let's run system updates and cleanup

```bash
sudo apt update && sudo apt full-upgrade -y
```

**Optional**: Use simple: [Update Script](https://3os.org/linux/ubuntu/#debianubunturaspberrypios-_update_script 'update script){target=\_blank}

**Optional**: [SSH Hardening with RSA Keys](https://3os.org/linux/SSH_Service_Security/#ssh_service_security 'SSH Hardening with RSA Keys'){target=\_blank}

**Optional**: [Fix bash local error](https://3os.org/linux/general/general/#fix_locales_fix_bash_local_error 'Fix bash local error'){target=\_blank}

**Optional**: [Set System Time With NTP](https://3os.org/linux/general/general/#set_system_time_with_time_zone_timedatectl_ntp 'Set System Time With NTP'){target=\_blank}

**Optional** [Install Oh My Zsh](https://3os.org/guides/BetterTerminal/#linux_installation 'Install Oh My Zsh'){target=\_blank}

Follow this to [Disable IPv6 on Raspberry Pi Os](https://3os.org/raspberryPi/piGeneral/#disable_ipv6_on_raspberry_pi_os 'Disable IPv6 on Raspberry Pi Os'){target=\_blank}

Change the Hostname to 'torPi' or any one you like

```bash
sudo raspi-config
```

Select: 2.Network Options -> N1 Hostname

```config
torPi
```

Install some usefully utils if missing

```bash
sudo apt install -y net-tools curl wget traceroute htop
```

Reboot The Pi for the first time

```bash
sudo reboot
```

## RaspAP WiFi Configuration Web Portal Installation

Many thanks to [billz](https://github.com/billz 'github.com/billz'){target=\_blank} for his project [RaspAP](https://raspap.com/ 'https://raspap.com)'){target=\_blank}

We will use [raspap-webgui](https://github.com/billz/ 'https://github.com/billz/'){target=\_blank} package to Manage our WiFi connections with simple Web-ui

Let's use the **Quick Interactive RaspAP Install** script

```bash
curl -sL https://install.raspap.com | bash
```

| **Question**                                                 | **Answer** |
|--------------------------------------------------------------|------------|
| lighttpd root: /var/www/html?                                | Y          |
| Complete installation with these values?                     | Y          |
| Enable HttpOnly for session cookies (Recommended)?           | Y          |
| Enable RaspAP control service (Recommended)?                 | Y          |
| Install ad blocking and enable list management?              | n          |
| Install OpenVPN and enable client configuration?             | n          |
| The system needs to be rebooted as a final step. Reboot now? | y          |

After the reboot at the end of the installation the wireless network will be configured as an access point as follows:

<!-- prettier-ignore-start -->
!!! note "Default SSID Information "
      SSID: raspi-webgui  
      IP address: 10.3.141.1  
      DHCP range: 10.3.141.50 to 10.3.141.255  
      Password: ChangeMe  

!!! note "Default WEB-UI Information "
      Web-Ui: [http://10.3.141.1/](http://10.3.141.1/){target=_blank}  
      Username: admin  
      Password: secret  
<!-- prettier-ignore-end -->

For this guide we will use the default gateway address of **10.3.141.1** and the gateway **DHCP range**
Login to the Web-Ui: [http://10.3.141.1/](http://10.3.141.1/){target=\_blank}.

<!-- prettier-ignore-start -->
!!! warning
      Change the Default web-ui Credentials
<!-- prettier-ignore-end -->

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/webui-authentication.png" alt="webui-authentication">
</div>

<!-- prettier-ignore-start -->
!!! Example "Configuration with One Wireless Interface"
      If you raspberry pi as only **one wireless** interface the default RaspAP configuration of the host sport is great.  
      The only think you should to in the interface is to change the SSD, PSK
<!-- prettier-ignore-end -->

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/wlan0_hotspot.png" alt="wlan0 hotspot">
</div>

<!-- prettier-ignore-start -->
!!! Example "Configuration with Two Wireless Interface"
      If you raspberry pi as only **two wireless** interface we need to set  
      **wlan1 as Hotspot**  
      **wlan0 as WiFi Client**  
<!-- prettier-ignore-end -->

Set the Hotspot with interface **wlan1**

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/wlan1_hotspost.png" alt="wlan1 hotspot">
</div>

Connect to known WiFi make sure the interface is set to wlan0

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/wlan0_wifiClient.png" alt="wlan0 hotspot">
</div>

## Tor Service

Install tor service

```bash
sudo apt install -y tor
```

delete the default torrc config

```bash
sudo rm -rf /etc/tor/torrc
```

Create new torrc and edit it

```bash
/etc/tor/torrc
```

Add the lines below to torrc

```bash
VirtualAddrNetwork 10.192.0.0/10
AutomapHostsSuffixes .onion,.exit
AutomapHostsOnResolve 1
TransPort 10.3.141.1:9040
TransListenAddress 10.3.141.1
DNSPort 10.3.141.1:53
DNSListenAddress 10.3.141.1
```

**Optional** add this to rotate the exit node every 10 seconds

```bash
CircuitBuildTimeout 10
LearnCircuitBuildTimeout 0
MaxCircuitDirtiness 10
```

<div style="width:60%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/torrc.png" alt="torrc">
</div>

Start and enable Tor Service a boot

```bash
sudo systemctl start tor.service
sudo systemctl enable tor.service
```

make sure the tor service started currently as in screen bellow:

```bash
sudo netstat -plnt
```

<div style="width:80%; margin:0 auto">
   <img src="/assets/images/RaspberryPi/torPi/netstat_tor.png" alt="netstat tor">
</div>
<!-- prettier-ignore-start -->
!!! bug
      There is a bug that Tor Service won't load at boot because of all the interfaces changes.  
      The solution is to install **Monit**. Monit Will load the tor Tor Service as soon as it can.  
      It will also reload it if it will crash
<!-- prettier-ignore-end -->

Install Monit

```bash
sudo apt install monit
```

Edit Monit Config

```bash
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
sudo systemctl restart monit
sudo systemctl enable monit
```

<!-- prettier-ignore-start -->
!!! warning
      Be Patient!!!  
      With my Pi2 full startup may take up to 3 minutes
<!-- prettier-ignore-end -->

## Configure iptables firewall rules

Its time to firewall the traffic to specific port

-   Allow port 22,80 from any interface to allow access to ssh and the web-ui
-   Route all DNS traffic from wlan1 to internal port 53
-   Route all other wlan1 tcp traffic via tor proxy on port 9040

Flash all iptables rules:

```bash
sudo iptables -F && sudo iptables -t nat -F
```

Route Rules

<!-- prettier-ignore-start -->
!!! Example "Route Rules for One Wireless Interface with Hotspot on wlan0"
<!-- prettier-ignore-end -->

```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-ports 22
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 80
sudo iptables -t nat -A PREROUTING -i wlan0 -p udp --dport 53 -j REDIRECT --to-ports 53
sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --syn -j REDIRECT --to-ports 9040
```

<!-- prettier-ignore-start -->
!!! Example "Route Rules for Two Wireless Interface with Hotspot on wlan1"
<!-- prettier-ignore-end -->

```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-ports 22
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 80
sudo iptables -t nat -A PREROUTING -i wlan1 -p udp --dport 53 -j REDIRECT --to-ports 53
sudo iptables -t nat -A PREROUTING -i wlan1 -p tcp --syn -j REDIRECT --to-ports 9040
```

Save and apply iptables rules

```bash
sudo sh -c "iptables-save > /etc/iptables.ipv4.nat"
```

## Testing

Well Thats about it, you should be able to connect the the Hotspot and gain tor network.  
You can test that you are on the Tor network at [https://check.torproject.org/](https://check.torproject.org/){target=\_blank}

### Buy As a Beer

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="../../assets/images/about/donation/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->

### Few Beers...

Specify the amount you would like to donate

<!-- Paypal Button - any amount -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="MRPWZPFN84MP4"><input type="image" src="../../assets/images/about/donation/paypalDonate.png" width="200px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Paypal Button - any amount -->
