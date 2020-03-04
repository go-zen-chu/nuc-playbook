# nuc-playbook

playbook for my NUC setup.

## structure

Follows [best practice structure](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)

## Prerequisite

Programs below should be installed & enabled

- sshd: ansible uses for ssh
- python: ansible uses when running playbook
- dhcpcd: network connection from ansible origin is required

## Run

```bash
# edit according to your env
$ vim hosts.yml
$ ansible-playbook -i hosts.yml site.yml
```
