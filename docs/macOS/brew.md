# Home Brew

## Installing Homebrew

run this at terminal:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Brewup - Bash Script to Update & Upgrade Brew and Brew Casks

Download zip from this [gist](https://gist.github.com/fire1ce/f9b6645b4c8cff5b7229e5011a168a47/archive/295e72da089a4d130911007b7b61bf47a42171e1.zip)
Unzip, move the "brewup" file to /usr/local/bin/

```bash
mv brewup /usr/local/bin/
```

Add executable permissions:

```bash
chmod +x /usr/local/bin/brewup
```

run the command 'brewup'

## Useful Packages

| Package       | Description                         |
|---------------|-------------------------------------|
| htop          | resource monitor                    |
| wget          |                                     |
| nmap          |                                     |
| geoip         | geolocation data for an inputted IP |
| speedtest_cli | speed test via cli                  |
| telnet        | telnet client                       |

## Brew Cask

```bash
brew cask install 'Packadge name'
```

Package:
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