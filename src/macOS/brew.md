title: Home Brew
description: Home Brew, examples and simple usage

# Home Brew

## Installing Homebrew

run this at terminal:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## BrewUP - Upgrades Brew & Casks Packages, macOS AppStore Apps

This script will perform the following:

- Cheeks for required packages, installs them if missing
- Runs brew doctor - display if there are `errors` in brew
- Updates brew packages
- Updates brew casks
- Updates macOS AppStore Apps
- Cleanups all unused packages

Installation: Run at Terminal

```bash
curl -fsSL https://git.io/fxlRD -o brewup
mv brewup /usr/local/bin/
chmod +x /usr/local/bin/brewup
```

Run brewup:

```bash
brewup
```

done.

Source:
[gist](https://gist.github.com/fire1ce/f9b6645b4c8cff5b7229e5011a168a47)
<script src="https://gist.github.com/fire1ce/f9b6645b4c8cff5b7229e5011a168a47.js"></script>

## Useful Packages

| Package           | Description                         |
|-------------------|-------------------------------------|
| htop              | resource monitor                    |
| wget              |                                     |
| nmap              |                                     |
| geoip             | geolocation data for an inputted IP |
| speedtest_cli     | speed test via cli                  |
| telnet            | telnet client                       |
| mas               | app store apps updater              |
| terminal-notifier | terminal notifier for macOS         |

## Brew Cask

```bash
brew cask install 'package name'
```

Packages:

- 1password
- visual-studio-code
- iterm2
- google-chrome
- alfred
- Bartender
- CyberDuck
- Deluge
- Dropbox
- Dropshare
- Etcher
- Firefox
- Geekbench
- google-drive-file-stream
- Insomnia
- istat-menus
- Krita
- micro-snitch
- rambox
- spotify
- snagit
- keka
- TimeMachineEditor
- TunnelBear
- tunnelblick
- VLC
- Wireshark
- Zenmap
- highsierramediakeyenabler
- android-platform-tools

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->