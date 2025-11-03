# :key: Secrets

Secret variables are encrypted using [Ansible Vault][1] as a string or the entire file is encrypted. My preference is to encrypt files or strings using a vault password file.

## :gear: Config

Set the `vault_password_file` variable in the `ansible.cfg` so you don't need to specify the file, `--vault-password-file`, with every command.

!!! abstract "ansible.cfg"

    ```ini
    [defaults]
    vault_password_file = ./.vault_pass
    ```

## :lock: Vault Password File

To create a new vault password file, use the `task init` command:

!!! warning

    Ensure that you're not overwriting an existing password!

=== "Task"

    ```shell
    task init
    ```

=== "Manual"

    ```shell
    openssl rand -hex 64 > .vault_pass
    chmod 600 .vault_pass
    ```

!!! tip

    It is recommended save the password elsewhere as a backup. 

This will create a `.vault_pass` file in the root directory. This file should be kept secret and is used to encrypt/decrypt sensitive variables. The `.vault_pass` file is encrypted using [SOPS][2].

To encrypt the `.vault_pass` file for later use:

=== "Task"

    ```bash
    task encrypt
    ```

=== "Manual"

    ```bash
    sops -e .vault_pass > .vault_pass.enc
    ```

To decrypt the `.vault_pass.enc` file:

=== "Task"

    ```bash
    task decrypt
    ```

=== "Manual"

    ```bash
    sops -d .vault_pass.enc > .vault_pass
    chmod 600 .vault_pass
    ```
    
## :thread: String

Encrypt a secret variable as a string to use in a playbook.

=== "Manual"

    ```bash
    ansible-vault encrypt_string "long-token-secret" --name "token_secret"
    ```

Copy the output to a playbook to use the variable.

!!! success "Output"

    ```yaml
    --8<-- "inventory/amd64.proxmox.yaml:token_secret"
    ```
    
## :file_folder: File

Encrypt the secrets file using Ansible Vault.

=== "Manual"

    ```bash
    ansible-vault encrypt "./inventory/group_vars/all.yaml"
    ```

Edit the secrets file.

=== "Task"

    ```bash
    task ve
    ```

=== "Manual"

    ```bash
    ansible-vault edit "./inventory/group_vars/all.yaml"
    ```

## :link: References

- <https://docs.ansible.com/ansible/latest/vault_guide/index.html>

[1]: <https://docs.ansible.com/ansible/latest/vault_guide/index.html>
[2]: <https://getsops.io/>
