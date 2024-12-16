<!-- markdownlint-disable-next-line no-trailing-punctuation -->
# :house_with_garden: homelab-playbooks :rocket:

[![task](https://img.shields.io/badge/task-enabled-brightgreen?logo=task&logoColor=white&style=for-the-badge)](https://taskfile.dev/)

An ansible playbook for my homelab

---

## :hammer_and_wrench: &nbsp; Usage

```shell
ansible-playbook playbooks/setup_lxc.yaml
Vault password:
```
---

## :gear: &nbsp; Variables

Variables are stored in `roles/<role>/vars/main.yaml` which is encrypted using [ansible-vault][2].

The vault password is prompted during run.

```yaml
# roles/<role>/vars/main.yaml
---
lxc_user: foo
ansible_user: bar
ansible_password: baz
```

---

<!-- spellchecker-disable -->
## :balance_scale: &nbsp; License
<!-- spellchecker-enable -->

​[​Apache 2.0 License​](../LICENSE)

---

## :pencil:​&nbsp;​Author

​This project was started in 2024 by [Nicholas Wilde][1].

[1]: <https://github.com/nicholaswilde/>
[2]: <https://docs.ansible.com/ansible/latest/vault_guide/vault.html>
