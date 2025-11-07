# :pencil: Usage

The primary way to use this project is by running Ansible playbooks. The `Taskfile.yaml` provides a set of convenient tasks for common operations.

*   **See all available tasks:**
    ```bash
    task -l
    ```

## :gear: General Tasks

*   `task bootstrap`: Bootstrap the environment by installing dependencies.
*   `task deps`: Install Ansible roles and collections from `requirements.yaml`.
*   `task update-deps`: Update Ansible, ansible-lint, and Ansible roles and collections from `requirements.yaml`.
*   `task setup`: Setup a single LXC using the `playbooks/setup_single.yaml` playbook.
*   `task update`: Update a single LXC using the `playbooks/update_single.yaml` playbook.
*   `task task_all`: Run a single task on all hosts.
*   `task task_lxcAll`: Run a single task on all LXC containers.
*   `task task_rpis`: Run a single task on all Raspberry Pis.
*   `task replace-apt-proxy`: Replace the apt proxy URL on all hosts.

## :nas: OMV Tasks

*   `task omv-update`: Update the OpenMediaVault host.

## :arrow_down: Homelab-Pull Tasks

*   `task remove-homelab-pull`: Remove the homelab-pull service and timer from all hosts.

## :file_folder: Inventory Tasks

*   `task list`: List all inventory.
*   `task ping`: Ping all hosts in the inventory.
*   `task amd64-list`: List the amd64 Proxmox inventory.
*   `task arm64-list`: List the arm64 Proxmox inventory.
*   `task amd64-graph`: Graph the amd64 Proxmox inventory.
*   `task arm64-graph`: Graph the arm64 Proxmox inventory.

## :test_tube: Testing Tasks

*   `task amd64-test`: Test amd64 hosts.
*   `task arm64-test`: Test arm64 hosts.
*   `task rpis-test`: Test Raspberry Pi hosts.

## :key: Vault Tasks

*   `task init`: Generate a new `.vault_pass` file.
*   `task decrypt`: Decrypt the `.vault_pass.enc` file.
*   `task encrypt`: Encrypt the `.vault_pass` file.
*   `task ve`: Edit the Ansible vault.

## :books: Documentation Tasks

*   `task docs-deps`: Install documentation dependencies.
*   `task serve`: Start a local development server for the documentation.
*   `task docs-deploy`: Deploy the documentation to GitHub Pages.

## :robot: Gemini Tasks

*   `task gpro`: Run Gemini with the `gemini-2.5-pro` model.
*   `task gflash`: Run Gemini with the `gemini-2.5-flash` model.
*   `task glite`: Run Gemini with the `gemini-2.5-lite` model.
