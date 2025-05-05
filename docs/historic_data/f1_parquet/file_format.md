# File Format

The F1 Parquet Format uses Apache Parquet as its underlying storage format, with specific conventions for F1 data.

## File Structure

### 1. File Header
- Magic number: "PAR1"
- File metadata
- Schema definition

### 2. Row Groups
- Data organized in row groups
- Each row group contains:
  - Column chunks
  - Column metadata
  - Statistics

### 3. File Footer
- File metadata
- Schema information
- Statistics
- Magic number: "PAR1"

## Metadata

### Required Metadata

```json
{
    "format_version": "1.0",
    "created_by": "MA.DataPlatforms.FiaF1ParquetFormat",
    "session_info": {
        "session_id": "string",
        "track": "string",
        "date": "YYYY-MM-DD",
        "time": "HH:MM:SS"
    }
}
```

### Optional Metadata

```json
{
    "car_info": {
        "team": "string",
        "driver": "string",
        "car_number": "integer"
    },
    "recording_info": {
        "start_time": "timestamp",
        "end_time": "timestamp",
        "duration": "float"
    }
}
```

## Compression

### Supported Compression Types

1. **Uncompressed**
   - No compression
   - Fastest read/write
   - Largest file size

2. **Snappy**
   - Default compression
   - Good balance of speed and size
   - Recommended for most use cases

3. **Gzip**
   - Higher compression ratio
   - Slower read/write
   - Good for archiving

### Compression Settings

```csharp
var options = new ParquetOptions
{
    Compression = CompressionType.Snappy,
    RowGroupSize = 128 * 1024 * 1024, // 128MB
    WriteBatchSize = 10000
};
```

## Data Organization

### Timeseries Data

1. **Column Layout**
   ```
   +-------------+-------------+-------------+
   | Timestamp   | ChannelName | Value       |
   +-------------+-------------+-------------+
   | 0.0         | Engine.RPM  | 12000.0     |
   | 0.1         | Engine.RPM  | 12500.0     |
   | 0.2         | Engine.RPM  | 13000.0     |
   +-------------+-------------+-------------+
   ```

2. **Row Group Organization**
   - Grouped by time windows
   - Optimized for sequential access
   - Balanced size for performance

### Event Data

1. **Column Layout**
   ```
   +-------------+-------------+-------------+
   | Timestamp   | EventType   | Parameters  |
   +-------------+-------------+-------------+
   | 123.456     | GearChange  | {...}       |
   | 124.567     | DRSActive   | {...}       |
   | 125.678     | ButtonPress | {...}       |
   +-------------+-------------+-------------+
   ```

2. **Row Group Organization**
   - Grouped by event type
   - Optimized for random access
   - Smaller row groups

## File Naming Convention

### Pattern
```
{SessionID}_{DataType}_{Timestamp}.parquet
```

### Examples
```
2023_Bahrain_GP_Timeseries_20230305_120000.parquet
2023_Bahrain_GP_Events_20230305_120000.parquet
```

## Performance Considerations

### Reading Optimization

1. **Column Projection**
   ```csharp
   var options = new ParquetReaderOptions
   {
       Columns = new[] { "Timestamp", "Engine.RPM" }
   };
   ```

2. **Row Group Selection**
   ```csharp
   var options = new ParquetReaderOptions
   {
       RowGroupIndices = new[] { 0, 1, 2 }
   };
   ```

### Writing Optimization

1. **Batch Writing**
   ```csharp
   var writer = new ParquetWriter("output.parquet", schema);
   writer.WriteBatch(data, batchSize: 10000);
   ```

2. **Row Group Size**
   ```csharp
   var options = new ParquetWriterOptions
   {
       RowGroupSize = 128 * 1024 * 1024 // 128MB
   };
   ```

## Next Steps

1. Return to [Data Model](data_model.md)
2. Return to [Architecture](architecture.md)
3. Return to [Overview](overview.md) 