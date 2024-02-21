# Ansible

## Table of Contents
- [Requirements](#requirements)
- [Usage](#usage)
- [Uninstalling](#uninstalling)

## Requirements

Before executing the ansible-playbook, ensure that the current version of the OS distribution has the necessary linux-headers package. For example, on Ubuntu/Debian, you can check it with this command:

```bash
apt search linux-headers-$(uname -r)
```

## Usage

Before running the playbook, ensure that you have added the necessary hosts to `env/hosts`. To execute the playbook, run:

```bash
ansible-playbook main.py
```

## Uninstalling

To uninstall specific components of the hbf-agent, set the variable `<component>_enabled: false`. If you uninstall the *hbf-agent* itself, any rules it created in *nft* will be automatically removed.
