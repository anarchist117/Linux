# NFS Server
### Install the NFS Server
```
apt install nfs-kernel-server
```
### Create share folder
```
mkdir /mnt/data
chown nobody:nogroup /mnt/data
chmod 777 /mnt/data
```
### Configure shared permissions
```
nano /etc/exports

/mnt/data *(rw,sync,no_subtree_check,no_root_squash)
# /mnt/share_1 192.168.0.0/24(rw,sync,no_subtree_check)
# /mnt/share_2 client_ip(ro,sync,no_subtree_check)
```
### Apply exports config
```
exportfs -a
```

# NFS Client
### Enable NFS support
```
apt install nfs-common
```
### Create mount point
```
mkdir /mnt/nfs
```
### Mount NFS Share
```
mount nfs.server.com:/mnt/data /mnt/nfs
```
```
nano /etc/fstab

nfs.server.com:/mnt/data        /mnt/nfs    nfs     default    0 0
```

# Windows NFS Client
```powershell
Enable-WindowsOptionalFeature -FeatureName ServicesForNFS-ClientOnly, ClientForNFS-Infrastructure -Online -NoRestart
```
```cmd
mount -o anon nfs.server.com:/mnt/data Z:
```
