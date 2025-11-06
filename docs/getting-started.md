# :rocket: Getting Started

## :package: Install dependencies

This project uses [Task](https://taskfile.dev/) to manage dependencies. To install all the necessary dependencies, run the following command:

=== "Task"

    ```bash
    task deps
    ```

=== "Manual"

    ```bash
    sudo apt install -y pipx
    pipx install --include-deps ansible
    ansible-galaxy role install -r requirements.yaml
    ansible-galaxy collection install -r requirements.yaml
    ```

This command will:

- Install `pipx` and ensure its paths are configured.
- Upgrade all `pipx` managed packages.
- Install Ansible roles from `requirements.yaml`.
- Install Ansible collections from `requirements.yaml`.

## :key: Generate a new password

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

## :closed_lock_with_key: Edit secrets

To edit the secrets file, use the following command:

=== "Task"

    ```bash
    task ve
    ```

=== "Manual"

    ```bash
    ansible-vault edit ./inventory/group_vars/all.yaml
    ```

This will open the `inventory/group_vars/all.yaml` file in your default editor. This file is encrypted with Ansible Vault.

For more information on managing secrets, see the [Secrets](./secrets.md) guide.
