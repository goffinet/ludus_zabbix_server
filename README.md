# Ansible Role: {{ Thing }} ([Ludus](https://ludus.cloud))

An Ansible Role that installs [Zabbix Server, Database and Frontend](https://www.zabbix.com/download?zabbix=7.0&os_distribution=debian&os_version=12&components=server_frontend_agent&db=mysql&ws=apache) on Debian 12.

> [!WARNING]
> This role supports only Debian 12 (Bookworm).
>
> Only HTTP supported

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    ludus_mysql_root_password: "secure_root_password"
    ludus_mysql_zabbix_database: "zabbix"
    ludus_mysql_zabbix_user: "zabbix"
    ludus_mysql_zabbix_password: "secure_zabbix_password"
    ludus_zabbix_version: "7.0"

## Dependencies

None.

## Example Playbook

```yaml
- hosts: localhost
  roles:
    - ludus_zabbix_server
  vars:
    ludus_mysql_root_password: "secure_root_password"
    ludus_mysql_zabbix_database: "zabbix"
    ludus_mysql_zabbix_user: "zabbix"
    ludus_mysql_zabbix_password: "secure_zabbix_password"
    ludus_zabbix_version: "7.0"
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-zabbix"
    hostname: "{{ range_id }}-zabbix"
    template: debian-12-x64-server-template
    vlan: 10
    ip_last_octet: 1
    ram_gb: 8
    cpus: 4
    linux: true
    testing:
      snapshot: false
      block_internet: false
    roles:
      - goffinet.ludus_zabbix_server
    role_vars:
      ludus_mysql_zabbix_password: "secure_zabbix_password_test"
```


## Author Information

This role was created by [goffinet](https://github.com/goffinet), for [Ludus](https://ludus.cloud/).
