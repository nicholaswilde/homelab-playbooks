# :test_tube: Testing

This project includes several tasks for testing the Ansible playbooks against different architectures.

## :computer: AMD64

To test the playbooks on amd64 hosts, run the following command:

```bash
task amd64-test
```

This task will run the `ansible.builtin.apt` module with `update_cache=true` on all hosts in the `inventory/amd64.proxmox.yaml` inventory.

## :fontawesome-solid-phone: ARM64

To test the playbooks on arm64 hosts, run the following command:

```bash
task arm64-test
```

This task will run the `ansible.builtin.apt` module with `update_cache=true` on all hosts in the `inventory/arm64.proxmox.yaml` inventory.

## :fontawesome-brands-raspberry-pi: Raspberry Pi

To test the playbooks on Raspberry Pi hosts, run the following command:

```bash
task rpis-test
```

This task will run the `ansible.builtin.apt` module with `update_cache=true` on all hosts in the `inventory/rpis.yaml` inventory.

## :whale: Dockerized Testing Environment

This project includes a Dockerized testing environment in the `test/` subdirectory, which allows you to test Ansible playbooks in an isolated Ubuntu container.

### :gear: Configuration

-   **`test/Dockerfile`**: Defines the Docker image used for testing. It sets up an Ubuntu container with SSH access.
-   **`test/machine-setup.yml`**: The Ansible playbook that will be run inside the test container. You can modify this file to test your own playbooks and roles.

### :hammer_and_wrench: Usage

To run the Dockerized test, navigate to the `test/` directory and use the `task run` command:

```bash
cd test/
task run
```

This will execute the `setup-container.sh` script, which automates the entire testing process:

1.  **Creates a temporary directory.**
2.  **Generates a temporary SSH key.**
3.  **Builds and starts a Docker container.**
4.  **Creates a temporary Ansible inventory file.**
5.  **Runs the `machine-setup.yml` playbook inside the container.**
6.  **Cleans up the container and temporary files.**

