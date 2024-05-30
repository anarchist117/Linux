# Docker mirrors
```bash
nano /etc/docker/daemon.json
```
```bash
{
  "registry-mirrors" : [
    "https://mirror.gcr.io",
    "https://daocloud.io",
    "https://c.163.com",
    "https://registry.docker-cn.com"
  ]
}
```
```bash
systemctl restart docker
```
