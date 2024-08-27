# SSH Config
```
# /etc/ssh/sshd_config

PasswordAuthentication no
PubkeyAuthentication yes
```
```
service ssh restart
```
# Copy ID_RSA.pub
```
ssh-copy-id root@server
```
