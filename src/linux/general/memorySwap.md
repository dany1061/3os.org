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
