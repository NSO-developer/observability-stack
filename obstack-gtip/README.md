# NSO Observability Stack

## Overview

This is an Observability Stack consisting of:
- Grafana as the web based GUI for showing metrics and traces
- Tempo for storage of trace data
- InfluxDB for trace-derived metrics
- Prometheus for metrics
- Otel-collector as OTLP receiver and forwards to Tempo & Prometheus

It is meant for use with NSO + Observability Exporter package.

## Start Observability Stack

`make start`

You'll find the Grafana UI on 'http://localhost:3000'

## Set up NSO for Observability Export

This folder contains only the Observability Stack itself. It is assumed you
already have NSO running somehow with the Observability Exporter installed.

This is primarily tested on Linux.

### Observability Exporter (OE)

You need to install the Observability Exporter package separately. Download it
from https://software.cisco.com

Install the package into the *packages* directory.
```
❯ cd packages/
❯ tar zxf <path>/ncs-6.0-observability-exporter-1.2.0.tar.gz
```

Observability Exporter have some Python dependencies. For a local install you
can create a virtualenv, install the packages and run NSO.

```
❯ python3 -m venv venv
❯ . venv/bin/activate
❯ pip install -r packages/observability-exporter/src/requirements.txt
```

#### Configure OE

Configure OE to export data to the Observability Stack running on localhost. If you are running NSO on a different computer, adjust the address accordingly.

```
❯ ncs_cli -u admin
admin@ncs# config
admin@ncs(config)# unhide debug
admin@ncs(config)# progress export otlp host localhost
admin@ncs(config)# progress export influxdb host localhost
admin@ncs(config)# commit
```
