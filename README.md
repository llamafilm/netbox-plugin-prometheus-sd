# netbox-plugin-prometheus-sd

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![CI](https://github.com/FlxPeters/netbox-plugin-prometheus-sd/workflows/CI/badge.svg?event=push)](https://github.com/FlxPeters/netbox-plugin-prometheus-sd/actions?query=workflow%3ACI)

Provide Prometheus http_sd compatible API Endpoint with data from Netbox.

HTTP SD is a new feature in Prometheus 2.28.0 that allows hosts to be found via a URL instead of just files. 
This plugin implements API endpoints in Netbox to make devices, IPs and virtual machines available to Prometheus.

## Installation

The plugin is available as a Python package in pypi and can be installed with pip

    pip install netbox-plugin-prometheus-sd

Enable the plugin in /opt/netbox/netbox/netbox/configuration.py:

    PLUGINS = ['netbox_prometheus_sd']

The plugin has not further plugin configuration at the moment.

## Usage

The plugin only provides a new API endpoint on the Netbox API. There is no further action required after installation. 

## API

The plugin reuses Netbox API view sets with new serializers for Prometheus. 
This means that all filters that can be used on the Netbox api can also be used to filter Prometheus targets.

```shell
GET        /api/plugins/prometheus-sd/devices/              Get a list of devices in a prometheus compatible format
GET        /api/plugins/prometheus-sd/virtual-machines/     Get a list of vms in a prometheus compatible format
GET        /api/plugins/prometheus-sd/ip-addresses/         Get a list of ip in a prometheus compatible format
```

The plugin also reuses the Netbox authentication and permission model. 
Depending on the configuration, a token must be passed to Netbox for authentication.

## Development

We use Poetry for dependency management and invoke as task runner. 
As Netbox plugins cannot be tested standalone, we need invoke to start all code embedded in Netbox Docker containers.

All code to run in docker is located under `development` which is also the starting point for VScode remote containers (not finished yet).

To start a virtual env managed by poetry run `poetry shell`. 
