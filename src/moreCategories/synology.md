title: Synology DSM
description: Synology how to, guides, examples, and simple usage

# Synology

## Allow SSH With RSA KEY

* Log into Synology web UI as an administrator user
* Enable “User Home”
* Control Panel / User / Advanced, scroll down to “User Home”
* Check “Enable user home service”, select an appropriate Location (i.e. volume1)
* Click “Apply”

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

* Uncomment line that says: #PubkeyAuthentication yes
* Uncomment the line that says: #AuthorizedKeyFiles .ssh/authorized_keys
* Add a line: PasswordAuthentication no
* Make sure that line is uncommented that says: ChallengeResponseAuthentication no
* Save the file and exit the editor

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

On Centos:

```bash
yum install qemu-guest-agent -y
```

## Automated SSL Using Let's Encrypt, CloudFlare API, acme.sh Script

ssh to synology nas

```bash
wget https://github.com/Neilpang/acme.sh/archive/master.tar.gz
tar xvf master.tar.gz
cd acme.sh-master/
./acme.sh --install --nocron --home /usr/local/share/acme.sh
cd /usr/local/share/acme.sh
```

CF_Key= `your cloudflare Global API key`
CF_Email= `your cloudflare email account`
CERT_DOMAIN= `your domain managed on cloudflare dns`, you can use wilde card domain like `*.your-domain.tld`

```bash
export CF_Key="MY_SECRET_KEY_SUCH_SECRET"
export CF_Email="<myEmail@example.com>"
export CERT_DOMAIN="your-domain.tld"
export CERT_DNS="dns_cf"
```

This Will Generate, Sing and install the Certificate

```bash
./acme.sh --issue -d "$CERT_DOMAIN" --dns "$CERT_DNS" \
      --cert-file /usr/syno/etc/certificate/system/default/cert.pem \
      --key-file /usr/syno/etc/certificate/system/default/privkey.pem \
      --fullchain-file /usr/syno/etc/certificate/system/default/fullchain.pem \
      --reloadcmd "/usr/syno/sbin/synoservicectl --reload nginx" \
      --dnssleep 20
```

### Automate The Certificate Renewal

* Login to DSM
* Go to Control Panel - Task Scheduler
* Create - Scheduled Task - User-defined script
* Name it something like that: `Lets-Encrypt Auto Renew`
* Run it under user root
* At Schedule define it to run dayily at night (so you won't have expierd certificate)
* at Task setting at this to the `user defined script` window:

```bash
 /usr/local/share/acme.sh/acme.sh --cron --home /usr/local/share/acme.sh/
```

* You can check if the script runs ok by ticking the `Send run details by mail` and provide your mail
* Close the window
* Select you newly created Task and Run it.
* Check you email, you should get massage like that:

```qoute
Dear user,

Task Scheduler has completed a scheduled task.

Task: Task 8
Start time: Tue, 04 Sep 2018 19:54:09 GMT
Stop time: Tue, 04 Sep 2018 19:54:09 GMT
Current status: 0 (Normal)
Standard output/error:
[Tue Sep 4 19:54:09 IDT 2018] ===Starting cron===
[Tue Sep 4 19:54:09 IDT 2018] Renew: '*.your-domain.tld'
[Tue Sep 4 19:54:09 IDT 2018] Skip, Next renewal time is: Sat Nov 3 16:34:19 UTC 2018
[Tue Sep 4 19:54:09 IDT 2018] Add '--force' to force to renew.
[Tue Sep 4 19:54:09 IDT 2018] Skipped *.your-domain.tld
[Tue Sep 4 19:54:09 IDT 2018] ===End cron===
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

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->