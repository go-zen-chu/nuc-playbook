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
pacman -S --noconfirm openssh python dhcpcd
```

## Run & setup

```bash
# edit according to your env
$ vim hosts.yml
$ ansible-playbook -i hosts.yml site.yml
```

On the first run, it disables ssh login with root user but creates ansible user instead for security.
