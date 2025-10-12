# Cluster Information Elasticsearch CRUD Commands

Lets explore several REST API commands that allow you to fetch essential cluster information and metadata from your Elasticsearch deployment. These commands are invaluable for monitoring, debugging, and managing Elasticsearch indices, shards, disk usage, and more.

## Retrieving Cluster Details
Start by checking the overall health of your Elasticsearch cluster. The following GET command provides a snapshot of cluster status:
```
GET /_cluster/health
```
A typical successful response is shown in the JSON snippet below:

```
{
  "cluster_name": "elasticsearch",
  "status": "yellow",
  "timed_out": false,
  "number_of_nodes": 1,
  "number_of_data_nodes": 1,
  "active_primary_shards": 11,
  "active_shards": 11,
  "relocating_shards": 0,
  "initializing_shards": 0,
  "unassigned_shards": 3,
  "delayed_unassigned_shards": 0,
  "number_of_opening_tasks": 0,
  "number_of_in_flight_fetch": 0,
  "task_max_waiting_in_queue_millis": 0,
  "active_shards_percent_as_number": 78.57142857142857
}
```

For additional metadata about your cluster, such as statistics and configuration settings, execute the following commands in your development tool:

```
GET /_cluster/health
GET /_cluster/stats
GET /_cluster/settings
GET /_cat/indices
```

These commands return detailed information about the cluster's health, metrics, configuration settings, and a list of all indices with their current statuses. For example, while a GeoIP index might be marked as green (healthy), another index like a school index could be yellow.

## Creating and Querying an Index
In this section, you'll learn how to create an index and add a document to inspect index-specific configurations and statistics.

### Step 1: Create the "products" Index
Create an index named "products" by running:
```
PUT /products
```

### Step 2: Insert a Document
Add a sample document to the "products" index with the following POST request:
```
POST /products/_doc/1
{
  "product_id": 67890,
  "name": "Cozy Winter Sweater",
  "description": "Soft and stylish sweater for cold days.",
  "price": 59.99,
  "category": "Apparel",
  "brand": "Trendly Threads"
}
```

### Step 3: Verify the Document
To ensure the document has been stored correctly, retrieve it using:
```
GET /products/_doc/1
```
### Step 4: Check Index Settings and Statistics
Inspect the index’s settings (like the number of shards and replicas) and detailed statistics by executing:
```
GET /products/_settings
GET /products/_stats
```

## Updating Index Settings
If you need to adjust dynamic settings for an index (for example, increasing the number of replicas), use a PUT request. The following command updates the dynamic setting for the "products" index:
```
PUT /products/_settings
{
  "index.number_of_replicas": 2
}
```

These Elasticsearch CRUD commands and REST API endpoints are essential tools for administering and troubleshooting your Elasticsearch cluster in both testing and production environments.