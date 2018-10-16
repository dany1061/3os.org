# Linux Files

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
