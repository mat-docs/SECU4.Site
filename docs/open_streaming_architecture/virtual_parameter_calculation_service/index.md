# Virtual Parameter Service

## Overview

The Virtual Parameter Service is a container-native component of the Open Streaming Architecture that simplifies the calculation and distribution of virtual parameters. Virtual parameters are defined as FDL (Function Definition Language) functions in ECU logging configurations and are traditionally calculated on-demand by clients.

## Key Features

- **Real-time Calculation**: Performs calculations in real-time, eliminating the need for downstream client recalculations
- **Stream Integration**: Seamlessly integrates with the Stream API for data distribution
- **Consistency**: Ensures consistent parameter calculations across all consumers
- **Performance Optimization**: Reduces client-side processing load
- **Monitoring**: Comprehensive metrics collection via Prometheus integration

## Architecture

The service is designed as a container-native application with the following key components:

- **Host Service**: Manages the service lifecycle and configuration
- **Component Layer**: Core calculation engine for virtual parameters
- **Common Library**: Shared functionality and interfaces
- **Internal Support Library**: Supporting utilities and infrastructure
- **Auditor Tools**: Monitoring and diagnostic capabilities

## Getting Started

### Prerequisites

- Docker runtime environment
- Prometheus (for monitoring)

### Running the Service

The service is distributed as a Docker container and is available on Docker Hub:

```bash
docker pull mclarenapplied/virtual-parameter-service-host
```

The service can be run using:

```bash
docker run mclarenapplied/virtual-parameter-service-host
```

## Monitoring

The service exposes comprehensive metrics through Prometheus, which can be visualized using Grafana. Key metrics include:

- Data source configuration status
- Session connection statistics
- Packet processing metrics
- Parameter definition tracking
- Virtual parameter calculation performance

### Accessing Metrics

Metrics can be accessed through:
- Prometheus targets endpoint
- Direct metrics endpoint

## Integration

The service integrates with the Open Streaming Architecture through:

1. **Stream API**: For data input and output
2. **Prometheus**: For metrics collection
3. **Configuration API**: For service configuration

## Best Practices

- Monitor the service metrics regularly to ensure optimal performance
- Configure appropriate resource limits in container environments
- Regularly update the service to benefit from performance improvements and bug fixes

## Support

For support and additional information, please refer to:
- [Open Streaming Architecture Documentation](https://atlas.mclarenapplied.com/secu4/open_streaming_architecture/)
- Service metrics and logs
- Technical support channels

## Metrics Reference

| Metric | Description | Labels |
|--------|-------------|--------|
| `vps_running_gauge_of_data_sources` | Running gauge of data sources configured for the virtual parameter service | - |
| `vps_running_gauge_of_connected_sessions` | Running gauge of connected sessions for the virtual parameter service | - |
| `vps_packet_dispatcher_counter` | Counter for the number of packets received | `action`, `data_source` |
| `vps_parameter_definition_counter` | Counter for the number of definitions | `type`, `data_source` |
| `vps_virtual_parameter_definition_failed_counter` | Counter for the number of failed virtual parameter definitions | `data_source` |
| `vps_virtual_parameter_definition_incomplete_gauge` | Gauge for the number of incomplete virtual parameter definitions | `data_source` |
| `vps_virtual_parameter_definition_built_counter` | Counter for the number of built virtual parameter definitions | `data_source` |
| `vps_data_packet_handler_parameter_sample_counter` | Counter for the number of samples received by the data packet handler for active parameter | `parameter_identifier`, `data_source` |
| `vps_parameter_data_buffer_counter` | Counter for the number of packets processed by a parameter | `parameter_identifier`, `data_source` |
| `vps_parameter_sample_store_gauge` | Gauge for the number of samples in the same parameter sample store | `parameter_identifier`, `data_source` |
| `vps_parameter_changed_notify_consumer_counter` | Counter for the number of notifications sent for a consumer | `consumer_identifier`, `parameter_identifier`, `data_source` |
| `vps_virtual_parameter_parameter_changed_buffer_counter` | Counter for the number of notifications received from its source parameters | `source_identifiers`, `data_source` |
| `vps_virtual_parameter_parameter_changed_counter` | Counter for the number of notifications received from its source parameters | `source_identifer`, `data_source` |

### Label Descriptions

| Label | Description |
|-------|-------------|
| `data_source` | The typically default provided by ADS |
| `session_key` | The session key |
| `parameter_identifier` | The parameter identifier |
| `type` | The type (differs per use, e.g., parameter or virtual) |
| `action` | Context specific (e.g., handled or unhandled for packet dispatcher) |
| `source_identifer` | The parameter that notified a virtual of new samples |
| `source_identifers` | The parameter identifiers that make up a virtual |
| `consumer_identifier` | The consumer identifier of the parameter in context |
| `sequence` | The point a subscriber of a parameter active after the first sub | 
