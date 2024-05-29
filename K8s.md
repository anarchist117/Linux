# 1. Before you begin
### System requirement
```bash
2 GB or more of RAM per machine (any less will leave little room for your apps).
2 CPUs or more.
```

### Disable swap
```bash
nano /etc/fstab
# /swap.img     none    swap    sw      0       0
```
```bash
swapoff -a
rm /swap.img
```



# 2. Installing a container runtime
### Enable IPv4 packet forwarding
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

#### Step 1: Installing containerd

Download the `containerd-<VERSION>-<OS>-<ARCH>.tar.gz` archive from https://github.com/containerd/containerd/releases ,
verify its sha256sum, and extract it under `/usr/local`:

```console
wget https://github.com/containerd/containerd/releases/download/v1.7.17/containerd-1.7.17-linux-amd64.tar.gz
tar Cxzvf /usr/local containerd-1.7.17-linux-amd64.tar.gz
```

##### systemd
If you intend to start containerd via systemd, you should also download the `containerd.service` unit file from
https://raw.githubusercontent.com/containerd/containerd/main/containerd.service into `/usr/local/lib/systemd/system/containerd.service`,
and run the following commands:

```bash
mkdir -p /usr/local/lib/systemd/system
wget https://raw.githubusercontent.com/containerd/containerd/main/containerd.service -O /usr/local/lib/systemd/system/containerd.service
systemctl daemon-reload
systemctl enable --now containerd
```

#### Step 2: Installing runc

Download the `runc.<ARCH>` binary from https://github.com/opencontainers/runc/releases ,
verify its sha256sum, and install it as `/usr/local/sbin/runc`.

```console
wget https://github.com/opencontainers/runc/releases/download/v1.1.12/runc.amd64
install -m 755 runc.amd64 /usr/local/sbin/runc
```

The binary is built statically and should work on any Linux distribution.

#### Step 3: Installing CNI plugins

Download the `cni-plugins-<OS>-<ARCH>-<VERSION>.tgz` archive from https://github.com/containernetworking/plugins/releases ,
verify its sha256sum, and extract it under `/opt/cni/bin`:

```console
mkdir -p /opt/cni/bin
wget https://github.com/containernetworking/plugins/releases/download/v1.5.0/cni-plugins-linux-amd64-v1.5.0.tgz
tar Cxzvf /opt/cni/bin cni-plugins-linux-amd64-v1.5.0.tgz
```

The binaries are built statically and should work on any Linux distribution.

### Customizing containerd

containerd uses a configuration file located in `/etc/containerd/config.toml` for specifying daemon level options.
A sample configuration file can be found [here](/docs/man/containerd-config.toml.5.md).
```bash
mkdir /etc/containerd
containerd config default > /etc/containerd/config.toml
```
The default configuration can be generated.

#### Configuring the `systemd` cgroup driver and Overriding the sandbox (pause) image

To use the `systemd` cgroup driver in `/etc/containerd/config.toml` with `runc`, set

```
[plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
  ...
  [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
    SystemdCgroup = true

[plugins."io.containerd.grpc.v1.cri"]
  sandbox_image = "registry.k8s.io/pause:3.9"
```

If you apply this change, make sure to restart containerd:

```shell
systemctl restart containerd
```



# 3. Installing kubeadm, kubelet and kubectl
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
