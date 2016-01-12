# Ansible Role: MySQL

[![Build Status](https://img.shields.io/travis/rwanyoike/ansible-role-mysql.svg)](https://travis-ci.org/rwanyoike/ansible-role-mysql) [![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/rwanyoike/ansible-role-mysql/master/LICENSE)

Installs and configures MySQL on RHEL/CentOS ~~or Debian/Ubuntu~~.

## Requirements

None

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
mysql_setup_server: true

# Set this to `yes` to forcibly update the root password.
mysql_root_password_update: no
mysql_root_username: root
mysql_root_password: hackme

mysql_cnf_use_template: true
mysql_cnf_bind_address: 0.0.0.0
mysql_cnf_port: 3306
mysql_cnf_datadir: /var/lib/mysql
mysql_cnf_socket: /var/lib/mysql/mysql.sock
mysql_cnf_mysqld_other: []

mysql_create_databases: []
mysql_create_users: []
```

## Dependencies

None

## Example Playbook

```yaml
- hosts: servers

  vars_files:
    - vars/main.yml

  roles:
    - role: rwanyoike.mysql
```

Inside `vars/main.yml`:

```yaml
mysql_root_password: super-secure-password

mysql_cnf_mysqld_other:
  - max_allowed_packet = 64M
  - max_connections = 151

mysql_create_databases:
  - name: example_db
    collation: latin1_general_ci
    encoding: latin1
mysql_create_users:
  - name: example_user
    host: "%"
    password: similarly-secure-password
    priv: "example_db.*:ALL"

# ... etc ...
```

## License

MIT

## Author Information

- This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
- This role was forked in 2015 by [Raymond Wanyoike](https://github.com/rwanyoike).
