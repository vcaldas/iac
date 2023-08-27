# ansible-k3s-cluster

## Prepare env

```sh
ansible-galaxy install -r ./collections/requirements.yml
```

## Overview

- 4 Nodes running proxmox

## Check if the connection works

    Proxmox nodes have root
    
    ansible-playbook playbooks/check-connection.yaml --user root --ask-pass

## Steps

1 - Check if certificates are available, if not

```sh
    ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/ansible -C "youremail@something"
    ssh-copy-id -i ~/.ssh/ansible ansibleadmin@eachhost
    ansible all -m ping
```

2 - Prepare nodes for passwordless access

    ansible-playbook playbooks/onboard-proxmox.yaml

## Debug

% ansible -m debug -a 'var=hostvars[inventory_hostname]'  proxmox --ask-vault-pass

## kubernetes setup

 ansible-playbook playbooks/kube-infra.yaml
nsible-galaxy collection list
