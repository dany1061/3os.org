title: Linux - LVM Partition Linux
description: Linux - LVM Partition how to, guides

# Linux LVM Partitions

## Removing LVM Partition and Merging In To / (root partition)

Find out the names of the partition with df

```bash
df
```

You need to unmount the partition before you can delete them and marge __backup the data of the partition you would like to delete__ this exmaple will use "centos-home" as the partition that will be merged to the root partition.

```bash
unmount -a
lvremove /dev/mapper/centos-home
lvextend -l +100%FREE -r /dev/mapper/centos-root
```

After the merging and before mounting you should remove the partition from fastab

```bash
nano /etc/fstab
mount -a
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->