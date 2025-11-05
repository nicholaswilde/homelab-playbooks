# :rocket: Getting Started

## :package: Install dependencies

This project uses [Task](https://taskfile.dev/) to manage dependencies. To install all the necessary dependencies, run the following command:

```bash
task deps
```

This command will:

- Install `pipx` and ensure its paths are configured.
- Upgrade all `pipx` managed packages.
- Install Ansible roles from `requirements.yaml`.
- Install Ansible collections from `requirements.yaml`.

## :key: Generate a new password

To create a new vault password file, use the `task init` command:

```bash
task init
```

This will create a `.vault_pass` file in the root directory. This file should be kept secret and is used to encrypt/decrypt sensitive variables. The `.vault_pass` file is encrypted using SOPS.

## :closed_lock_with_key: Edit secrets

To edit the secrets file, use the following command:

```bash
task ve
```

This will open the `inventory/group_vars/all.yaml` file in your default editor. This file is encrypted with Ansible Vault.

For more information on managing secrets, see the [Secrets](./secrets.md) guide.
