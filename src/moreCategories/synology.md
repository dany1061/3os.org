title: Synology DSM
description: Synology how to, guides, examples, and simple usage

# Synology

## Allow SSH With RSA KEY

-   Log into Synology web UI as an administrator user
-   Enable “User Home”
-   Control Panel / User / Advanced, scroll down to “User Home”
-   Check “Enable user home service”, select an appropriate Location (i.e. volume1)
-   Click “Apply”

SSH into Synology as `Admin User`

```bash
sudo chmod 755 /volume1/homes/*youruser*
mkdir ~/.ssh && chmod 0700 ~/.ssh
touch ~/.ssh/authorized_keys && chmod 0644 ~/.ssh/authorized_keys
echo PUCLICK_Key_STRING >> ~/.ssh/authorized_keys
```

Configure the Synology’s SSH service to allow login by key

```bash
sudo vi /etc/ssh/sshd_config
```

-   Uncomment line that says: #PubkeyAuthentication yes
-   Uncomment the line that says: #AuthorizedKeyFiles .ssh/authorized_keys
-   Add a line: PasswordAuthentication no
-   Make sure that line is uncommented that says: ChallengeResponseAuthentication no
-   Save the file and exit the editor

```bash
sudo synoservicectl --restart sshd
```

You should now connect with rsa key.

## Installing VM Tools on Linux VM

On Debian:

```bash
sudo add-apt-repository universe
sudo apt-get install qemu-guest-agent
```

On CentOS 7:

```bash
yum install -y qemu-guest-agent
```

On CentOS 8:

```bash
dnf install -y qemu-guest-agent
```

## Automated SSL Using Let's Encrypt, CloudFlare API, acme.sh Script

### Requirements

Synology ssh enabled and sudo permission
Cloudflare API key

ssh to synology nas

```bash
sudo -i
wget https://github.com/Neilpang/acme.sh/archive/master.tar.gz
tar xvf master.tar.gz
cd acme.sh-master/
./acme.sh --install --nocron --home /usr/local/share/acme.sh --accountemail "email@example.com"
```

CF_Key= `your cloudflare Global API key`
CF_Email= `your cloudflare email account`
CERT_DOMAIN= `your domain managed on cloudflare dns`, you can use wilde card domain like `*.your-domain.tld`

```bash
export CF_Key="MY_SECRET_KEY_SUCH_SECRET"
export CF_Email="myEmail@example.com"
export CERT_DOMAIN="*.your-domain.tld"
export CERT_DNS="dns_cf"
```

This Will Generate, Sing and install the Certificate

### Creating the Certificate

```bash
cd /usr/local/share/acme.sh
./acme.sh --issue -d "$CERT_DOMAIN" --dns "$CERT_DNS" \
      --certpath /usr/syno/etc/certificate/system/default/cert.pem \
      --keypath /usr/syno/etc/certificate/system/default/privkey.pem \
      --fullchainpath /usr/syno/etc/certificate/system/default/fullchain.pem \
      --capath /usr/syno/etc/certificate/system/default/chain.pem \
      --reloadcmd "cp -a /usr/syno/etc/certificate/system/default/* `find /usr/syno/etc/certificate/_archive/ -maxdepth 1 -mindepth 1 -type d` && /usr/syno/sbin/synoservicectl --reload nginx" \
      --dnssleep 20 \
      --config-home "/volume1/activeShare/Dropbox/SettingsConfigs/SSL_Certificates"
```

### Configuring Certificate Renewal by /etc/crontab

```bash
vi /etc/crontab
```

add this:

```bash
0   10  2   *   *   root    /usr/local/share/acme.sh/acme.sh --cron --home /volume1/activeShare/Dropbox/SettingsConfigs/SSL_Certificates
```

### done

## CloudFlare DDNS

based on this [SynologyCloudflareDDNS](https://github.com/joshuaavalon/SynologyCloudflareDDNS)

Ssh to synology nas as root
Download cloudflareddns.sh from this repository to /sbin/cloudflaredns.sh

```bash
wget https://raw.githubusercontent.com/joshuaavalon/SynologyCloudflareDDNS/master/cloudflareddns.sh -O /sbin/cloudflaredns.sh
chmod +x /sbin/cloudflaredns.sh
```

Edit Synology's DDNS service config:

```bash
vi /etc.defaults/ddns_provider.conf
```

Add this to the config

```bash
[Cloudflare]
        modulepath=/sbin/cloudflaredns.sh
        queryurl=https://www.cloudflare.com/
```

Go to your cloudflare account
Go to your domain overview page and get the Zone ID.
Go to DNS zone and create A record you want to use for the DDNS with any IP address (just for the recored creation)
Go to your account setting page and get API Key.
Get record id using Cloudflare API.

Run this. You need to replace with [] with your parameter.

```bash
curl -X GET "https://api.cloudflare.com/client/v4/zones/[Zone ID]/dns_records" \
     -H "X-Auth-Email: [Email]" \
     -H "X-Auth-Key: [API Key]" \
     -H "Content-Type: application/json"
```

You will Get information acout your Zone in the response. Look for `ID` Recored you created before.

```bash
vi /sbin/cloudflaredns.sh
```

chnage **RECID**, **ZONE_ID** with the values you got before.

exmaple:

```bash
__RECTYPE__="A"
__RECID__="f3690c72ef24a964936f78760d62a3e1"
__ZONE_ID__="2ffb4915izhe84e5974b0dec74fcd4f2"
__TTL__="1"
__PROXY__="true"
```

**`__PROXY__ true/false depandes on your usage`**

Login to your DSM
Go to Control Panel > External Access > DDNS > Add
Select Cloudflare as service provider. Enter your domain as hostname, your Cloudflare account as Username/Email, and API key as Password/Key

At the console:

```bash
tail -f /var/log/cloudflareddns.log
```

Click Test Connection
You shoud see somthing like that at the console:

```bash
cloudflaredns.sh (7): Updating with 185.185.185.185...
cloudflaredns.sh (7): Status: good
```
