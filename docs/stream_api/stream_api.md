# Stream API

The Stream API is responsible for publishing and consuming data from the Kafka broker. Created under the gRPC framework,
it allows clients to communicate to a server which handles the kafka communication.

The server and the client can be deployed locally within the same application or the server can be deployed remotely 
with the docker image provided.

## Stream API Client

C# libraries for the Stream API Client are compiled from the proto files, to facilitate deployment.

`MA.Streaming.Proto.Client.Local` can be used in conjunction with `MA.Streaming.Proto.ServerComponent`. 

`MA.Streaming.Proto.Client.Remote` can be used in conjunction with the [Stream API Server Container](./#stream-api-server-container).

Given the API is created under the gRPC framework, it is possible to generate client and server classes in a language of
your choice. 
For details documentation of each of the RPC calls, refer to the [proto file]().

## Stream API Server Container

The image for the Stream API Server is available on DockerHub as `mclarenapplied/streaming-proto-server-host` 

### Ports
| Port                                            | Protocol | Usage                                |
|-------------------------------------------------|----------|--------------------------------------|
| 13579, or `StreamApiPort`                       | gRPC     | Communication with Stream API Client |  
| Dependent on `RemoteKeyGeneratorServiceAddress` | gRPC     | Remote Key Generator service         |

### Configuration
| Option        | Value                                                                | Required | Default                   |
|---------------|----------------------------------------------------------------------|----------|---------------------------|
| `CONFIG_PATH` | Path to the [config file](#configuration-file) within the container. | No       | `/Configs/AppConfig.json` |

### Configuration file
Several options are available for 

| Option                             | Value                                                                          | Required                                          | Default | DataType              |
|------------------------------------|--------------------------------------------------------------------------------|---------------------------------------------------|---------|-----------------------|
| `BrokerUrl`                        | URL(s) to the Kafka broker including port number, separated by commas.         | Yes                                               |         | string                |
| `StreamCreationStrategy`           | `1` for partition based, or<br/> `2` for topic based                           | Yes                                               |         | int                   |
| `PartitionMappings`                | An array of Key/Value pairs mapping the stream to a specific partition         | Only applies when `StreamCreationStrategy` is `1` |         | array\[(string,int)\] |
| `IntegrateSessionManagement`       | True to enable the integrated session management service.                      | No                                                | `true`  | bool                  |
| `IntegrateDataFormatManagement`    | True to enable the data format management service.                             | No                                                | `true`  | bool                  |
| `UseRemoteKeyGenerator`            | Use a Remote Key Generator within the Data Format Management Service, if used. | No                                                | `false` | bool                  |
| `RemoteKeyGeneratorServiceAddress` | The address of the service if the remote key generator service is used.        | Required when `UseRemoteKeyGenerator` is `true`   | `""`    | string                |
| `BatchingResponses`                | Process messages in [batch](#batching-responses).                              | No                                                | `false` | bool                  |
| `StreamApiPort`                    | Port to be used to establish the gRPC connection                               | No                                                | `13579` | int                   |

## Stream Creation Strategy

Data can be split into multiple streams to suite your requirements. `StreamCreationStrategy` allows you to partition the
data into streams that corresponds to kafka topics or partitions. 

### Topic based

When a topic based stream creation strategy is applied, data will be published to a topic named `{DataSource}.{Stream}`,
e.g. a source named `Chassis` with an app group `Driver` will publish to the topic `Chassis.Driver`. If the Stream is 
not defined, it will publish to the "main topic", that is `{DataSource}`. 

### Partition Based
When a partition based stream creation strategy is applied, the data will be published to the main topic `{datasource}`, and 
the corresponding partition based on `PartitionMappings`
If there are no partition mapping given, the default partition of the main topic will be used.   


## Batching Responses

When a high amount of messages is processed at the same time. The overhead can be significant and the bandwidth can be 
more efficiently utilised by batching the responses. 

The configuration on the server side corresponds to the behaviour when consuming off the broker, whereas 
the configuration on the client side corresponds to the behaviour when producing to the broker.
