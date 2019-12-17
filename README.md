# Ansible Role: phpfpm Exporter

[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![GitHub tag](https://img.shields.io/github/v/tag/umanit/ansible-prometheus_phpfpm_exporter)](https://github.com/umanit/ansible-prometheus_phpfpm_exporter/tags)

## Description

Deploy prometheus [Hipages php-fpm_exporter](https://github.com/hipages/php-fpm_exporter) using ansible.

Hipages php-fpm_exporter, isn't the exporter recommanded on [Prometheus export page](https://prometheus.io/docs/instrumenting/exporters/) but it offer multiple advantages : 
* mutliple fpm pool monitored
* ability to customize fpm status page URL

And so on...

## Notes

Role forked and largely inspired by [Cloudalchemy Node Exporter Ansible role](https://github.com/cloudalchemy/ansible-node-exporter)

Role is supposed to work with Debian, Suse, RedHat, Fedora, (See [Ansible Galaxy meta](/meta/main.yml)), but it was only tested on Ubuntu Bionic (18.04).

## Requirements

- Ansible >= 2.7 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `phpfpm_exporter_version` | 1.0.0 | Used to install phpfpm Exporter package. Also accepts latest as parameter. |
| `phpfpm_exporter_system_group` | "phpfpm-exp" | System group used to run phpfpm_exporter <br>(used to launch phpfpm_exporter binary in systemd service unit file)|
| `phpfpm_exporter_system_user` | "phpfpm-exp" | System user used to run phpfpm_exporter <br>(used to launch phpfpm_exporter binary in systemd service unit file)|
| `phpfpm_exporter_manage_system_user_group` | true | Whether or not this role must manage previously defined system user and group (example: if phpfpm_exporter run as www-data this don't need to manage the user, used to launch phpfpm_exporter binary in systemd service unit file) |
| `phpfpm_exporter_web_listen_address` | ":9253" | Address on which phpfpm exporter will listen (HTTP) <br>(used to launch phpfpm_exporter binary in systemd service unit file) |
| `phpfpm_exporter_web_telemetry_paths` | "" | URL to listen on for metrics. <br>(default "/metrics" in phpfpm_exporter if not provided, used to launch phpfpm_exporter binary in systemd service unit file) |
| `phpfpm_exporter_scrape_uri` | "" | Address of phpfpm status page, unix/socket style FastCGI address (e.g. unix:///var/run/php-fpm.sock;/status) or URI/TCP style (e.g. tcp://127.0.0.1:9000/status).<br>Multiple phpfpm pools listening on multiple socket/URI can be configured spearating them with coma (e.g. unix:///var/run/php-fpm-pool1.sock;/status,unix:///var/run/php-fpm-pool2.sock;/status) <br>(Used to launch phpfpm_exporter binary in systemd service unit file) |
| `phpfpm_exporter_fix_process_count` | false | See [Hipages php-fpm_exporter page](https://github.com/hipages/php-fpm_exporter#why---phpfpmfix-process-count) |
| `phpfpm_exporter_log_level` | error | Minimal log level to write [debug, info, warn, error, fatal] <br>(ie: Used to launch phpfpm_exporter binary in systemd service unit file) |
|


## Example

### Playbook

Use it in a playbook as follows:
```yaml
- hosts: all
  roles:
    - umanit.prometheus_phpfpm_exporter
```
## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
