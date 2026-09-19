# observability-stack

Metrics, logs, and traces for the labs in this repo. Telemetry flows from
the `collectors/`, `gnmi-openconfig/`, `snmp/`, `syslog/`, `netflow-ipfix/`,
and `telegraf/` subdirectories into storage/query backends
(`prometheus/`, `influxdb/`, `loki/`, `tempo/`), which `grafana/` and
`dashboards/` visualize. `exporters/` holds Prometheus exporters bridging
non-native metric sources into this pipeline.

**Status:** Scaffolded, no content yet — start with `/speckit-specify`.
