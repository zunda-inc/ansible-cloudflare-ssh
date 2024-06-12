
# Cloudflare Browser SSH Playbook
## Summary

This is a sample playbook for configuring Cloudflare Browser SSH using Ansible.

## Usage
### Install python
Install pyenv according to your environment.  
https://github.com/pyenv/pyenv?tab=readme-ov-file#installation

In Ubuntu 22.04 case,
```bash
sudo apt update -y && sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev curl libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
# install pyenv
curl https://pyenv.run | bash
# Add PATH
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile
# install python 3.12.3
pyenv install 3.12.3
pyenv global 3.12.3
```
### Prepare Ansible
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Update  `requirements.txt`  
```bash
pip freeze > requirements.txt
```
### Add cloudflare CA Keys
```bash
vim playbook/inventory/hosts.yml
# edit cloudflared_ca_key: "ecdsa-sha2-nistp256 AAAA"
```

### Execute Ansible

  ```bash
ansible-playbook cloudflare-ssh.yml -i inventory/hosts.yml --ask-become-pass --extra-vars "cloudflared_token=your_access_token"
```

## Licence

MIT License
