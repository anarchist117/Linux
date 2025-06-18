## Install Gitlab runner
```
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
apt install -y gitlab-runner
```
```
systemctl stop gitlab-runner
nano /etc/systemd/system/gitlab-runner.service
"--working-directory" "/root" "--user" "root"
systemctl daemon-reload
systemctl start gitlab-runner
```
```
gitlab-runner register
```
