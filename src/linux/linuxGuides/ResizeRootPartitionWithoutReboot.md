title: Linux - Resize Root Partition Without Reboot
description: Linux - Resize Root Partition Without Reboot how to, guides, examples, and simple usage

# Resize Root Partition Without Reboot

Resize HD size in VC Run: (replace the device if needed)

```bash
echo 1 > /sys/class/scsi_device/2\:0\:0\:0/device/rescan
run fdisk:
```

print the old partition and save the output delete the root partition create a new partition using the SAME start block and make sure that the end block is higher than previous one (enter, enter, enter…) write changes (ignore error) run:

```bash
partx -u /dev/sda
resize2fs -f /dev/sda3
```

Make sure everything is OK:

```bash
df -h
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->