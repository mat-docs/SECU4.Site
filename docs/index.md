# SECU 4 Off Car Systems Documentation

## Configuration API
A new multi-platform API for ECU programming and monitoring, which will make it easier 
to handle multiple units, and to integrate across the network with clients written in 
languages including C#, C++, Python, Java or Go. The Configuration Service provides a 
modern, cross-platform gRPC interface, and mediates access to the units – via System 
Monitor – across the network from multiple clients. 

[Configuration API](configuration_api/index.md) 

## Open Streaming Architecture
A standard API to expose streaming data from SECU units and abstract away proprietary
implementation details. Consumers of this API will be able to write software that 
interfaces with any viewer, network protocol, or storage technology of their choice. 
All the data from the SECU unit (after RDA filtering) will be available on the stream.
This will be integrated with a protocol for streaming engineering (calibrated) 
telemetry, interoperating with ATLAS clients and the surrounding data processing 
ecosystem.

[Open Streaming Architecture](stream_api/index.md) 

## Historical Data Storage (Parquet)
In addition to the ATLAS session formats, a Parquet format will be supported for storing
open engineering data directly from the stream or as an export from ATLAS.
Parquet is an open-source file format for storing large datasets in an optimized way. 
Columnar storage allows for fast data processing and good compression rates. Parquet 
files can be easily accessed using a variety of programming languages and APIs, to allow
teams to access their data independent of ATLAS.

[Historical Data Storage](historic_data/index.md) 
