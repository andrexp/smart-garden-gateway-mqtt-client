
# Generic GARDENA smart Gateway MQTT client

This is an unofficial service for the GARDENA smart Gateway, allowing the GARDENA
smart system to be monitored and controlled without the cloud.

## Prerequisites

You will need shell access to your GARDENA smart Gateway. The instructions for
that can be found in the [smart-garden-gateway-public] repository.

[smart-garden-gateway-public]: https://github.com/husqvarnagroup/smart-garden-gateway-public#getting-access

## Configuration

The minimal required configuration can be created as follows:
```
cat << EOF > /etc/sg-mqtt-client.conf
[mqtt_broker]
host = my-mqtt-broker.lan
EOF
```

Here, all the available settings and their default values:
```
[mqtt_broker]
host = localhost
port = 1883

[mqtt_topics]
command = smart-garden/command
event = smart-garden/event
```

## Installation

To install the service on the GARDENA smart Gateway, run the following commands:
```
opkg update
opkg install sg-mqtt-client
```

To preserve the application across OS upgrades, you can run:
```
echo sg-mqtt-client >> /etc/devpkgs.conf
```

After the installation, the service should automatically start up. To inspect
the logs, run:
```
journalctl -u sg-mqtt-client
```

## Development

The application can be built and run as usual:
```
cargo run
```

To change the behavior of the application, either place a configuration file in
the current directory or set environment variables like
`SG_MQTT_CLIENT__MQTT_BROKER__HOST`.
