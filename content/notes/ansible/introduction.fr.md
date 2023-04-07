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

{{< /note >}}