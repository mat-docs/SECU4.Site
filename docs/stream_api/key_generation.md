# Key generation Service

Keys are used to uniquely identify objects within the Stream API. 
Examples include Session Keys and Data Format Ids.

### Ports
| Port  | Protocol | Usage                                |
|-------|----------|--------------------------------------|
| 15379 | gRPC     | Server connection for Key Generation | 


### Configuration
| Option | Value                                                | Required | Default |
|--------|------------------------------------------------------|----------|---------|
| PORT   | Port for gRPC communication as Key Generation server | No       | 15379   |

