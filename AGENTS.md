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
    ansible-playbook playbooks/setup_single.yaml
    ```

*   **Update all hosts:**
    ```bash
    ansible-playbook playbooks/update_all.yaml
    ```

*   **Update OMV host:**
    ```bash
    ansible-playbook playbooks/update_omv.yaml
    ```

*   **Remove homelab-pull:**
    ```bash
    ansible-playbook playbooks/remove_homelab_pull.yaml
    ```

*   **Replace dotfiles3 with dotfiles:**
    ```bash
    ansible-playbook playbooks/replace_dotfiles.yaml
    ```

*   **See all available tasks:**
    ```bash
    task -l
    ```

## Tasks

The `Taskfile.yaml` provides a set of convenient tasks for common operations. Here are some of the most common tasks:

*   `task deps`: Install dependencies.
*   `task setup`: Setup a single LXC container.
*   `task update`: Update a single LXC container.
*   `task omv-update`: Update the OMV host.
*   `task remove-homelab-pull`: Remove the homelab-pull service and timer.
*   `task task-chromeos`: Run the chromeos task on all hosts.
*   `task replace-dotfiles`: Replace the dotfiles3 repo with the dotfiles repo.
*   `task ve`: Edit the vault.
*   `task init`: Generate a new vault password.
*   `task encrypt`: Encrypt the vault password.
*   `task decrypt`: Decrypt the vault password.
*   `task list`: List all inventory.
*   `task ping`: Ping all hosts in inventory.

## Development Conventions

### Inventory

*   The inventory is located in the `inventory/` directory.
*   Hosts are grouped by operating system or function (e.g., `ubuntu`, `rpis`, `pve`, `lxcSingle`, `docker`).
*   Group variables are stored in `inventory/group_vars/`.
*   The `inventory/group_vars/all.yaml` file is encrypted with Ansible Vault and contains common variables for all hosts.

### Playbooks

*   Playbooks are located in the `playbooks/` directory.
*   Playbooks are named based on their function (e.g., `setup_single.yaml`, `update_all.yaml`).

### Host Targeting

When creating a playbook that should target all hosts, use the following `hosts` definition to ensure the correct machines are included while excluding specific ones:

```yaml
hosts:
  - rpis
  - proxmox_all_lxc:!mealie:!ntfy
```

This configuration targets all hosts in the `rpis` group and all hosts in the `proxmox_all_lxc` group, except for `mealie` and `ntfy`.

### Roles

*   Roles are located in the `roles/` directory.
*   Each role is self-contained and has a specific purpose. The main roles are:
    *   `setup`: Configures a new generic Linux instance.
    *   `update_apt`: Updates apt packages.
    *   `update_git`: Updates git repositories.
*   Role tasks are defined in `roles/<role>/tasks/main.yaml`.
*   Role variables are stored in `roles/<role>/defaults/main.yml` and are often encrypted with Ansible Vault.

### Vault

*   Ansible Vault is used to encrypt sensitive variables.
*   The vault password will be prompted when running playbooks.
*   The vault password can be provided via a file named `.vault_pass` in the project root. This file is encrypted using SOPS.
*   To create a new `.vault_pass` file, use the `task init` command:
    ```bash
    task init
    ```
*   To decrypt the `.vault_pass.enc` file, use the `task decrypt` command:
    ```bash
    task decrypt
    ```
*   To encrypt the `.vault_pass` file, use the `task encrypt` command:
    ```bash
    task encrypt
    ```
*   To edit the vault, use the following command:
    ```bash
    task ve
    ```
*   To edit the `.vault_pass` file, use the following command:
    ```bash
    sops .vault_pass
    ```

### Dynamic Proxmox Inventory

This project uses dynamic inventory for Proxmox VE. The inventory files `inventory/amd64.proxmox.yaml` and `inventory/arm64.proxmox.yaml` use the `community.proxmox.proxmox` plugin to connect to a Proxmox VE instance and retrieve information about LXC containers. This allows for dynamic discovery of hosts based on your Proxmox setup. The `ansible_host` variable is automatically set to the container's IP address.

**Note:** Do not modify the `ansible_user` variable in the Proxmox dynamic inventory files. The value is intentionally set to a literal string that is processed by the dynamic inventory script.

## Inventory Management

*   **List all inventory:**
    ```bash
    task list
    ```
*   **Ping all hosts in inventory:**
    ```bash
    task ping
    ```
*   **Test amd64 hosts:**
    ```bash
    task amd64-test
    ```
*   **Test arm64 hosts:**
    ```bash
    task arm64-test
    ```
*   **Test rpis hosts:**
    ```bash
    task rpis-test
    ```
*   **List amd64 Proxmox inventory:**
    ```bash
    task amd64-list
    ```
*   **List arm64 Proxmox inventory:**
    ```bash
    task arm64-list
    ```
*   **Graph amd64 Proxmox inventory:**
    ```bash
    task amd64-graph
    ```
*   **Graph arm64 Proxmox inventory:**
    ```bash
    task arm64-graph
    ```