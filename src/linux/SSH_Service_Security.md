title: Linux - SSH Service Security
description: Linux - SSH Service Security how to, guides, examples, and simple usage

# SSH Service Security

## SSH Login With RSA Keys

ssh to the host (`do not close this connection`)

```bash
mkdir -p ~/.ssh && touch .ssh/authorized_keys
```

copy your public key usually located at `~/.ssh/id_rsa.pub`

```bash
echo PUCLICK_Key_STRING >> ~/.ssh/authorized_keys
```

edit `/etc/ssh/sshd_config`
change:

```bash
#PasswordAuthentication yes
```

to

```bash
PasswordAuthentication no
```

save&exit

restart ssh service:

```bash
sudo systemctl restart ssh
```

`Open New SSH Season and Test RSA Login`

---

### Optional: change ssh port

edit `/etc/ssh/sshd_config`
change the port to a desired one

```bash
port 1337
```

save&exit

restart ssh service:

```bash
sudo systemctl restart ssh
```

## Add Privet id_rsa key to Server

copy the id_rsa key to ~/.ssh folder

```bash
cd ~/.ssh
sudo ssh-agent bash
ssh-add id_rsa
```

### Open New SSH Season and Test RSA Login

```bash
ssh root@HOSTNAME.local -p <port>
```

example:

```bash
ssh example@192.168.1.99 -p 1337
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->