# Open Streaming Architecture
A standard, open set of rules and services for streaming telemetry data over a broker 
(assumed to be Kafka, but other brokers will be supported). Includes full definition of 
the Protobuf schema for transmitting messages, along with documentation describing the 
messages.
 
**Hight level pic**
 

## Components

### [Stream API](stream_api/overview)
A standard API to expose streaming data from SECU units and abstract away proprietary 
implementation details. Consumers of this API will be able to write software that 
interfaces with any viewer, network protocol, or storage technology of their choice. 
All the data from the SECU unit (after RDA filtering) will be available on the stream. 
This will be integrated with a protocol for streaming engineering (calibrated) telemetry, 
interoperating with ATLAS clients and the surrounding data processing ecosystem.

### Routing Service

### Bridge Service

### Virtual Parameter Service

### Multicaster Service


