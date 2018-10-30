title: Linux Files Handling
description: Linux - Files Handling how to, guides, examples, and simple usage

# Linux Files Handling

## SMB Mount on Linux With Credentials

```bash
sudo apt-get install cifs-utils
nano ~/.smbcredentials
```

add this to the config.

```bash
username=msusername
password=mspassword
```

Save the file, exit the editor.
Change the permissions of the file to prevent unwanted access to your credentials:

```bash
chmod 600 ~/.smbcredentials
```

Then edit your /etc/fstab file (with root privileges) to add this line (replacing the insecure line in the example above, if you added it):

```bash
//servername/sharename /media/windowsshare cifs vers=1.0,credentials=/home/ubuntuusername/.smbcredentials,iocharset=utf8,sec=ntlm 0 0
```

Save the file, exit the editor.

Finally, test the fstab entry by issuing:

```bash
sudo mount -a
```

If there are no errors, you should test how it works after a reboot. Your remote share should mount automatically.

## Find big files and folders

```bash
find / -mount -type f -print0 2>/dev/null | xargs -0 du 2>/dev/null | sort -n | tail -40 | cut -f2 | xargs -I{} du -sh 2>/dev/null {} | uniq; printf '+%.0s' {1..100}; echo; \
find / -mount -type d -print0 2>/dev/null | xargs -0 du 2>/dev/null | sort -n | tail -40 | cut -f2 | xargs -I{} du -sh 2>/dev/null {} | uniq; printf '+%.0s' {1..100}; echo; \
du -sh /var/cpanel/user_notifications && du -sh /backup/cpbackup/*/dirs/_var_cpanel/user_notifications
```

## Delete files with a large file list - Argument list too long

```bash
find . -name '*'|xargs rm
```

## Change permissions (chmod) to folders and files

```bash
find . -type d -exec chmod 755 {} +
find . -type f -exec chmod 644 {} +
```

## Change permissions to all files and folders

```bash
chown `stat -c %U .`.`stat -c %U .` * -R
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="150px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"></form>
<!-- Donation Button -->