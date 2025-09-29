# Documents in Elasticsearch

Elasticsearch stores all information in the form of **documents**. These documents are the fundamental data unit, structured in **JSON format** and optimized for rapid, full-text search.

## Key Features of Documents in Elasticsearch

### JSON Format
- Documents are stored in a lightweight JSON format.
- Human-readable and machine-parsable.
- Supports complex nested structures.
- Capable of representing:
  - Numbers
  - Strings
  - Dates
  - Arrays
  - Embedded objects

### Indexing
- Indexing is the process of storing documents to facilitate quick search operations.
- During indexing:
  - JSON data is converted into an **inverted index**.
  - This structure enables **fast full-text search**.

### Nodes and Clusters
- A **node** is a single instance of Elasticsearch.
  - Stores data.
  - Participates in indexing and search operations.
- A **cluster** is a group of nodes working together.
  - Distributes data and queries.
  - Enhances performance and reliability.
- Nodes can have different roles:
  - Master
  - Data
  - Client (Coordinating)

### Sharding and Replicas
- Large datasets are split into **shards**.
  - Each shard is a self-contained index.
  - Shards can be distributed across nodes for **parallel query processing**.
- **Replicas** provide:
  - **Redundancy** (fault tolerance).
  - **Faster search** due to query load balancing.

### Schema-Less Flexibility
- Elasticsearch can operate without a predefined schema.
- Automatically detects and adds new fields.
- Ideal for **agile environments** with evolving data structures.
- Optionally, mappings can be defined to enforce structure.

---

## How a Log File is Stored as a Document

When a log file is ingested:

- Elasticsearch transforms it into a document.
- Adds metadata for efficient storage and retrieval.

### Common Metadata Includes:
- A designated **index name** (e.g., `webserver_logs`).
- A **type identifier** (commonly `_doc`).
- A unique **document ID**.
- A **score** representing relevance in search queries.
- The actual log data in the `_source` field.

### Example: Transformed Log File

```json
{
  "_index": "webserver_logs",
  "_type": "_doc",
  "_id": "DD46948BFqy1faFsINf8",
  "_score": 0.2876821,
  "_source": {
    "timestamp": "2024-02-28T10:35:12+0000",
    "ip": "192.168.1.100",
    "method": "GET",
    "url": "/images/logo.png",
    "status": 200,
    "bytes": 2326,
    "referer": "https://www.example.com/",
    "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) ..."
  }
}
```
### Breakdown of the Example

- **_index**: Groups related log entries (e.g., `webserver_logs`).
- **_type**: Identifies the document type (usually `_doc`).
- **_id**: Uniquely identifies the document.
- **_score**: Indicates the document's relevance during search operations.
- **_source**: Contains the actual log data extracted from the ingested file.
