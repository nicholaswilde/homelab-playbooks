# :rocket: Getting Started

## :key: Password File

A password file is used by ansible vault to encrypt passwords.

### Generate a new password

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

To decrypt the `.vault_pass.enc` file, use the `task decrypt` command:

```bash
task decrypt
```

To encrypt the `.vault_pass` file, use the `task encrypt` command:

```bash
task encrypt
```

## :mag: &nbsp; Dynamic Proxmox Inventory

This project uses dynamic inventory for Proxmox VE. The inventory files `inventory/amd64.proxmox.yaml` and `inventor
y/arm64.proxmox.yaml` use the `community.proxmox.proxmox` plugin to connect to a Proxmox VE instance and retrieve in
formation about LXC containers. This allows for dynamic discovery of hosts based on your Proxmox setup. The `ansible
_host` variable is automatically set to the container's IP address.

## :link: References
