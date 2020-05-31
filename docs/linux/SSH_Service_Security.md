---
description: Linux - SSH Service Security how to, guides, examples, and simple usage
---

# SSH Service Security

## SSH Login With RSA Keys

### Copy Public Key to The Server

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
```

__Or Do It Manually :__

ssh to the host (`do not close this connection`)

```bash
mkdir -p ~/.ssh && touch .ssh/authorized_keys
```

copy your public key usually located at `~/.ssh/id_rsa.pub`

```bash
echo PUCLICK_Key_STRING >> ~/.ssh/authorized_keys
```

### Configure sshd Service

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
