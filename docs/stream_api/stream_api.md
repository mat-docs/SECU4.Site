# Stream API

The Stream API is responsible for publishing and consuming data from the Kafka broker.

The Stream API consist of a server, and a client, with gRPC channel to communicate between the two.

The server and the client can be deployed locally within the same application or the server can be deployed remotely 
with the docker image provided.

## Stream API Server Container
### Ports
| Port  | Protocol | Usage                                               |
|-------|----------|-----------------------------------------------------|
| 13579 | gRPC     | Communication with Stream API Client                |  
| 15379 | gRPC     | Remote Key Generator service                        |

### Configuration
| Option        | Value                                         | Required | Default                   |
|---------------|-----------------------------------------------|----------|---------------------------|
| `CONFIG_PATH` | Path to the config file within the container. | No       | `/Configs/AppConfig.json` |

### Configuration file
Several options are available for 

| Option                             | Value                                                                                                                                                        | Required                                        | Default | DataType              |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|---------|-----------------------|
| `StreamCreationStrategy`           | `1` for partition based, or<br/> `2` for topic based                                                                                                         | Yes                                             |         | int                   |
| `BrokerUrl`                        | URL to the Kafka broker including port number                                                                                                                | Yes                                             |         | string                |
| `PartitionMappings`                | An array of Key/Value pairs mapping the stream to a specific topic/partition                                                                                 | Required when `StreamCreationStrategy` is `1`   |         | array\[(string,int)\] |
| `IntegrateSessionManagement`       | True to enable the integrated session management service.                                                                                                    | No                                              | `true`  | bool                  |
| `IntegrateDataFormatManagement`    | True to enable the data format management service.                                                                                                           | No                                              | `true`  | bool                  |
| `UseRemoteKeyGenerator`            | Use a Remote Key Generator within the Data Format Management Service, if used.                                                                               | No                                              | `false` | bool                  |
| `RemoteKeyGeneratorServiceAddress` | The address of the service if the remote key generator service is used.                                                                                      | Required when `UseRemoteKeyGenerator` is `true` | `""`    | string                |
| `BatchingResponses`                | Process messages in batch, at a cost of minor latency, this allows a large amount of messages at the same time. Recommended to be use during session offload | No                                              | `false` | bool                  |
| `StreamApiPort`                    | Port to be used to establish the gRPC connection                                                                                                             | No                                              | `13579` | int                   |

### PartitionMappings

Topic based - no partition mapping require - refer to open doc for more info 

[//]: # (TODO: link to doc / reword)
Partition based - if there is no partition mapping given, the default partition of the main topic will be used.   


