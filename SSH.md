# SSH Key
## Generate Certificate
```
ssh-keygen -t ed25519

# Legacy system that doesn't support the Ed25519 algorithm
ssh-keygen -t rsa -b 4096
```

## Copy public key
```
# Linux
ssh-copy-id root@server

# Windows
cat .ssh/id_rsa.pub >> /user/.ssh/authorized_keys
```

# SSH Config
```
# /etc/ssh/sshd_config

PasswordAuthentication no
PubkeyAuthentication yes
```
```
service ssh restart
```

## Check key type
```
ssh-keygen -lf .ssh/id_rsa
```

# SSH Tunnel
```
ssh -L8001:localhost:8001 user@remote-host
```
