# Generate Certificate
```
ssh-keygen -t ed25519
```

# Copy Public Key
```
# Linux
ssh-copy-id root@server
```
```
# Windows
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh user@vm "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

# SSH Config
```
nano /etc/ssh/sshd_config.d/00-security.conf
```
```
PubkeyAuthentication yes
AuthenticationMethods publickey
KbdInteractiveAuthentication no
PermitRootLogin prohibit-password
PasswordAuthentication no
PermitEmptyPasswords no
X11Forwarding no
MaxAuthTries 3
LoginGraceTime 20
KexAlgorithms curve25519-sha256
HostKeyAlgorithms ssh-ed25519
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com
MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com
```
```
service ssh restart
```

# SSH Tunnel
```
ssh -L 80:localhost:3000 user@vm
```

# SSH Jumphost
```
ssh -J user@jumphost user@vm
```

# Documentation
[Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) </br>
https://sshaudit.online/
