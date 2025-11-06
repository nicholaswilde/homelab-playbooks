# :stethoscope: Troubleshooting

## :warning: SSH Connection Issues

If you are experiencing issues connecting to your hosts via SSH, your `~/.ssh/config` file might be causing problems.

Ansible uses the SSH client to connect to remote hosts. If your `~/.ssh/config` file contains incorrect configurations, such as wrong hostnames, invalid identities, or conflicting options, it can prevent Ansible from establishing a successful SSH connection.

### :mag: Diagnosis

To diagnose SSH connection issues, you can try the following:

1.  **Test SSH connection manually:**

    ```bash
    ssh -vvv your_host_alias
    ```

    The `-vvv` option provides verbose output, which can help identify where the connection is failing.

2.  **Check `~/.ssh/config` for conflicts:**

    Review your `~/.ssh/config` file for any entries that might be overriding Ansible's connection parameters or causing unexpected behavior. Pay close attention to `Host`, `Hostname`, `User`, `IdentityFile`, and `ProxyCommand` directives.

3.  **Temporarily disable `~/.ssh/config`:**

    You can temporarily bypass your `~/.ssh/config` file by using the `-F /dev/null` option with the `ssh` command:

    ```bash
    ssh -F /dev/null -vvv user@your_host_ip
    ```

    If the connection works without the `config` file, the issue is definitely within your `~/.ssh/config`.

### :wrench: Resolution

-   **Correct or remove conflicting entries:** Edit your `~/.ssh/config` file to fix any incorrect configurations or remove entries that are no longer needed.
-   **Specify connection parameters in Ansible:** You can explicitly define SSH connection parameters in your Ansible inventory or playbook to override any problematic settings in `~/.ssh/config`.

    Example in inventory:

    ```ini
    [your_group]
    your_host_alias ansible_host=your_host_ip ansible_user=your_user ansible_ssh_private_key_file=/path/to/your/key
    ```

## :bug: Debugging Ansible Variables

When troubleshooting Ansible playbooks, it's often helpful to inspect the values of variables that Ansible is using. The `task list` command can be used to display all inventory variables, which can help you verify if your variables are being set as expected.

To list all inventory variables, run the following command:

=== "Task"

    ```bash
    task list
    ```

=== "Manaul"

    ```bash
    ansible-inventory -i ./inventory/ --vars --list -y
    ```

This command will output a detailed YAML representation of your entire inventory, including all host and group variables, which can be invaluable for debugging.

## :link: References
