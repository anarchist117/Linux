### Installing a new Hard Drive
```bash
fdisk -l
```
```bash
fdisk /dev/sdb
g         # create a new empty GPT partition table
n         # Add a new partition
default   # Partition number
default   # First sector
default   # Last sector
w         # Write table to disk and exit
```



### Format the new Partition
```bash
mkfs.ext4 /dev/sdb1
```
