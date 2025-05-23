# 1. Global config
### Set username and email address
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```
```bash
git config --list
```

# 2. Create a new repository
```bash
cd /home/user/project
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/anarchist117/repository.git
git push -u origin main
```
```bash
git status
```
# 3. Managing personal access tokens
[Creating a fine-grained personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token)

[Creating a personal access token (classic)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic)

# Other command
```
git tag
git checkout v2.26.0
git describe --tag
git switch -
```
