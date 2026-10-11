# Ansible Playbooks for Linux Administration

Linux automation practice covering users and sudoers, packages and services, files and templates, handlers, inventories, and role structure. The repository also retains course/exam exercises and bundled third-party Ansible content for learning context.

**Status:** a collection of lab playbooks, not a tested production configuration-management system. Some exercises expect course infrastructure, local input files, or installed collections.

## Relationship to the other repository

At this cleanup's baseline, this repository and [ansibleHomeServer](https://github.com/saket-neovim/ansibleHomeServer) had identical commits and tracked file trees. Both are retained; neither is presented as a separate implementation. They may diverge later.

## Repository guide

| Area | Examples |
| --- | --- |
| Users and privileges | `playbook3.yml`, `CreatingUserwithPasswdlessSudo.yml`, `RevokeSudoAccess.yml`, `deploy_sudoers.j2` |
| Packages and services | `playbook4.yml`, `package.yml`, `systemd.yml` |
| Files and templates | `fileManagement.yml`, `fetchModule.yml`, `templateModule.yml` |
| Handlers and archives | `playbook_handler1.yml`, `playbookArchive.yml` |
| SSH access | [sshAccess.yml](sshAccess.yml), using your local public key rather than a committed identity |
| Inventory examples | [inventory/](inventory/), [inventory_test.ini](inventory_test.ini) |
| Custom roles | `my_role/`, `test_role_1/`, `test_role_2/` |
| Additional exercises | [ansibleHomeServer/AnsibleHomeServerTesting/](ansibleHomeServer/AnsibleHomeServerTesting/) |

`dynamic_inventory.py` is currently empty; it does not implement dynamic inventory. Vendored collections and external roles retain their upstream code, documentation, and licenses. Credit for those implementations belongs to their authors.

## Prerequisites and safe inspection

Install a compatible Ansible controller with Python and the collections required by the chosen playbook. Linux target hosts need SSH access, Python, and appropriate privilege escalation. Read `ansible.cfg` and the selected playbook before execution; the root config disables SSH host-key checking for lab convenience.

The committed inventory uses documentation addresses or localhost. Copy an example into ignored `inventory.local/` and set your own hosts and SSH identity there.

```bash
mkdir -p inventory.local
cp inventory/inventory.ini inventory.local/hosts.ini
# Edit inventory.local/hosts.ini for disposable hosts you own.
ansible-inventory -i inventory.local/hosts.ini --graph
ansible-playbook -i inventory.local/hosts.ini playbook4.yml --syntax-check
ansible-playbook -i inventory.local/hosts.ini playbook4.yml --check --diff --ask-become-pass
```

The last command connects to real hosts; check mode is a preview whose support depends on each task/module. Review before running it. For password-based SSH, prompt with `--ask-pass` rather than saving a password in inventory. Use Ansible Vault for sensitive variable files.

`sshAccess.yml` reads `~/.ssh/id_ed25519.pub` on the controller; create or choose your own public key before using it. Several classroom labs reference private input files or classroom hostnames that are intentionally not provided as working public infrastructure.

## Validation and operational tradeoffs

Syntax checks verify playbook structure, not permissions, idempotency, package availability, or successful host changes. A useful lab record compares the first and second run, identifies tasks reporting changes, and checks the resulting service/file/user state. Do not assume every practice playbook is idempotent.

Read tasks that modify sudoers, user access, packages, or services before using privilege escalation. Test in disposable VMs/containers, track changes, and remove or rebuild those environments after the exercise.

## Security and attribution

Keep real inventory, passwords, private keys, and raw host output local. Current placeholder cleanup does not establish that older commits are safe; see [security notes](SECURITY.md). Bundled collection documentation and integration-test fixtures can produce secret-scanner findings and need contextual review. No broad scanner exclusions are applied.
