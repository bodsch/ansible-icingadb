
# Ansible Role:  `icingadb`

This role will fully configure and install [icingadb](https://icinga.com/docs/icinga-db).


[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/bodsch/ansible-icingadb/main.yml?branch=main)][ci]
[![GitHub issues](https://img.shields.io/github/issues/bodsch/ansible-icingadb)][issues]
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/bodsch/ansible-icingadb)][releases]
[![Ansible Quality Score](https://img.shields.io/ansible/quality/50067?label=role%20quality)][quality]

[ci]: https://github.com/bodsch/ansible-icingadb/actions
[issues]: https://github.com/bodsch/ansible-icingadb/issues?q=is%3Aopen+is%3Aissue
[releases]: https://github.com/bodsch/ansible-icingadb/releases
[quality]: https://galaxy.ansible.com/bodsch/icingadb



## Requirements & Dependencies

Ansible Collections

- [bodsch.core](https://github.com/bodsch/ansible-collection-core)

```bash
ansible-galaxy collection install bodsch.core
```
or
```bash
ansible-galaxy collection install --requirements-file collections.yml
```

- redis version > 6
- mariadb / mysql

### supported operating systems

* ArchLinux
* Debian based
    - Debian 10 / 11
    - Ubuntu 20.04

## usage

```yaml
icingadb_user: icingadb
icingadb_group: icingadb

icingadb_database: {}
icingadb_redis: {}
icingadb_logging: {}
```

### `icingadb_database`

```yaml
icingadb_database:
  host: database
  port: 3306
  database: icingadb
  user: icingadb
  password: icingadb
```

### `icingadb_redis`

```yaml

icingadb_redis:
  host: 127.0.0.1
  port: 6379
```

### `icingadb_logging`

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



### `icingadb_retention`

By default, no historical data is deleted, which means that the longer the data is retained, the more disk
space is required to store it. History retention is an optional feature that allows you to limit the number
of days that historical data is available for each history category. There are separate options for the full
history tables used to display history information in the web interface and SLA tables which store the
minimal information required for SLA reporting, allowing to keep this information for longer with a smaller
storage footprint.

All parameters are given in days, e.g. `120`

#### `history-days`

**Optional**

Number of days to retain historical data for all history categories.

Use options in order to enable retention only for specific categories or to override the retention days configured here.


#### `sla-days

**Optional**

*Number of days* to retain historical data for SLA reporting.

#### `options`

**Optional**

Map of history category to *number of days* to retain its data.

Available categories are `acknowledgement`, `comment`, `downtime`, `flapping`, `notification` and `state`.


```yaml
icingadb_retention:
  history_days: ""
  sla_days: ""
  options:
    acknowledgement: ""
    comment: ""
    downtime: ""
    flapping: ""
    notification: ""
    state: ""
```

## Contribution

Please read [Contribution](CONTRIBUTING.md)

## Development,  Branches (Git Tags)

The `master` Branch is my *Working Horse* includes the "latest, hot shit" and can be complete broken!

If you want to use something stable, please use a [Tagged Version](https://github.com/bodsch/ansible-icingadb/tags)!

---

## Author

- Bodo Schulz

## License

[Apache](LICENSE)

**FREE SOFTWARE, HELL YEAH!**
