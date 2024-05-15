# Enable IPv4 packet forwarding
To manually enable IPv4 packet forwarding:
```shell
# sysctl params required by setup, params persist across reboots
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF

# Apply sysctl params without reboot
sudo sysctl --system
```
Verify that `net.ipv4.ip_forward` is set to 1 with:
```shell
sysctl net.ipv4.ip_forward
```


# Installing kubeadm, kubelet and kubectl
1. Update the `apt` package index and install packages needed to use the Kubernetes `apt` repository:

```shell
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```

2. Download the public signing key for the Kubernetes package repositories.
   The same signing key is used for all repositories so you can disregard the version in the URL:

```shell
# If the directory `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

3. Add the appropriate Kubernetes `apt` repository. Please note that this repository have packages
   only for Kubernetes {{< skew currentVersion >}}; for other Kubernetes minor versions, you need to
   change the Kubernetes minor version in the URL to match your desired minor version
   (you should also check that you are reading the documentation for the version of Kubernetes
   that you plan to install).

```shell
# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

4. Update the `apt` package index, install kubelet, kubeadm and kubectl, and pin their version:

```shell
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

5. (Optional) Enable the kubelet service before running kubeadm:

```shell
sudo systemctl enable --now kubelet
```
