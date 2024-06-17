# Installing a new Hard Drive
```bash
fdisk -l
```
### Create Partition
```bash
fdisk /dev/sdb
g         # create a new empty GPT partition table
n         # Add a new partition
default   # Partition number
default   # First sector
default   # Last sector
w         # Write table to disk and exit
```

### Format Partition
```bash
mkfs.ext4 /dev/sdb1
```

### Mount Point
```bash
mkdir /mnt/data
```
```bash
nano /etc/fstab
/dev/sdb1 /mnt/data ext4 defaults 0 2
```



# Extend Partition
```
df -Th
```
### Rescan sdb disk
```bash
echo 1 > /sys/block/sdb/device/rescan
```
### Extending Partition
```bash
growpart /dev/sdb 1
```
### Resizing File System
```bash
resize2fs /dev/sdb1
```
