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
# or
cat .ssh/id_rsa.pub >> /user/.ssh/authorized_keys
```
# Check key type
```
ssh-keygen -lf .ssh/id_rsa
```
# SSH Tunnel
```
ssh -L8001:localhost:8001 user@remote-host
```
