# :gear: Configuration

## :mag: Dynamic Proxmox Inventory

This project uses dynamic inventory for Proxmox VE. The inventory files `inventory/amd64.proxmox.yaml` and `inventory/arm64.proxmox.yaml` use the `community.proxmox.proxmox` plugin to connect to a Proxmox VE instance and retrieve information about LXC containers. This allows for dynamic discovery of hosts based on your Proxmox setup.

### :wrench: Options

The following options can be configured in `inventory/amd64.proxmox.yaml` and `inventory/arm64.proxmox.yaml`:

- `plugin`: The Ansible plugin to use. This should be set to `community.proxmox.proxmox`.
- `url`: The URL of your Proxmox VE instance.
- `validate_certs`: Whether to validate the SSL certificate of the Proxmox server. Defaults to `false`.
- `want_facts`: Whether to retrieve facts about the Proxmox nodes. Defaults to `true`.
- `user`: The Proxmox user to connect with.
- `token_id`: The ID of the Proxmox API token.
- `token_secret`: The secret of the Proxmox API token. This should be encrypted with Ansible Vault, see the [Secrets](./secrets.md) guide.

### :computer: Example

```yaml
---
plugin: community.proxmox.proxmox
url: https://pve01.l.nicholaswilde.io
validate_certs: false
want_facts: true

# Proxmox credentials. Create a token on the Proxmox node.
user: root@pam
token_id: ansible

# password file .vault_pass
token_secret: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          63356539313533663964636139333037386262616239373638333136643834303631653139633437
          6562613738653338613134343635383639363237343833390a353364373034383664343661316339
          64333066646635396134323334336164633965373830666665353431326338363131386530383631
          3939643133346134300a393136636137326431303965353537386665323766313464666331333337
          62326331663361376632393331396439383666333739323766316432393761666561356266643938
          3165353364633639326632336539313466343531363431373465

compose:
  ansible_host: proxmox_agent_interfaces[1]['ip-addresses'][0] | default(proxmox_net0.ip) | ansible.utils.ipaddr('address')
  ansible_user: "'root'"
```

!!! warning "`ansible_user` Quoting"

    The `ansible_user` value needs to be in single quotes inside of double quotes (e.g., `"'root'"`). This specific quoting is necessary due to the multi-layered parsing involved:

    1.  **YAML Parsing:** The outer double quotes (`"..."`) instruct the YAML parser to treat the entire content (`'root'`) as a single string.
    2.  **Jinja2 Evaluation:** Ansible's `compose` feature then evaluates this string using the Jinja2 templating engine. The inner single quotes (`'...'`) ensure that the final output of this Jinja2 evaluation is a literal string `'root'`, which is what the underlying system expects for the `ansible_user` variable.

The `ansible_user` variable in the `compose` section sets the default SSH user for all discovered Proxmox LXC containers. In the example above, it is set to `'root'` for all containers.

### :pencil: Overriding `ansible_user` for Individual Hosts

If you need to set a different `ansible_user` for a specific Proxmox host or a subset of hosts, you can do so by creating a static inventory file. This allows you to override the dynamic inventory's `ansible_user` setting for those particular hosts.

For example, you can create a file like `inventory/static_arm64.yaml` (as shown below) to define specific connection parameters for an individual ARM64 host:

```yaml
---
all:
  hosts:
    arm64:
      ansible_host: <IP_ADDRESS_OF_ARM64>
      ansible_user: <YOUR_USERNAME>
      ansible_private_key_file: /home/nicholas/.ssh/id_ed25519 # Assuming this is the key you want to use
```

By including this static inventory file when running your Ansible playbooks, the `ansible_user` specified in `inventory/static_arm64.yaml` will take precedence for the `arm64` host, while other dynamically discovered hosts will continue to use the `ansible_user` defined in the Proxmox dynamic inventory configuration.

## :gear: Role Configuration Variables

Variables for individual roles are stored in the `roles/<role name>/defaults/main.yaml`

!!! example

    ```yaml
    --8<-- "roles/linux_generic/defaults/main.yaml"
    ```

## :gear: Ansible Configuration File

The `ansible.cfg` file contains default settings for Ansible. Here are the key configurations used in this project:

```ini
[defaults]
inventory = ./inventory/
playbook = ./playbooks/update_all.yaml 
timeout = 25
vault_password_file = ./.vault_pass
interpreter_python = auto_silent
roles_path = ./roles/
host_key_checking = False
private_key_file = /home/nicholas/.ssh/id_ed25519

[ssh_connection]
scp_if_ssh = True
```

### :pencil: Explanation of Key Settings

-   `inventory`: Specifies the default inventory directory.
-   `playbook`: Sets a default playbook to run if none is specified (e.g., `update_lxc.yaml`).
-   `timeout`: Sets the default SSH connection timeout to 25 seconds.
-   `vault_password_file`: Points to the `.vault_pass` file for Ansible Vault passwords.
-   `interpreter_python`: Automatically detects the Python interpreter on remote hosts.
-   `roles_path`: Specifies the directory where Ansible roles are located.
-   `host_key_checking`: Disables host key checking for SSH connections (use with caution in production environments).
-   `private_key_file`: Specifies the default private key file for SSH connections.
-   `scp_if_ssh`: Forces Ansible to use `scp` for file transfers over SSH, even if `sftp` is available.
```
