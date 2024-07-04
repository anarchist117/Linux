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

/mnt/data *(rw,sync,no_subtree_check)
# /mnt/share_1 192.168.0.0/24(rw,sync,no_subtree_check)
# /mnt/share_2 client2(ro,sync,no_subtree_check)
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
