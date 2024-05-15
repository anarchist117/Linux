# Linux
### Architecture
```bash
uname -mov
#1 SMP PREEMPT Debian 1:6.6.20-1+rpt1 (2024-03-07) aarch64 GNU/Linux
```
### swap
```bash
nano /etc/fstab
# /swap.img     none    swap    sw      0       0
```
```bash
swapoff -a
```
```bash
rm /swap.img
```
```bash
free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       200Mi       1.4Gi       1.0Mi       281Mi       1.6Gi
Swap:             0B          0B          0B
```
