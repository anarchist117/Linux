### Installing A New Hard Drive
```bash
fdisk -l



Disk /dev/sda: 25 GiB, 26843545600 bytes, 52428800 sectors
Disk model: Virtual disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: A58C9653-526D-48D8-A25B-395A65B61CA7

Device       Start      End  Sectors  Size Type
/dev/sda1     2048  2203647  2201600    1G EFI System
/dev/sda2  2203648  6397951  4194304    2G Linux filesystem
/dev/sda3  6397952 52426751 46028800 21.9G Linux filesystem

Disk /dev/mapper/ubuntu--vg-ubuntu--lv: 10.97 GiB, 11781799936 bytes, 23011328 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```
