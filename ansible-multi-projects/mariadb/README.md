 MariaDB Authentication Strategy

This project uses **MariaDB root access** for creating databases and users via Ansible.

Default Authentication (Unix Socket)

By default, the playbook uses the `login_unix_socket` method because most MariaDB installations on CentOS/RHEL-based systems configure the `root` user to authenticate via **Unix socket** without a password:

```yaml
login_user: root
login_unix_socket: /var/lib/mysql/mysql.sock
```

This allows secure, local root access **without a password**, avoiding the need to store credentials in playbooks or vaults.

---

Alternative: Password-Based Authentication

If your MariaDB server is configured to use `mysql_native_password` or another method requiring a password, you should:

* Create a `.my.cnf` file containing root credentials.
* Copy it to the remote nodes using the provided playbook below.
Example `.my.cnf` file

```ini
[client]
user=root
password=your_root_password
```

Ensure it's saved at `/root/.my.cnf` on your control node.

---

Playbook: `copy-mycnf.yml`

Use this playbook to distribute the `.my.cnf` file to your remote hosts:

```yaml
---
- name: Copy MySQL root credentials file to remote hosts
  hosts: all
  become: true
  tasks:
    - name: Copy .my.cnf for root authentication
      copy:
        src: /root/.my.cnf
        dest: /root/.my.cnf
        owner: root
        group: root
        mode: '0600'
```
