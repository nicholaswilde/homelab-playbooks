---
# :house_with_garden: Homelab Playbooks :rocket:

[![task](https://img.shields.io/badge/Task-Enabled-brightgreen?style=for-the-badge&logo=task&logoColor=white)](https://taskfile.dev/#/)
[![ci](https://img.shields.io/github/actions/workflow/status/nicholaswilde/homelab-playbooks/ci.yaml?label=ci&style=for-the-badge&branch=main)](https://github.com/nicholaswilde/homelab-playbooks/actions/workflows/ci.yaml)

[Ansible playbooks][1] repo for my [homelab][2].

---

## :pushpin: TL;DR

- **Install dependencies:** `task deps`
- **Generate a new vault password:** `task init`
- **Edit secrets:** `task ve`
- - **Edit role variables:** `ansible-vault edit roles/<role>/vars/main.yaml`
- **Update all hosts:** `ansible-playbook playbooks/update_all.yaml`
- **See all available tasks:** `task -l`

---

## :frame_with_picture: Background

This repository contains Ansible playbooks used to configure and manage my homelab environment. The playbooks are designed to be idempotent and are used to set up and maintain various services and configurations across different types of machines, including Ubuntu servers, Raspberry Pis, Proxmox VE nodes, LXC containers, and Docker hosts.

---

## :construction_worker: Prerequisites

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [Python](https://www.python.org/downloads/)
- [Task](https://taskfile.dev/installation/)

## :package: Installation

To get started, clone the repository and install the dependencies:

```bash
git clone https://github.com/nicholaswilde/homelab-playbooks.git
cd homelab-playbooks
task deps
```

For more detailed instructions, see the [Getting Started](./getting-started.md) guide.

## :hammer_and_wrench: Development

This project uses [Task](https://taskfile.dev/) for command running and [MkDocs](https://www.mkdocs.org/) for documentation.

For more information on development, see the [Development](./development.md) guide.

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
