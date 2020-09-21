---
description: Raspberry Pi Tips & Tricks how to, guides, examples, and simple usage, Raspberry Pi, Default User and Password, Install Oh-My-Zsh on Raspbian
---

<link rel="stylesheet" href="/assets/CSS/roundedCorners.css">

# Raspberry Pi Tips & Tricks

## Default User and Password After Installation

```bash
User: pi
Password: raspberry
```

## Basic Configuration

```bash
sudo raspi-config
```

## Update OS

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

## Install Oh-My-Zsh on Raspbian

```bash
sudo apt-get install -y zsh && sudo apt-get install -y git
sudo wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh && chsh -s `which zsh`
sudo usermod -s /usr/bin/zsh pi
```

Optional:
Setting fishy skin:

```bash
sudo sed -i 's/robbyrussell/fishy/g' ~/.zshrc
```

Its preferred to reboot after installation:

```bash
sudo reboot
```

## Fixing Locale failed for ZSH

This warning pops up in terminal:

```bash
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
    LANGUAGE = (unset),
    LC_ALL = (unset),
    LC_CTYPE = "UTF-8",
    LANG = "en_IL"
    are supported and installed on your system.
perl: warning: Falling back to a fallback locale ("en_IL").
```

run this:

```bash
echo "export LC_ALL=C" >> ~/.zshrc && source ~/.zshrc
```

## Show Raspberry Temperature

```bash
/opt/vc/bin/vcgencmd measure_temp
```

## Samba for RaspberryPi

```bash
sudo apt-get update
sudo apt-get install -y samba samba-common-bin smbclient cifs-utils
sudo smbpasswd -a pi ( my-pi-samba-remote-password )
sudo nano /etc/samba/smb.conf
```

change:

```bash
workgroup = YOUR WINDOWS WORKGROUP NAME
```

add at end:

```bash
[share]
    path = /home/pi/Desktop/share
    available = yes
    valid users = pi
    read only = no
    browsable = yes
    public = yes
    writable = yes
```

`the shared path must exist: ( if you work via desktop ( HDMI or VNC ) it is very convenient just to read or drop from/to this shared dir ) mkdir /home/pi/Desktop/share`

```bash
sudo reboot
```

Start samba Server

```bash
sudo /usr/sbin/service smbd start
```

## Clone Raspberry Pi SD Card

### Linux

On Linux, you can use the standard dd tool:

```bash
dd if=/dev/sdx of=/path/to/image bs=1M
```

### Mac

On Mac, you can also use the standard dd tool with a slightly different syntax:

```bash
dd if=/dev/rdiskx of=/path/to/image.img bs=1m
```

Where `/dev/rdiskx` is your SD card.

(using rdisk is preferable as its the raw device - quicker)

To find out which disk your device is type `diskutil list` at a command prompt - also, you may need to be root; to do this type `sudo -s` and enter your password when prompted.

### Windows

#### Option 1

On Windows, you can use the reverse process that you used when flashing the SD card.

You can use [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/), which is the preferred tool for flashing a SD card of the Foundation. Just enter the filename (the location and name of the backup image file to be saved), select the device (the SD card) and press read:

![89CMl.png](https://i.stack.imgur.com/89CMl.png)

Of course, you can also use [RawWrite](http://www.chrysocome.net/rawwrite), [dd for Windows](http://www.chrysocome.net/dd) or similar tools, the process is quite similar.

#### Option 2

If you don't want to back up your entire system, but only specific files, I suggest you connect to your Raspberry Pi via SFTP and copy the files to your local computer (You can use the [WinScp](http://winscp.net/eng/index.php) client). If you have SSH enabled, SFTP usually requires no special configuration on the Raspberry Pi side.

Another option is to [copy the files to a remote system using rsync](https://raspberrypi.stackexchange.com/questions/5427/can-a-raspberry-pi-be-used-to-create-a-backup-of-itself/).

You can also install special drivers so your Windows can read `ext` filesystems (and will thus be able to read the whole SD card), such as [ext2fsd](http://www.ext2fsd.com/) but it is probably not worth the effort.

---

**Since the image will be of the same size as your SD card, you may want to compress it. This can be achieved simply by using your favorite compression tool, such as gzip, 7zip, WinZip, WinRar ...**
