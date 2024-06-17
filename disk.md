# Installing a new Hard Drive
### Create Partition
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
```bash
echo 1 > /sys/block/sdb/device/rescan
```
```bash
fdisk /etc/sdb
w         # Write table to disk and exit
```
```bash
resize2fs /dev/sda1
```
