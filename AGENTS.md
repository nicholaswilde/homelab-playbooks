# GEMINI.md

## Project Overview

This project contains Ansible playbooks for configuring and managing a homelab environment. The playbooks are designed to be idempotent and are used to set up and maintain various services and configurations across different types of machines, including Ubuntu servers, Raspberry Pis, Proxmox VE nodes, LXC containers, and Docker hosts.

The project uses Ansible Vault to encrypt sensitive variables, and the inventory is organized into groups of hosts.

## Building and Running

The primary way to use this project is by running Ansible playbooks. The `Taskfile.yaml` provides a set of convenient tasks for common operations.

### Prerequisites

*   Ansible
*   Python

### Installation

1.  Install dependencies:
    ```bash
    task deps
    ```

### Running Playbooks

*   **Setup a single LXC container:**
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

## Development Conventions

### Inventory

*   The inventory is located in the `inventory/` directory.
*   Hosts are grouped by operating system or function (e.g., `ubuntu`, `rpis`, `pve`, `lxcSingle`, `docker`).
*   Group variables are stored in `inventory/group_vars/`.
*   The `inventory/group_vars/all.yaml` file is encrypted with Ansible Vault and contains common variables for all hosts.

### Playbooks

*   Playbooks are located in the `playbooks/` directory.
*   Playbooks are named based on their function (e.g., `setup_lxcSingle.yaml`, `update_all.yaml`).

### Roles

*   Roles are located in the `roles/` directory.
*   Each role is self-contained and has a specific purpose (e.g., `setup`, `update_apt`, `update_git`).
*   Role tasks are defined in `roles/<role>/tasks/main.yaml`.
*   Role variables are stored in `roles/<role>/vars/main.yaml` and are often encrypted with Ansible Vault.

### Vault

*   Ansible Vault is used to encrypt sensitive variables.
*   The vault password will be prompted when running playbooks.
*   To edit the vault, use the following command:
    ```bash
    task ve
    ```
