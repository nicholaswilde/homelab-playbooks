# :repeat: Workflows

This document outlines the common workflows for testing and setting up new hosts in this project.

## :test_tube: Testing Workflow

This workflow describes the process for testing a new Ansible task before deploying it to all hosts.

1.  **Add a Test Host:**

    Add the IP address of your test host to the `inventory/single.yaml` file under the `hosts` section.

    ```yaml
    --- 
    single:
      vars:
        ansible_user: root
      hosts:
        test:
          ansible_host: <YOUR_TEST_HOST_IP>
    ```

2.  **Create a Test Task:**

    Create your test task in the `playbooks/test.yaml` file. This playbook is configured to run on the `single` host group.

3.  **Run the Test Playbook:**

    Execute the test playbook to apply the task to your test host:

    ```bash
    ansible-playbook playbooks/test.yaml
    ```

4.  **Deploy to All Hosts:**

    Once you have verified that the task works as expected, you can deploy it to all other hosts using one of the following playbooks:

    -   `playbooks/task_all.yaml`: Deploys the task to all LXC containers and Raspberry Pis.
    -   `playbooks/task_lxcAll.yaml`: Deploys the task to all LXC containers.

5.  **Incorporate into `linux_instance_generic` Role:**

    After successful deployment, incorporate the new task into the `roles/linux_instance_generic` role. This ensures that the task is included in the setup process for new single hosts.

## :rocket: Setting up a Single Host

This workflow describes how to set up a new single host using the `linux_instance_generic` role. This role is designed to apply a generic Linux configuration to a new host.

1.  **Add the Host to Inventory:**

    Add the new host to your Ansible inventory. You can either add it to an existing inventory file or create a new one.

    I prefer to add it to my `inventory`

2.  **Create a Playbook:**

    Create a new playbook that targets the new host and includes the `linux_instance_generic` role.

    ```yaml
    --- 
    - name: Setup a new single host
      hosts: <your_new_host>
      become: true

      roles:
        - role: linux_instance_generic
    ```

3.  **Run the Playbook:**

    Execute the playbook to configure the new host:

    ```bash
    ansible-playbook playbooks/setup_single.yaml
    ```
