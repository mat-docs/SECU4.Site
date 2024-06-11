# Configuration API

The configuration API is a new multi-platform API for ECU programming and monitoring, 
which will make it easier to handle multiple units, and to integrate across the network 
with clients written in languages including C#, C++, Python, Java or Go. The 
Configuration Service provides a modern, cross-platform gRPC interface, and mediates 
access to the units – via System Monitor – across the network from multiple clients. 
All existing COM API methods within System Monitor will be supported.

All information available via the COM API will be available via the Configuration 
Service.
All calls to the API are managed on a single threaded basis and any subsequent calls are
blocked until previous requests are completed.
Measurement values are cached within the API server to provide the fastest possible 
response time to requests, these calls are not blocked due to other actions. The rate of
cache update is configurable.
A .NET Standard client NuGet package and interface definition to make it easy to create 
interoperable tools using any mainstream language or platform.