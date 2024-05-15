# Linux
### Check Architecture
```bash
uname -mov
```
```bash
#1 SMP PREEMPT Debian 1:6.6.20-1+rpt1 (2024-03-07) aarch64 GNU/Linux
```
### Disable swap
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
```
