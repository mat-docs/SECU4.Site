# Stream API / Protocol 

A standard API to expose streaming data from SECU units and abstract away proprietary
implementation details. Consumers of this API will be able to write software that 
interfaces with any viewer, network protocol, or storage technology of their choice. 
All the data from the SECU unit (after RDA filtering) will be available on the stream.
This will be integrated with a protocol for streaming engineering (calibrated) 
telemetry, interoperating with ATLAS clients and the surrounding data processing 
ecosystem.
 
# Components
For the 2024 July milestone, 3 components will be delivered for evaluation:

1. Stream API container
2. Stream API client as NuGet package
3. Windows service application (TODO: ADS Dev version?)

# Sample Implementation

## Simple stream produce consumer
In this scenario, a custom data producer can publish data onto the Kafka broker via the
Stream API client and the Stream API Container. 

The Stream API Client is an in-process API, so in the implementation, the producer and the
Stream API Client can be in the same executable. The Stream API Client will establish a 
gRPC channel with the Container to transfer the data to be published to the broker. 

The same combination of Stream API Container and Stream API Client can be used to 
retrieve the same data from the broker.

![Architecture of simple stream producer consumer](assets/stream_architecture_light.png#only-light)
![Architecture of simple stream producer consumer](assets/stream_architecture_dark.png#only-dark)

## Streaming SECU data

With the Windows service application provided, SECU data can be streamed into a Kafka broker.

![Architecture of streaming SECU data](assets/SECU_data_light.png#only-light)
![Architecture of streaming SECU data](assets/SECU_data_dark.png#only-dark)
