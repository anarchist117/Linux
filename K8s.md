# Enable IPv4 packet forwarding
To manually enable IPv4 packet forwarding:
```bash
# sysctl params required by setup, params persist across reboots
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF

# Apply sysctl params without reboot
sudo sysctl --system
```
Verify that `net.ipv4.ip_forward` is set to 1 with:
```bash
sysctl net.ipv4.ip_forward
```
