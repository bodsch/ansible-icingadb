
# Ansible Role:  `icingadb`

This role will fully configure and install [dockerd](https://www.docker.com/).

[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/bodsch/ansible-icinga2/CI)][ci]
[![GitHub issues](https://img.shields.io/github/issues/bodsch/ansible-icingadb)][issues]
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/bodsch/ansible-icingadb)][releases]

[ci]: https://github.com/bodsch/ansible-icingadb/actions
[issues]: https://github.com/bodsch/ansible-icingadb/issues?q=is%3Aopen+is%3Aissue
[releases]: https://github.com/bodsch/ansible-icingadb/releases



## Requirements & Dependencies

- redis version > 6
- mariadb / mysql

### supported operating systems

* ArchLinux
* Debian based
    - Debian 10 / 11
    - Ubuntu 20.04
* RedHat based
    - CentOS 8 (**not longer supported**)
    - Alma Linux 8
    - Rocky Linux 8
    - OracleLinux 8

## usage

```yaml
icingadb_user: icingadb
icingadb_group: icingadb

icingadb_database: {}
icingadb_redis: {}
icingadb_logging: {}
```

### icingadb_database

```yaml
icingadb_database:
  host: database
  port: 3306
  database: icingadb
  user: icingadb
  password: icingadb
```
### icingadb_redis

```yaml

icingadb_defaults_redis:
  address: 127.0.0.1:6379
```

### icingadb_logging

#### `level`
Default logging level. Can be set to `fatal`, `error`, `warn`, `info` or `debug`.

If not set, defaults to `info`.

#### `output`
Logging output. Can be set to `console` (stderr) or `systemd-journald`.

If not set, logs to systemd-journald when running under systemd, otherwise stderr.

#### `interval`

Interval for periodic logging defined as duration string.
A duration string is a sequence of decimal numbers and a unit suffix, such as "20s".

Valid units are "ms", "s", "m", "h".

Defaults to `20s`.

#### `options`

Map of component-logging level pairs to define a different log level than the default
value for each component.

Can be set to `fatal`, `error`, `warn`, `info` or `debug`.

```yaml
icingadb_logging:
  level: info
  output: systemd-journald
  interval: "20s"
  options:
    database: fatal
    redis: fatal
    heartbeat: fatal
    high-availability: fatal
    config-sync: fatal
    history-sync: fatal
    runtime-updates: fatal
    overdue-sync: fatal
    dump-signals: fatal
```




## Contribution

Please read [Contribution](CONTRIBUTING.md)

## Development,  Branches (Git Tags)

The `master` Branch is my *Working Horse* includes the "latest, hot shit" and can be complete broken!

If you want to use something stable, please use a [Tagged Version](https://github.com/bodsch/ansible-icingaweb2/tags)!

---

## Author

- Bodo Schulz

## License

[Apache](LICENSE)

`FREE SOFTWARE, HELL YEAH!`
