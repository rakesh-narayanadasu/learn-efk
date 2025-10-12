# Input, Filter and Output Plugins in Fluent Bit

## Input Plugins
Input plugins are the starting point for data collection in Fluent Bit. They interface with various data sources, ensuring that logs are correctly captured for further processing. Here are some common input plugins:

**1. Tail Plugin:**
The Tail plugin reads data from log files as new entries are written. It is particularly useful for monitoring application logs, such as those from Nginx.

```
[INPUT]
  Name   tail
  Path   /var/log/nginx/access.log
  Tag    nginx.access
  Parser nginx
```

**2. Systemd Plugin:**
Use the Systemd plugin to collect logs from the system journal. This is ideal for systems managed by Systemd, capturing both application and service logs.
```
[INPUT]
  Name   systemd
  Tag    host.*
```

**3. TCP Plugin**
The TCP plugin listens for logs sent over TCP connections, making it versatile for capturing network-based logging data.
```
[INPUT]
  Name   tcp
  Listen 0.0.0.0
  Port   5170
  Tag    tcp.input
```

## Filter Plugins
Once the logs are collected, they often need processing before reaching their final destination. Fluent Bit’s filter plugins facilitate this by transforming, enriching, or screening the raw log data.

**1. Grep Plugin:**
The Grep plugin filters log records by using regular expressions. For instance, to capture only logs that contain error messages:
```
[FILTER]
  Name   grep
  Match  nginx.access
  Regex  message error
```
**2. Modify Plugin:**
With the Modify plugin, you can add, remove, or alter fields in your log entries. This is useful for including extra context, such as the service name.
```
[FILTER]
  Name  modify
  Match *
  Add   service nginx
```
**3. Parser Plugin:**
The Parser plugin converts unstructured log data (e.g., JSON strings) into a more organized structure for easier analysis.
```
[FILTER]
  Name      parser
  Match     nginx.access
  Key_Name  message
  Parser    json
```

## Output Plugins
After processing, log data is transmitted to designated destinations through output plugins. These plugins ensure that logs are stored in systems where they can be queried and analyzed.

**1. Elasticsearch (ES) Plugin:**
The Elasticsearch output plugin sends logs directly to an Elasticsearch instance, offering a centralized solution for log management.
```
[OUTPUT]
  Name  es
  Match *
  Host  127.0.0.1
  Port  9200
  Index fluentbit
  Type  _doc
```
**2. HTTP Plugin**
For more flexibility, the HTTP plugin forwards log data to any HTTP endpoint. This is useful if you have custom endpoints or need to integrate with other systems.
```
[OUTPUT]
  Name   http
  Match  *
  Host   example.com
  Port   80
  URI    /data
  Format json
```

## Real-World Configuration Example
Consider a scenario where you need to capture Nginx logs, filter out only error messages, and send the results to Elasticsearch. The configuration below demonstrates how to set up this logging pipeline:
```
# Input section: Collect Nginx logs from the access log file
[INPUT]
  Name   tail
  Path   /var/log/nginx/access.log
  Tag    nginx.access
  Parser nginx

# Filter section: Filter only the logs that include error messages
[FILTER]
  Name  grep
  Match nginx.access
  Regex message error

# Output section: Send the filtered logs to Elasticsearch for analysis
[OUTPUT]
  Name  es
  Match *
  Host  127.0.0.1
  Port  9200
  Index fluentbit
  Type  _doc
```  
This configuration instructs Fluent Bit to continuously collect logs with the Tail plugin, process them with the Grep plugin by filtering error messages, and finally send the output to Elasticsearch using the ES plugin.