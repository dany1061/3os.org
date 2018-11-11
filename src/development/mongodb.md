title: Development - Python
description: Development - Python how to, guides, examples, and simple usage

# MongoDB

## Secure MongoDB Replica Setup

ssh to server1
edit /etc/hosts to contain other two servers server2, server3
repeat action for all servers respectively

### Server Setup

ssh to server

```bash
cd to home directory
openssl rand -base64 756 > keyfile
chmod 400 keyfile
scp keyfile user@server2:~/
scp keyfile user@server3:~/

sudo chown mongodb:mongodb keyfile
sudo mv keyfile /var/lib/mongodb/
edit /etc/mongod.conf
```

Replace _#security_ with:

```config
#security:
  #keyFile: /var/lib/mongodb/keyfile
```

Replace _#replication_ with:

```config
replication:
  replSetName: rs0              (or whatever name you want)
```

Save edits and exit

```bash
sudo systemctl restart mongod.service
```

ssh to server2,server3 and repeat the [Server Setup](#server_setup) section

### Initiate Connection

ssh to the server
On server open mongo shell

```bash
rs.initiate()
rs.add('server2:27017')
rs.add('server3:27017')
```

Now one of the servers should be the PRIMARY and others should be SECONDARY

On the same server,

edit /etc/mongod.conf

Replace:

```config
#security:
  #keyFile: /var/lib/mongodb/keyfile
```

with:

```config
security:
  keyFile: /var/lib/mongodb/keyfile
```

Save edits and exit

```bash
sudo systemctl restart mongod.service
```

ssh to server2,server3 and repeat the [Initiate Connection](#initiate_connection) section

again one of the servers should be the PRIMARY and others should be SECONDARY
ssh to the PRIMARY server

run mongo shell

```bash
use admin
db.createUser({user: "yourUsernameHere", pwd: "yourPasswordHere", roles: [{role: "userAdminAnyDatabase", db: "admin"}, {role: "clusterAdmin", db: "admin"}]})
use myDB
db.createUser({user: "databaseUsernameHere", pwd: "databasePasswordHere", roles: [{role: "readWrite", db: "myDB"}]})
```

--------------------------------
to verify everything was done correctly

ssh to PRIMARY
run mongo shell

```bash
use admin
db.auth("yourUsernameHere", "yourPasswordHere")
```

OUTPUT SHOULD BE 1

```bash
use myDB
db.auth("databaseUsernameHere", "databasePasswordHere")
OUTPUT SHOULD BE 1
> for (var i = 0; i<= 10; i++) db.replicaTestCollection.insert( { x : i } )
> exit
```

ssh to any SECONDARY

```bash
> use myDB
> db.auth("databaseUsernameHere", "databasePasswordHere")
```

OUTPUT SHOULD BE 1

```bash
> db.replicaTestCollection.count()
OUTPUT SHOULD BE 10
```

Credit to [bergerg](https://github.com/bergerg "github.com/bergerg") for this guide.

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->