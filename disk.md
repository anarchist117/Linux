### Installing A New Hard Drive
```bash
fdisk -l
fdisk /dev/sdb
n         # Add a new partition
p         # Primary partition type
1         # Partition number
default   # First sector
default   # Last sector
w         # Write table to disk and exit
```
