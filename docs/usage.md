# :pencil: Usage

The primary way to use this project is by running Ansible playbooks. The `Taskfile.yaml` provides a set of convenient tasks for common operations.

*   **Setup a single LXC container:**
    ```bash
    ansible-playbook playbooks/setup_lxcSingle.yaml
    ```

*   **Update all hosts:**
    ```bash
    ansible-playbook playbooks/update_all.yaml
    ```

*   **See all available tasks:**
    ```bash
    task -l
    ```

## :link: References
