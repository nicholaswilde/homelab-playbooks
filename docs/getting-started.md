# :rocket: Getting Started

## :package: Install dependencies

=== "Task"

    ```bash
    task deps
    ```
    
## Generate a new password

To create a new vault password file, use the `task init` command:

=== "Task"

    ```bash
    task init
    ```

=== "Manual"

    ```bash
    openssl rand -hex 64 > .vault_pass
    chmod 600 .vault_pass
    ```

This will create a `.vault_pass` file in the root directory. This file should be kept secret and is used to encrypt/decrypt sensitive variables. The `.vault_pass` file is encrypted using SOPS.

## Edit secrets

=== "Task"

    ```bash
    task ve
    ```

=== "Manual"

    ```bash
    ansible-vault edit "./inventory/group_vars/all.yaml"
    ```

!!! example "./inventory/group_vars/all.yaml"

    ```yaml
    ---
    ansible_password: foo
    ansible_become_password: bar
    ...
    ```

## :mag: Dynamic Proxmox Inventory

This project uses dynamic inventory for Proxmox VE. The inventory files `inventory/amd64.proxmox.yaml` and `inventor
y/arm64.proxmox.yaml` use the [`community.proxmox.proxmox`][1] plugin to connect to a Proxmox VE instance and retrieve in
formation about LXC containers. This allows for dynamic discovery of hosts based on your Proxmox setup. The `ansible
_host` variable is automatically set to the container's IP address.

Set the variables for the dynamic Proxmox inventory. See [configuration](./configuration.md).

??? abstract "inventory/amd64.proxmox.yaml"

    ```yaml
    --8<-- "inventory/amd64.proxmox.yaml"
    ```

??? abstract "inventory/arm64.proxmox.yaml"

    ```yaml
    --8<-- "inventory/arm64.proxmox.yaml"
    ```
    
## :link: References

[1]: <https://docs.ansible.com/ansible/latest/collections/community/proxmox/proxmox_inventory.html>
