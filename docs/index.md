# SECU 4 Off Car Systems Documentation

## [Configuration API](configuration_api/index.md)
A new multi-platform API for ECU programming and monitoring, which will make it easier 
to handle multiple units, and to integrate across the network with clients written in 
languages including C#, C++, Python, Java or Go. The Configuration Service provides a 
modern, cross-platform gRPC interface, and mediates access to the units – via System 
Monitor – across the network from multiple clients. 

## [Open Streaming Architecture](open_streaming_architecture/index.md)
A standard, open set of rules and services for streaming telemetry data over a broker 
(assumed to be Kafka, but other brokers will be supported). Includes full definition of 
the Protobuf schema for transmitting messages, along with documentation describing the 
messages.

## Historical Data Storage (Parquet)
In addition to the ATLAS session formats, a Parquet format will be supported for storing
open engineering data directly from the stream or as an export from ATLAS.
Parquet is an open-source file format for storing large datasets in an optimized way. 
Columnar storage allows for fast data processing and good compression rates. Parquet 
files can be easily accessed using a variety of programming languages and APIs, to allow
teams to access their data independent of ATLAS.

[//]: # ([Historical Data Storage]&#40;historic_data/index.md&#41; \)
