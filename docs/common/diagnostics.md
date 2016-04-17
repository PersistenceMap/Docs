Diagnostics can be added to PersistenceMap in several ways  

## App.config
Add a Diagnostics Writer through the global application configuration file. To add loggers, PersistenceMap provides a ConfigurationSection in the Namespace PersistenceMap.Configuration.
```xml
<configuration>
  <configSections>
    <section name="PersistenceMap" type="PersistenceMap.Configuration.PersistenceMapSection, PersistenceMap" />
  </configSections>
  <PersistenceMap>
    <loggers>
      <!-- Write all log messages of PersistenceMap to System.Diagnostics.Trace -->
      <add type="PersistenceMap.Diagnostics.TraceLogger, PersistenceMap"/>
    </loggers>
  </PersistenceMap>
</configuration>
```
  
## Per Context
Loggers can also be added directly to the Settings of a Context
```csharp
context.Settings.AddWriter(new TraceLogger());
```

## LoggerConfiguration
The LoggerConfiguration object is a Builder class that helps add Diagnostics to the Context.  

### Per Context
The Method SetToFactory(Settings) adds the logger to the settings that are specifig to the given Context.  
```csharp
new LoggerConfiguration()
    .AddWriter(new TraceLogger())
    .SetToFactory(context.Settings);
```

### Global
The Method SetDefault() adds the logger globaly to all Context.    
```csharp
new LoggerConfiguration()
    .AddWriter(new TraceLogger())
    .SetDefault();
``` 