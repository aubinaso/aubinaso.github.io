---
title: Ansible Introduction
weight: 10
menu:
  notes:
    name: Introduction
    identifier: notes-ansible-introduction
    parent: notes-ansible
    weight: 10
---

<!-- Introduction -->
{{< note title="Introduction" >}}

# What is Ansible ?
`Ansible` is an open-source configuration management, software provisioning and application deployment tool that makes automating  your application deployments and IT infrastructure operation very simple. It is an agentless solution and easy to configure unlike other automation tool like `Puppet` or `Chef`

# Installation
Ansible rely on SSH and Python to do all automation and so you only need to install Ansible on the control node and make sure that OpenSSH and Python is installed on both the **control** (*Where the Ansible is install*) and the **node** (*host which needs to be configure*).
When configuring network equipments, there is another way to configure node since it isn't possible to install python (Python 3 recommended) on these host.

Here are some way to install Ansible :
- via PIP
- via binary
- via repository
- docker

## PIP
```bash
sudo apt install python3-pip
VERSION=3
pip install ansible==$VERSION
ansible --version
```
## Binary
```bash
git clone https://github.com/ansible/ansible.bit
cd ansible
source ./hacking/env-setup
sudo apt install python3-pip
pip install --user -r ./requirements # Module installation for Jinja
```
## Repository
```bash
apt-add-repository --yes --update ppa:/ansible/ansible-2.9
sudo apt install ansible
ansible --version
```

# Notes and Recommendations
Even though you can use the root user in Ansible to run Ad-Hoc commands and playbooks, it is not considered a best practice due to the security risks that can arise bys allowing root user ssh access. For this reason, it's is recommended to create a dedicated Ansible user with sudo privileged on every node and on the manager.
```bash
useradd -m aubin
echo "aubin ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers
```
Now configure the SSH Key to access node without using password
```bash
ssh-keygen
ssh-copy-id node[1-x]
```

Configurer Python3 comme interpreteur par défaut de Ansible. On pourra faire un lien de `/usr/bin/python` vers `python3` ou alors on doit configurer la valeur de `ansible_python_interpreter=/usr/bin/python3` dans le fichier `ansible.cfg`


{{< /note >}}