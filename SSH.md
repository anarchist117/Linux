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
```
# Check key type
```
ssh-keygen -lf .ssh/id_rsa
```
