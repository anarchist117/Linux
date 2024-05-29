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


# Container runtimes
#### Step 1: Installing containerd

Download the `containerd-<VERSION>-<OS>-<ARCH>.tar.gz` archive from https://github.com/containerd/containerd/releases ,
verify its sha256sum, and extract it under `/usr/local`:

```console
wget https://github.com/containerd/containerd/releases/download/v1.7.17/containerd-1.7.17-linux-amd64.tar.gz
tar Cxzvf /usr/local containerd-1.7.17-linux-amd64.tar.gz
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

3. Add the appropriate Kubernetes `apt` repository.
   Please note that this repository have packages only for Kubernetes 1.30

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

# Installing a container runtime (Containerd)
1. Set up Docker's `apt` repository.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
   
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
2. Install the containerd packages:
   
```bash
sudo apt-get install containerd.io
```

3. Remove default config file and restart service containerd
```bash
rm /etc/containerd/config.toml
systemctl restart containerd.service
```
