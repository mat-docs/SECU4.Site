# Data Model

The F1 Parquet Format supports two main types of data: Timeseries Data and Event Data.

## Timeseries Data

Timeseries data represents continuous measurements from various sensors and systems.

### Structure

```csharp
public class TimeseriesData
{
    public string ChannelName { get; set; }
    public DataType DataType { get; set; }
    public string Unit { get; set; }
    public double[] Timestamps { get; set; }
    public object[] Values { get; set; }
    public Dictionary<string, string> Metadata { get; set; }
}
```

### Supported Data Types

1. **Numeric Types**
   - `Int8`, `Int16`, `Int32`, `Int64`
   - `UInt8`, `UInt16`, `UInt32`, `UInt64`
   - `Float32`, `Float64`

2. **Boolean Type**
   - `Boolean`

3. **String Type**
   - `String`

4. **Timestamp Types**
   - `Timestamp` (nanosecond precision)
   - `Date32`
   - `Time32`
   - `Time64`

### Example

```csharp
var data = new TimeseriesData
{
    ChannelName = "Engine.RPM",
    DataType = DataType.Float64,
    Unit = "RPM",
    Timestamps = new double[] { 0.0, 0.1, 0.2 },
    Values = new double[] { 12000.0, 12500.0, 13000.0 },
    Metadata = new Dictionary<string, string>
    {
        { "Source", "ECU" },
        { "SamplingRate", "100Hz" }
    }
};
```

## Event Data

Event data represents discrete occurrences or state changes.

### Structure

```csharp
public class EventData
{
    public string EventType { get; set; }
    public double Timestamp { get; set; }
    public Dictionary<string, object> Parameters { get; set; }
    public Dictionary<string, string> Metadata { get; set; }
}
```

### Event Types

1. **System Events**
   - Session start/end
   - System state changes
   - Error conditions

2. **Driver Events**
   - Button presses
   - Control inputs
   - Driver messages

3. **Vehicle Events**
   - Gear changes
   - DRS activations
   - System activations

### Example

```csharp
var event = new EventData
{
    EventType = "GearChange",
    Timestamp = 123.456,
    Parameters = new Dictionary<string, object>
    {
        { "OldGear", 3 },
        { "NewGear", 4 },
        { "RPM", 12000.0 }
    },
    Metadata = new Dictionary<string, string>
    {
        { "Source", "Gearbox" },
        { "Driver", "HAM" }
    }
};
```

## Schema Definition

### Timeseries Schema

```csharp
var schema = new SchemaBuilder()
    .AddColumn("Timestamp", DataType.Float64)
    .AddColumn("ChannelName", DataType.String)
    .AddColumn("Value", DataType.Float64)
    .AddColumn("Unit", DataType.String)
    .Build();
```

### Event Schema

```csharp
var schema = new SchemaBuilder()
    .AddColumn("Timestamp", DataType.Float64)
    .AddColumn("EventType", DataType.String)
    .AddColumn("Parameters", DataType.Map)
    .Build();
```

## Data Validation

### Timeseries Validation

1. **Data Type Validation**
   - Verify value types match schema
   - Check for null values
   - Validate numeric ranges

2. **Timestamp Validation**
   - Ensure monotonic increase
   - Check for gaps
   - Validate against session time

### Event Validation

1. **Event Type Validation**
   - Verify event type exists
   - Check required parameters
   - Validate parameter types

2. **Timestamp Validation**
   - Check against session time
   - Validate sequence
   - Detect duplicates

## Next Steps

1. Review the [File Format](file_format.md) specifications
2. Return to [Architecture](architecture.md)
3. Return to [Overview](overview.md) 