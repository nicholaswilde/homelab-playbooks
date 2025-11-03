# :key: Secrets

Secret variables are encrypted using Ansible Vault as a string or the entire file is encrypted.

## Config

Set the `vault_password_file` variable in the `ansible.cfg` so you don't need to specify the file with every command.

!!! abstract "ansible.cfg"

    ```ini
    [defaults]
    vault_password_file = ./.vault_pass
    ```

## :thread: String

Encrypt a secret variable as a string.

=== "Manual"

    ```bash
    ansible-vault encrypt_string "long-token-secret" --name "token_secret"
    ```

!!! success "Output"

    ```yaml
    token_secret: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          63356539313533663964636139333037386262616239373638333136643834303631653139633437
          6562613738653338613134343635383639363237343833390a353364373034383664343661316339
          64333066646635396134323334336164633965373830666665353431326338363131386530383631
          3939643133346134300a393136636137326431303965353537386665323766313464666331333337
          62326331663361376632393331396439383666333739323766316432393761666561356266643938
          3165353364633639326632336539313466343531363431373465
    ```
    
## :file_folder: File

Encrypt the secrets file.

=== "Manual"

    ```bash
    ansible-vault encrypt "./inventory/group_vars/all.yaml"
    ```

Edit the secrets file.

=== "Manual"

    ```bash
    ansible-vault edit "./inventory/group_vars/all.yaml"
    ```
