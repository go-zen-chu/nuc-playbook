# nuc-playbook

Playbook for NUC setup.

## structure

Follows [best practice structure](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)

## Prerequisite

Programs below should be installed to the target manually before running this playbook.

- sshd: ansible uses for ssh
- python: ansible uses when running playbook
- dhcpcd: network connection from ansible origin is required

```bash
# on archlinux installed machine
pacman -Sy --noconfirm openssh python dhcpcd
# set root password for sshd
passwd

# from your laptop, check connectivity
nc -vz 192.168.x.x 22
```

## setup

At first, you need to setup your node.

```bash
# edit according to your env
vim .envrc
# if you use direnv then run below
direnv allow .
# if not run below
source .envrc
# envsubst read env vars and substitute them
envsubst < hosts-template.yml > hosts.yml
ansible-playbook -i hosts.yml initialize.yml
```

This will create ansible user to your node and configure ssh settings

## Create kubernetes cluster

```bash
vim hosts.yml
ansible-playbook -i hosts.yml site.yml
```

On the first run, it disables ssh login with root user but creates ansible user instead for security.

### kubernetes deploy

We use kustomize for applying manifest to k8s.
Use following command when you want to add resources to kustomization.yaml file in base dir.

```bash
cd roles/k8s/files/base
# declaritively add files to kustomization.yaml
kustomize edit add resources/monitoring/*
```

## How ansible runs

ansible-playbook command runs with root user.

- root: can do anything. make it simple
- ansible: non root application user. used for ssh login or running non root application.
