<!-- markdownlint-disable-next-line no-trailing-punctuation -->
# :house_with_garden: homelab-playbooks :rocket:

[![task](https://img.shields.io/badge/task-enabled-brightgreen?logo=task&logoColor=white&style=for-the-badge)](https://taskfile.dev/)

Ansible playbooks for my [homelab][3]

---

## :framed_picture: Background

This repo is being used to push configurations to my homelab via SSH.

I'm in the process of using my [Homelab Pull repo][4] as a test of using GitOps, similar to [Flux CD][6], to configure my homelab by having each container pull this repo periodically and run ansible locally. Pros of this method are discussed in this [Learn Linux TV video][5].

A downside is that `ansible-pull` needs to be installed on all containers, thus taking up resources, which goes against my general homelab methodology.

---

## :hammer_and_wrench: &nbsp; Usage

### Vault Password

To create a new vault password file, use the `task init` command:

```shell
task init
```

This will create a `.vault_pass` file in the root directory. This file should be kept secret and is used to encrypt/decrypt sensitive variables.

### Running Playbooks

```shell
ansible-playbook playbooks/setup_lxc.yaml
Vault password:
```
---

## :gear: &nbsp; Variables

Variables are stored in `roles/<role>/vars/main.yaml` which is encrypted using [ansible-vault][2].

The vault password is prompted during run.

```yaml
# roles/<role>/vars/main.yaml
---
lxc_user: foo
ansible_user: bar
ansible_password: baz
```

---

## :mag: &nbsp; Dynamic Proxmox Inventory

This project uses dynamic inventory for Proxmox VE. The inventory files `inventory/amd64.proxmox.yaml` and `inventory/arm64.proxmox.yaml` use the `community.proxmox.proxmox` plugin to connect to a Proxmox VE instance and retrieve information about LXC containers. This allows for dynamic discovery of hosts based on your Proxmox setup. The `ansible_host` variable is automatically set to the container's IP address.


---

<!-- spellchecker-disable -->
## :balance_scale: &nbsp; License
<!-- spellchecker-enable -->

​[​Apache 2.0 License​](../LICENSE)

---

## :pencil:​&nbsp;​Author

​This project was started in 2024 by [Nicholas Wilde][1].

[1]: <https://github.com/nicholaswilde/>
[2]: <https://docs.ansible.com/ansible/latest/vault_guide/vault.html>
[3]: <https://nicholaswilde.io/homelab>
[4]: <https://github.com/nicholaswilde/homelab-pull>
[5]: <https://www.youtube.com/watch?v=sn1HQq_GFNE>
[6]: <https://fluxcd.io/>
