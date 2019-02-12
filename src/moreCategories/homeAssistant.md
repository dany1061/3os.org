# Home-Assistant

## [Home-Assistant.io](https://www.home-assistant.io/) Installation on Ubuntu 18.04 (host) & Docker

```bash
sudo apt-get update && sudo apt-get upgrade --yes
sudo apt-get -y install apparmor-utils apt-transport-https avahi-daemon ca-certificates curl dbus jq network-manager socat software-properties-common bash openssh-server
curl -sSL https://get.docker.com | sh
curl -sL https://raw.githubusercontent.com/home-assistant/hassio-build/master/install/hassio_install | sudo bash -s
```

```bash
sudo -s
add-apt-repository universe
apt-get upgrade
apt-get update
apt-get install -y bash jq curl avahi-daemon dbus network-manager apparmor-utils
apt-get install -y apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"

curl -sL https://raw.githubusercontent.com/home-assistant/hassio-build/master/install/hassio_install | bash -s
```

```bash
docker pull portainer/portainer
docker run \
-d \
--name=portainer \
--restart always \
-p 9000:9000 \
-v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```
