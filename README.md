# Ansible Multi-Project Automation

This repository contains multiple Ansible automation projects organized by service or use-case.

## Projects

- `mariadb/`: Automates installation and configuration of MariaDB
- `apache/`: Configures Apache2 web server
- `others/`: Additional tasks and future projects

## Running a Playbook

Navigate to the desired subproject and run:

```bash
ansible-playbook projects/vars/db.yml --ask-vault-pass
