![disk-volume](https://github.com/anarchist117/linux/blob/main/disk-volume.jpg)

# Installing a new Hard Drive
```bash
lsblk -f
# or
fdisk -l
```
### 1. Create Partition
```bash
fdisk /dev/sdb
g         # Create a new empty GPT partition table
n         # Add a new partition
default   # Partition number
default   # First sector
default   # Last sector
w         # Write table to disk and exit
```
```
parted -s /dev/sdb mklabel gpt
parted -s /dev/sdb mkpart primary ext4 1MiB 100%
```

### 2. Format Partition
```
mkfs.ext4 -L data /dev/sdb1
```
### 3. Mount Point
```bash
mkdir /mnt/data
```
```bash
echo "LABEL=data            /mnt/data ext4 defaults,nofail                     0 2" | tee -a /etc/fstab
```
```
systemctl daemon-reload
mount -a
```


# Extend Partition
```
df -Th
```
### 1. Rescan Disk
```bash
echo 1 > /sys/block/sdb/device/rescan

# For system partition
echo 1 > /sys/block/sda/device/rescan
```
### 2. Extending Partition
```bash
growpart /dev/sdb 1

# For system partition
growpart /dev/sda 3
lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```
### 3. Resizing File System
```bash
resize2fs /dev/sdb1

# For system partition
resize2fs /dev/ubuntu-vg/ubuntu-lv
```



# Convert MBR to GPT
### 1. Add unallocated disk space before convert
### 2. Convert partition table
```
gdisk /dev/sdb
w         # Write data
y         # Do you want to proceed?
```
