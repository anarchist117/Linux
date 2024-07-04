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
```

### Apply exports config
```
exportfs -a
```
