title: Linux Memory & Swap
description: Linux Memory & Swap how to, guides, examples, and simple usage

# Linux Memory & Swap

## Who uses RAM

```bash
ps aux  | awk '{print $6/1024 " MB\t\t" $11}'  | sort -n
```

## Prevent OOM killer

Edit file /etc/sysctl.conf

```bash
vm.overcommit_memory = 2
vm.overcommit_ratio = 100
```

In case of bad memory usage (php out of memory) use this settings:

```bash
vm.overcommit_memory = 0
vm.overcommit_ratio = 80
```

## Who is using SWAP

```bash
grep VmSwap /proc/*/status 2>/dev/null | sort -nk2 | tail -n5
```

## Clear cache and swap

```bash
echo 3 > /proc/sys/vm/drop_caches && swapoff -a && swapon -a
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="220px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->