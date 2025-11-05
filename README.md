# :house_with_garden: Homelab Playbooks

[![task](https://img.shields.io/badge/task-enabled-brightgreen?logo=task&logoColor=white&style=for-the-badge)](https://taskfile.dev/)

Ansible playbooks for my [homelab](https://nicholaswilde.io/homelab).

---

## :pushpin: TL;DR

- **Install dependencies:** `task deps`
- **Generate a new vault password:** `task init`
- **Edit secrets:** `task ve`
- **Edit role variables:** `ansible-vault edit roles/<role>/vars/main.yaml`
- **Update all hosts:** `ansible-playbook playbooks/update_all.yaml`
- **See all available tasks:** `task -l`

---

## :books: Documentation

For more detailed information, please see the [full documentation](https://nicholaswilde.io/homelab-playbooks).

## :framed_picture: Background

This repository contains Ansible playbooks used to configure and manage my homelab environment. The playbooks are designed to be idempotent and are used to set up and maintain various services and configurations across different types of machines, including Ubuntu servers, Raspberry Pis, Proxmox VE nodes, LXC containers, and Docker hosts.

## :balance_scale: License

[Apache License 2.0](https://github.com/nicholaswilde/homelab-playbooks/blob/main/LICENSE)

## :pencil: Author

This project was started in 2025 by [Nicholas Wilde](https://github.com/nicholaswilde/).