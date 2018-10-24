title: Linux - Sophos Firewall
description: Linux - Sophos Firewall how to, guides, examples, and simple usage

# Sophos Firewall

## Rebuild Sophos when disk full

```bash
/etc/init.d/postgresql92 rebuild
```

On older versions:

```bash
/var/mdw/scripts/smtp stop
dropdb -U postgres smtp
createdb -U postgres smtp
/var/mdw/scripts/smtp start
```

## Clear allowed networks on Sophos

Login to the Sophos

```bash
Type ‘cc’
In cc, you’ll be in MAIN, if not, type ‘MAIN’
Type ‘webadmin'
Type ‘allowed_networks@'
=['REF_NetworkAny']
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="220px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->
