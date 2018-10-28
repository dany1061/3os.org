title: Ubiquiti Networks
description: Ubiquiti Networks how to, guides, examples, and simple usage

# Ubiquiti Networks

## EdgeRouter - SSH via RSA keys

SSH to the Edge Router:
Copy the public key to /tmp folder

Run:

```bash
configure
loadkey [your user] /tmp/id_rsa.pub
```

Check that the keys are working by opening new session

```bash
set service ssh disable-password-authentication
commit ; save
```

## Hardening EdgeRouter

This will change the GUI to port 8443, disable old cyphers, Only will listen on internal Network.
assuming your Edge Router IP is 192.168.1.1, if not change it accordingly.

SSH to the Edge Router

```bash
configure
set service gui listen-address 192.168.1.1
set service gui https-port 8443
set service gui older-ciphers disable
set service ssh protocol-version v2
commit ; save
```

## EdgeRouter OpenVPN Configuration 443/TCP

This Guide is based on [Original guide form ubnt support](https://help.ubnt.com/hc/en-us/articles/115015971688-EdgeRouter-OpenVPN-Server) with modifications to the VPN port and protocol

For the purpose of this article, it is assumed that the routing and interface configurations are already in place and that reachability has been tested.

ssh to the EdgeRouter

Make sure that the date/time is set correctly on the EdgeRouter.

```bash
show date
Thu Dec 28 14:35:42 UTC 2017
```

Log in as the root user.

```bash
sudo su
```

Generate a Diffie-Hellman (DH) key file and place it in the /config/auth directory. This Will take some time...

```bash
openssl dhparam -out /config/auth/dh.pem -2 2048
```

Change the current directory.

```bash
cd /usr/lib/ssl/misc
```

Generate a root certificate (replace <secret> with your desired passphrase).

```bash
./CA.sh -newca
```

exmaple:

PEM Passphrase: <secret>
Country Name: `US`
State Or Province Name: `New York`
Locality Name: `New York`
Organization Name: `Ubiquiti`
Organizational Unit Name: `Support`
Common Name: `root`
Email Address: `support@ubnt.com`

**`NOTE: The Common Name needs to be unique for all certificates.`**

Copy the newly created certificate + key to the /config/auth directory.

```bash
./CA.sh -newreq
```

exmaple:

Country Name: `US`
State Or Province Name: `New York`
Locality Name: `New York`
Organization Name: `Ubiquiti`
Organizational Unit Name: `Support`
Common Name: `server`
Email Address: `support@ubnt.com`

Sign the server certificate.

```bash
./CA.sh -sign
```

Move and rename the server certificate + key to the /config/auth directory.

```bash
mv newcert.pem /config/auth/server.pem
mv newkey.pem /config/auth/server.key
```

Generate, sign and move the client1 certificates.

```bash
./CA.sh -newreq
```

Common Name: client1

```bash
./CA.sh -sign
mv newcert.pem /config/auth/client1.pem
mv newkey.pem /config/auth/client1.key
```

(Optional) Repeat the process for client2.

```bash
./CA.sh -newreq
```

Common Name: client2

```bash
./CA.sh -sign
mv newcert.pem /config/auth/client2.pem
mv newkey.pem /config/auth/client2.key
```

Verify the contents of the /config/auth directory.

```bash
ls -l /config/auth
```

You should have those files:

- cacert.pem
- cakey.pem
- client1.key
- client1.pem
- client2.key
- client2.pem
- dh.pem
- server.key
- server.pem

Remove the password from the client + server keys. This allows the clients to connect using only the provided certificate.

```bash
openssl rsa -in /config/auth/server.key -out /config/auth/server-no-pass.key
openssl rsa -in /config/auth/client1.key -out /config/auth/client1-no-pass.key
openssl rsa -in /config/auth/client2.key -out /config/auth/client2-no-pass.key
```

Overwrite the existing keys with the no-pass versions.

```bash
mv /config/auth/server-no-pass.key /config/auth/server.key
mv /config/auth/client1-no-pass.key /config/auth/client1.key
mv /config/auth/client2-no-pass.key /config/auth/client2.key
```

Return to operational mode.

```bash
exit
```

Enter configuration mode.

```bash
configure
```

If EdgeRouter's Interface is on port 433, you must change it.

```bash
set service gui https-port 8443
commit ; save
```

Add a firewall rule for the OpenVPN traffic to the local firewall policy.

```bash
set firewall name WAN_LOCAL rule 30 action accept
set firewall name WAN_LOCAL rule 30 description OpenVPN
set firewall name WAN_LOCAL rule 30 destination port 433
set firewall name WAN_LOCAL rule 30 protocol tcp
```

Configure the OpenVPN virtual tunnel interface.

```bash
set interfaces openvpn vtun0 mode server
set interfaces openvpn vtun0 server subnet 172.16.1.0/24
set interfaces openvpn vtun0 server push-route 192.168.1.0/24
set interfaces openvpn vtun0 server name-server 192.168.1.1
set interfaces openvpn vtun0 openvpn-option --duplicate-cn
set openvpn vtun0 local-port 443
set openvpn-option "--push redirect-gateway"
set protocol tcp-passive
```

Link the server certificate/keys and DH key to the virtual tunnel interface.

```bash
set interfaces openvpn vtun0 tls ca-cert-file /config/auth/cacert.pem
set interfaces openvpn vtun0 tls cert-file /config/auth/server.pem
set interfaces openvpn vtun0 tls key-file /config/auth/server.key
set interfaces openvpn vtun0 tls dh-file /config/auth/dh.pem
commit ; save
```

Exmaple for clinet.opvn config:

```bash
client
dev tun
proto udp
remote <server-ip or hostname> 443
float
resolv-retry infinite
nobind
persist-key
persist-tun
verb 3
ca cacert.pem
cert client1.pem
key client1.key
```

## EdgeRouter Free Up space by Cleaning Old Firmware

ssh to the EdgeRouter:

```bash
delete system image
```

## EdgeRouter task-scheduler

**`Work In Progress`**

```bash
configure
show system task-scheduler
set system task-scheduler task SSL_UPDATE interval 1d
```

## Installing UniFi Controller on Ubuntu 16.04

```bash
sudo apt update
sudo apt-get install openjdk-8-jdk-headless openjdk-8-jre-headless
echo 'deb http://www.ubnt.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/100-ubnt-unifi.list
sudo wget -O /etc/apt/trusted.gpg.d/unifi-repo.gpg https://dl.ubnt.com/unifi/unifi-repo.gpg
sudo apt update
sudo apt install unifi
sudo apt install haveged
sudo update-rc.d haveged defaults
reboot
```

Interface:

```markdown
https://<serversAdress>:8443
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->