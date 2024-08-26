# iptables list
```
iptaables -L
```

# Restrict access to SSH
```shell
iptables -A INPUT -p tcp --dport 22 --source 192.168.0.0/24 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```
# Remove rule
```shell
iptables -D INPUT -p tcp --dport 22 --source 192.168.0.0/24 -j ACCEPT
iptables -D INPUT -p tcp --dport 22 -j DROP
```
