# SSH Config
```
# /etc/ssh/sshd_config

PasswordAuthentication no
PubkeyAuthentication yes
```
```
service ssh restart
```
# Copy id_rsa.pub
```
ssh-copy-id root@server

cat .ssh/id_rsa.pub >> /user/.ssh/authorized_keys
```
# Check key type
```
ssh-keygen -lf .ssh/id_rsa
```
