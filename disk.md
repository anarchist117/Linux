### Installing A New Hard Drive
```bash
fdisk -l

fdisk /dev/sdb
g         # create a new empty GPT partition table
n         # Add a new partition
default   # Partition number
default   # First sector
default   # Last sector
w         # Write table to disk and exit
```
