# Observability Stack

This repository contains information on how to set up an Observability Stack for use with the NSO Observability Exporter. There are multiple available stacks that are suitable based on your needs, such as if you want a standalone stack or one integrated with NSO in Docker.

- `obstack-gtip`: Grafana, Tempo, InfluxDB, Prometheus & otlp-collector
  - this is a generic and standalone Observability Stack that works well with NSO
  - NSO itself is not included, since it is presumed you already have some way of running NSO
  - you can run NSO separately using a local install or in a container or any other way
- `nid`: Grafana, Tempo, InfluxDB, Prometheus & otlp-collector packaged for a NID testenv
  - fully integrated with NID testenvs, just drop in the 'nso_observability.mk` and include from Makefile
