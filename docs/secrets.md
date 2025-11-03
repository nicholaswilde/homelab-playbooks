# :key: Secrets

Secret variables are encrypted using Ansible Vault as a string or the entire file is encrypted.

## Config

WIP

## String

=== "Manual"

    ```bash
    ansible-vault encrypt_string "long-token-secret" --name "token_secret"
    ```

## File

=== "Manual"

    ```bash
    ansible-vault encrypt "./inventory/group_vars/all.yaml"
    ```
