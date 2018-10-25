title: Linux - Plesk
description: Linux - Plesk how to, guides, examples, and simple usage

# Plesk

## Plesk on CentOS 12 bind fix

The problem was nginx was attempting to bind to port 443 before the IP was initialized.
To fix edit the /etx/sysctl.conf file and add:

```bash
net.ipv4.ip_nonlocal_bind = 1
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->