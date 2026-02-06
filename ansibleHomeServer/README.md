# Ansible Home Server

This folder contains a collection of Ansible labs, practice exams, and roles for home‑server automation. It includes custom playbooks and a few vendored roles/collections for learning.

## Structure

- `AnsibleHomeServerTesting/` — main lab area
  - playbooks like `Lab5.yml`, `lab12.yml`, `timesync.yml`, etc.
  - `roles/` — custom and third‑party roles
  - `PracticeExam/` — practice exam playbooks/roles

## Running Playbooks

Example:
```bash
ansible-playbook -i ansibleHomeServer/AnsibleHomeServerTesting/inventory \
  ansibleHomeServer/AnsibleHomeServerTesting/Lab5.yml
```