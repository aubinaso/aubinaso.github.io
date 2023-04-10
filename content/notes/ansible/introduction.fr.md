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

# C'est quoi Ansible ?
`Ansible` est un outil open-source de gestion de configuration, de provisionnement de logiciels et de déploiement d'applications qui rend très simple l'automatisation des déploiements d'applications et des opérations d'infrastructure informatique. C'est une solution sans agent et facile à configurer contrairement à d'autres outils d'automatisation comme `Puppet` ou `Chef`.

# Installation
Ansible s'appuie sur SSH et Python pour réaliser toute l'automatisation et il suffit donc d'installer Ansible sur le nœud de contrôle et de s'assurer qu'OpenSSH et Python sont installés à la fois sur le **contrôle** (*l'endroit où Ansible est installé*) et sur le **nœud** (*l'hôte qui a besoin d'être configuré*).
Lors de la configuration d'équipements réseau, il existe une autre façon de configurer le nœud car il n'est pas possible d'installer Python (Python 3 recommandé) sur ces hôtes.

Voici quelques méthodes pour installer Ansible :
- via PIP
- via le fichier binaire
- via les dépôts
- docker
## PIP
```bash
sudo apt install python3-pip
VERSION=3
pip install ansible==$VERSION
ansible --version
```
## Fichier binaire
```bash
git clone https://github.com/ansible/ansible.bit
cd ansible
source ./hacking/env-setup
sudo apt install python3-pip
pip install --user -r ./requirements # Module installation for Jinja
```
## Dépôts
```bash
apt-add-repository --yes --update ppa:/ansible/ansible-2.9
sudo apt install ansible
ansible --version
```

# Notes et Recommendations
Même si vous pouvez utiliser l'utilisateur root dans Ansible pour exécuter des commandes Ad-Hoc et des playbooks, cela n'est pas considéré comme une bonne pratique en raison des risques de sécurité qui peuvent survenir en permettant à l'utilisateur root d'accéder à ssh. Pour cette raison, il est recommandé de créer un utilisateur Ansible dédié avec des privilèges sudo sur chaque nœud et sur le manager.
```bash
useradd -m aubin
echo "aubin ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers
```
Configurez maintenant la clé SSH pour accéder au nœud sans utiliser de mot de passe.
```bash
ssh-keygen
ssh-copy-id node[1-x]
```

Configurer Python3 comme interpreteur par défaut de Ansible. On pourra faire un lien de `/usr/bin/python` vers `python3` ou alors on doit configurer la valeur de `ansible_python_interpreter=/usr/bin/python3` dans le fichier `ansible.cfg`

{{< /note >}}