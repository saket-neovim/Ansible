# Ansible Playbooks

This repository contains learning and lab playbooks that cover common Ansible tasks (users, packages, services, files, sudoers, handlers, fetch/archive, and basic inventories). The playbooks are designed to be simple and readable for practice.

## Quick Start

Run a playbook:
```bash
ansible-playbook -i inventory/inventory.ini playbook.yml
```

Ping all hosts:
```bash
ansible-playbook -i inventory/inventory.ini playbook2.yml
```

## Playbook Index

- `playbook.yml` — Hello world example + file write
- `playbook2.yml` — Ping + copy a local file to remote hosts
- `playbook3.yml` — User creation
- `playbook4.yml` — Install and start Apache (cross‑distro)
- `playbook5.yml` — Install multiple packages
- `playbook6.yml` — Multi‑play example: users, copy file, conditionals
- `playbook7.yml` — Set hostname dynamically
- `playbook_handler1.yml` — Handler example
- `systemd.yml` — Manage services safely with facts
- `CommandModule.yml` — Command module usage (idempotent patterns)
- `fileModule.yml` — File module examples
- `fileManagement.yml` — Copy + checksum comparison + handler
- `fetchModule.yml` — Fetch files from remote hosts
- `package.yml` — Package management on RHEL/Debian
- `playbookArchive.yml` — Archive, fetch, copy, cleanup flow
- `CreatingUserwithPasswdlessSudo.yml` — Create user + sudoers
- `ApplyingSudoersToMultipleUsers.yml` — Multiple sudoers entries
- `RevokeSudoAccess.yml` — Remove sudo access
- `SudoersRuleUsingj2.yml` — Sudoers via template
- `templateModule.yml` — Template example
- `sshAccess.yml` — Create user + authorized keys

## Inventories

- `inventory/` — example inventories (all redacted and safe to share)
- `inventory_test.ini` — sample multi‑group inventory
- `RHEL/inventory.ini` — example RHEL inventory

## Notes on Safety

- All secrets and private keys have been replaced with placeholders like `<REDACTED_PASSWORD>`.
- Avoid committing real `ansible_password`, `ansible_become_password`, or private key paths.
- Use Ansible Vault for sensitive values.

## Tips

- Use `--check` for dry‑runs:
```bash
ansible-playbook -i inventory/inventory.ini playbook4.yml --check
```
