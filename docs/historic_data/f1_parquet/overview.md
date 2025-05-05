# F1 Parquet Format Overview

The F1 Parquet Format is a high-performance library for reading and writing Formula 1 data in Parquet format, adapted from Mercedes AMG Grand Prix Ltd. and supporting various data types for McLaren Applied's control units (ECUs).

## Key Features

- **High Performance**: Optimized for large datasets
- **Multiple Language Support**: C#, Python, and MATLAB interfaces
- **Flexible Data Types**: Support for various Formula 1 data formats
- **Advanced Compression**: Multiple compression algorithms
- **Schema Validation**: Robust data validation
- **Metadata Support**: Rich metadata capabilities

## System Components

The library consists of several key components:

1. **ArrowWrapper**
   - Implements the Apache Arrow Parquet interface
   - Provides entry points for reading timeseries, events, and metadata files
   - Handles low-level Parquet file operations

2. **PolarisParquet**
   - Defines schemas and metadata structures
   - Implements business logic for reading and writing files
   - Manages data type conversions and validations

3. **PolarisParquetNet**
   - Generates and builds the SWIG interface C layer
   - Enables C# interoperability
   - Provides type-safe bindings for .NET applications

4. **Polaris.Parquet.Wrapper**
   - Builds the generated SWIG C# files
   - Provides a high-level C# API
   - Implements .NET-specific optimizations

## Supported Platforms

### Windows
- Visual Studio 2023
- MATLAB 2023b
- Python 3.10
- C# net6.0

### Linux (Coming Soon)
- Ubuntu 22.04
- GCC 10.3
- Python 3.10

## Data Types

The library supports two main types of data:

1. **Timeseries Data**
   - Continuous measurements over time
   - Sensor readings and telemetry data
   - High-frequency data streams

2. **Event Data**
   - Discrete occurrences
   - System state changes
   - Alerts and notifications

## Next Steps

1. Review the [Architecture](architecture.md) documentation
2. Check the [Data Model](data_model.md) specifications
3. Explore the [File Format](file_format.md) details 