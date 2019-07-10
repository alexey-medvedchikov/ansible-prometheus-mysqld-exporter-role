# Ansible Role: prometheus-mysqld-exporter

An Ansible role that installs Prometheus MySQL Exporter on Ubuntu|Debian|Redhat-based machines with systemd|Upstart|sysvinit.

## Requirements

All needed packages will be installed with this role.

## Role Variables

| Variable                                | Type   | Choices                           | Default                                                              | Comment                                                                       |
|-----------------------------------------|--------|-----------------------------------|----------------------------------------------------------------------|-------------------------------------------------------------------------------|
| prometheus_mysqld_exporter_version      | string | See [mysqld_exporter][1] releases | v0.12.0                                                              | Version of mysqld_exporter that will be installed.                            |
| prometheus_mysqld_exporter_release_name | string |                                   | mysqld_exporter-{{ prometheus_mysqld_exporter_version }}.linux-amd64 | Name of the binary that will be download from the [releases][1]) page         |
| prometheus_mysqld_exporter_config_flags | dict   |                                   | {}                                                                   | Dict of flag, flag-value options to start exporter with                       |
| prometheus_mysqld_exporter_collectors   | dict   |                                   | {}                                                                   | Dict of flag, flag-value (ignored, leave blank) to control enabled collectors |
| prometheus_mysqld_exporter_mycnf        | string |                                   |                                                                      | Contents of MySQL client credentials file                                     |
| prometheus_mysqld_exporter_mycnf_path   | string |                                   | /etc/mysqld_exporter/my.cnf                                          | Path to store MySQL client credentials                                        |

## Dependencies

- UnderGreen.prometheus-exporters-common

## Example Playbook

```yaml
- hosts: mysqld-exporters
  roles:
    - role: alexey-medvedchikov.prometheus-mysqld-exporter
      prometheus_mysqld_exporter_version: 0.11.0
      prometheus_mysqld_exporter_config_flags:
        'web.listen-address': '9104'
      prometheus_mysqld_exporter_mycnf: |
        [client]
        user = myusername
        password = 1qa2ws3ed
      prometheus_mysqld_exporter_collectors:
        collect.perf_schema.eventsstatements:
        collect.perf_schema.eventsstatementssum:
```

## License

GPLv2

[1]: https://github.com/prometheus/mysqld_exporter/releases
