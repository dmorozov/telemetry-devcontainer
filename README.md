# Devcontainer with OpenTelemetry, Prometheus+Grafana, Jaeger and Zippkin

## Disclaimer

This is personal playground template project to get working configuration for the telemetry (distributed tracing) and metrics within Devcontainers.
All credits for [OpenTelemetry](https://github.com/open-telemetry) and [OpenTelemetry Collector Contrib](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main) projects.

The test demo server was taken from the [OpenTelemetry Collector Demo](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/examples/demo) without any changes. It is written in go but that not important for the matter for the example. It is using OpenTelemetry API to report telemetry traces to the open source distributed tracing applications like Jaeger and Zippkin through special OpenTelemetry connector. The demo test server can be replaced with any application of your language choice as soon as it is using OpenTelemetry API.

The demo endpoint can be triggered as HTTP GET to <http://localhost:7080/hello>

## Configuration

1. OpenTelemetry collector providing OpenTelemetry API.
2. Jaeger and Zipkin to collect distributed traces (telemetry).
3. Prometheus to collect metrics.

## Limitations

The common approach I found to configure Devcontainer network is to use network mode like this (when using docker-container configuration):

```docker-compose.yml
...
    network_mode: service:telemetry-test-db
```

where "telemetry-test-db" is the network used by DB service. That allows to use Devcontainer "forwardPorts" (in the devcontainer.json) to forward ports outside of the Devcontainer.

I wasn't able to make this network configuration work properly.
So, I have configured more classic bridge network within the Devcontainer and have port forwarding "standard" docker-compose way.
It doesn't show port forwarded in Devcontainer "Ports" panel (at the bottom of the VSCode). But all ports are still forwarded with docker-compose itself so available at the host system.
