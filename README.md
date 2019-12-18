# Docker Image with InfluxDB and Grafana

[![Docker Pulls](https://img.shields.io/docker/pulls/maxirosson/docker-influxdb-grafana.svg)](https://hub.docker.com/maxirosson/docker-influxdb-grafana) [![license](https://img.shields.io/github/license/maxirosson/docker-influxdb-grafana.svg)](https://hub.docker.com/maxirosson/docker-influxdb-grafana)

![Grafana][grafana-version] ![Influx][influx-version] ![Chronograf][chronograf-version]

This is a Docker image based on the awesome [Docker Image with InfluxDB and Grafana](https://github.com/philhawthorne/docker-influxdb-grafana) from [Phil Hawthorne](https://github.com/philhawthorne).

The main point of difference with this image is:

* Upgraded Grafana & InfluxDB versions
* Enabled Users Signup on Grafana
* Installed some Grafana plugins: `grafana-piechart-panel` & `grafana-influxdb-flux-datasource`
* Enabled InfluxDB Flux

| Description  | Value   |
|--------------|---------|
| InfluxDB     | 1.7.9   |
| ChronoGraf   | 1.7.12  |
| Grafana      | 6.5.2   |

## Quick Start

To start the container with persistence you can use the following:

```sh
docker run -d \
  --name docker-influxdb-grafana \
  -p 3003:3003 \
  -p 3004:8083 \
  -p 8086:8086 \
  -v /path/for/influxdb:/var/lib/influxdb \
  -v /path/for/grafana:/var/lib/grafana \
  philhawthorne/docker-influxdb-grafana:latest
```

To stop the container launch:

```sh
docker stop docker-influxdb-grafana
```

To start the container again launch:

```sh
docker start docker-influxdb-grafana
```

## Mapped Ports

```
Host		Container		Service

3003		3003			grafana
3004		8083			chronograf
8086		8086			influxdb
```
## SSH

```sh
docker exec -it <CONTAINER_ID> bash
```

## Grafana

Open <http://localhost:3003>

```
Username: root
Password: root
```

### Add data source on Grafana

1. Using the wizard click on `Add data source`
2. Choose a `name` for the source and flag it as `Default`
3. Choose `InfluxDB` as `type`
4. Choose `direct` as `access`
5. Fill remaining fields as follows and click on `Add` without altering other fields

Basic auth and credentials must be left unflagged. Proxy is not required.

Now you are ready to add your first dashboard and launch some queries on a database.

## InfluxDB

### Web Interface (Chronograf)

Open <http://localhost:3004>

```
Username: root
Password: root
Port: 8086
```

### InfluxDB Shell (CLI)

1. Establish a ssh connection with the container
2. Launch `influx` to open InfluxDB Shell (CLI)

[grafana-version]: https://img.shields.io/badge/Grafana-6.5.2-brightgreen
[influx-version]: https://img.shields.io/badge/Influx-1.7.9-brightgreen
[chronograf-version]: https://img.shields.io/badge/Chronograf-1.7.12-brightgreen
