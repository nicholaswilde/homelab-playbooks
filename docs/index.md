---
# :house_with_garden: Homelab Playbooks :rocket:

[![task](https://img.shields.io/badge/Task-Enabled-brightgreen?style=for-the-badge&logo=task&logoColor=white)](https://taskfile.dev/#/)
[![ci](https://img.shields.io/github/actions/workflow/status/nicholaswilde/homelab-playbooks/ci.yaml?label=ci&style=for-the-badge&branch=main)](https://github.com/nicholaswilde/homelab-playbooks/actions/workflows/ci.yaml)

[Ansible playbooks][1] repo for my [homelab][2].

---

## :pushpin: TL;DR

### :closed_lock_with_key: Vault Password

To create a new vault password file, use the `task init` command:

```shell
task init
```
This will create a `.vault_pass` file in the root directory. This file should be kept secret and is used to encrypt/decrypt sensitive variables. The `.vault_pass` file is encrypted using SOPS.

To decrypt the `.vault_pass.enc` file, use the `task decrypt` command:

```bash
task decrypt
```

To encrypt the `.vault_pass` file, use the `task encrypt` command:

```bash
task encrypt
```

Update passwords located in `inventory/group_vars/all.yaml`. To edit this file, use the following command:

```bash
task ve
```

Run playbook to setup a single LXC.

```bash
ansible-playbook playbooks/setup_lxcSingle.yaml
```

*   **Update all hosts:**
    ```bash
    ansible-playbook playbooks/update_all.yaml
    ```

*   **See all available tasks:**
    ```bash
    task -l
    ```

---

## :mag: &nbsp; Dynamic Proxmox Inventory

This project uses dynamic inventory for Proxmox VE. The inventory files `inventory/amd64.proxmox.yaml` and `inventory/arm64.proxmox.yaml` use the `community.proxmox.proxmox` plugin to connect to a Proxmox VE instance and retrieve information about LXC containers. This allows for dynamic discovery of hosts based on your Proxmox setup. The `ansible_host` variable is automatically set to the container's IP address.

---

## :scales: License

​[​Apache License 2.0](https://github.com/nicholaswilde/homelab-pull/raw/refs/heads/main/LICENSE)

## :pencil:​Author

​This project was started in 2025 by [​Nicholas Wilde​][3].

## :link: References

[1]: <https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html>
[2]: <https://nicholaswilde.io/homelab>
[3]: <https://nicholaswilde.io>
[4]: <https://www.youtube.com/watch?v=sn1HQq_GFNE>
[5]: <https://github.com/nicholaswilde/homelab-playbooks>
[6]: <https://fluxcd.io/>
[7]: <https://github.com/settings/keys>
[8]: <https://docs.ansible.com/ansible/latest/vault_guide/vault.html>
[9]: <https://github.com/nicholaswilde/homelab>
[10]: <https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html>
[11]: <https://github.com/jktr/ansible-pull-example>
[12]: <https://www.redhat.com/en/ansible-collaborative>
