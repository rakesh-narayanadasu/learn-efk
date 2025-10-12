# CRUD operations on Elasticsearch

CRUD represents the core operations you’ll perform when managing data in Elasticsearch, whether you’re working with databases or search engines. Below is a breakdown of each operation:

## Create:
Add new documents to an index. When a document is created, you provide its data fields and corresponding values. Elasticsearch then indexes this data, making it readily searchable.

```json
POST /products/_doc/1
{
  "name": "Wireless Headphones",
  "brand": "SoundMax",
  "price": 129.99,
  "in_stock": true
}
```

## Read:
Retrieve or search for documents within an index. Elasticsearch’s robust search functionality allows you to query data using various criteria, ensuring you get accurate results.

```json
GET /products/_search
{
  "query": {
    "match": { "brand": "SoundMax" }
  }
}
```

## Update:
Modify existing documents in an index. This operation enables you to adjust field values, introduce new fields, or update multiple records at once. Updated documents are **re-indexed** to maintain search precision.

```json
POST /products/_update/1
{
  "doc": {
    "price": 119.99,
    "in_stock": false
  }
}
```

## Delete:
Remove documents from an index. You can delete individual records or perform bulk deletions based on specific criteria.

```json
DELETE /products/_doc/1
```

## The Importance of CRUD Operations
Mastering CRUD operations in Elasticsearch is crucial for:

**Ingesting Fresh Data:** Quickly index new information into your system.

**Efficient Data Retrieval:** Leverage powerful search capabilities to fetch desired records.

**Seamless Data Updates:** Keep your indexed data current with minimal downtime.

**Data Cleanup:** Remove outdated or irrelevant records to maintain optimal performance.

> Furthermore, you can perform **cluster-wide operations** by making `GET` calls to Elasticsearch, expanding your management capabilities.

**Summary Table**

| Operation | Method | Endpoint Example | Description |
|------------|---------|------------------|--------------|
| **Create** | `POST` | `/index/_doc/{id}` | Adds new documents |
| **Read** | `GET` | `/index/_search` | Retrieves documents |
| **Update** | `POST` or `PUT` | `/index/_update/{id}` | Modifies existing documents |
| **Delete** | `DELETE` | `/index/_doc/{id}` | Removes documents |

---

**Tip:**  
When working with large datasets, consider using **bulk APIs** in Elasticsearch to perform multiple CRUD operations in a single request for improved efficiency.



# Searching All Documents

To retrieve all documents from Elasticsearch, run the following command:

```json
GET _search
{
  "query": {
    "match_all": {}
  }
}
```
## Checking Cluster Health
Before executing any modifications, it is advisable to verify the health of your Elasticsearch cluster.

Run this GET request to check the cluster's status:
```json
GET /_cluster/health
```

A successful response (HTTP status 200) returns details similar to the example below:

```json
{
  "cluster_name": "elasticsearch",
  "status": "yellow",
  "timed_out": false,
  "number_of_nodes": 1,
  "number_of_data_nodes": 1,
  "active_primary_shards": 10,
  "active_shards": 10,
  "relocating_shards": 0,
  "initializing_shards": 0,
  "unassigned_shards": 2,
  "delayed_unassigned_shards": 0,
  "number_of_pending_tasks": 0,
  "number_of_in_flight_fetch": 0,
  "task_max_waiting_in_queue_millis": 0,
  "active_shards_percent_as_number": 83.33333333333334
}
```

> Note: The response status will typically be yellow or green. A red status indicates critical issues that require immediate attention.

## Creating an Index
To create a new index named "products", execute the following PUT command:
```json
PUT /products
```
On successful execution, you will receive an acknowledgement confirming the creation of the "products" index.

## Adding a Document
Insert a new document into the "products" index using the POST command. The example below adds a product document with multiple properties:
```json
POST /products/_doc/1
{
  "product_id": 67890,
  "name": "Cozy Winter Sweater",
  "description": "Soft and stylish sweater for cold days",
  "price": 59.99,
  "category": "Apparel",
  "brand": "Trendy Threads"
}
```

## Retrieving the Document
To confirm that the document has been added, retrieve it with the following GET command:
```json
GET /products/_doc/1
```
You can also search for the document by matching specific fields. For example, to find a product with "sweater" in its name, use:
```json
GET /products/_search
{
  "query": {
    "match": {
      "name": "sweater"
    }
  }
}
```
In the response, note that the document data is stored under the `_source` key, while other keys hold metadata.

## Updating a Document
### Incorrect Approach Using PUT
Attempting to update a document using the PUT command may result in issues, as it replaces the entire document rather than updating specific fields. For example:
```json
PUT /products/_doc/1
{
  "price": 129.99
}
```
This approach can trigger a parsing exception (HTTP status 400) if not formatted correctly.

### Correct Approach Using POST with _update
To modify only specific fields without replacing the entire document, use the POST command with the `_update` endpoint. First, ensure your document exists:
```json
POST /products/_doc/1
{
  "product_id": 67890,
  "name": "Cozy Winter Sweater",
  "description": "Soft and stylish sweater for cold days",
  "price": 59.99,
  "category": "Apparel",
  "brand": "Trendy Threads"
}
```
Now, update specific fields using:
```json
POST /products/_doc/1/_update
{
  "doc": {
    "description": "Soft and stylish sweater for cold days. Available in multiple colors.",
    "category": "Apparel - Seasonal"
  }
}
```
After executing this update command, verify the changes by retrieving the document again:
```json
GET /products/_doc/1
```

> Using PUT replaces the whole document, whereas using POST with _update only modifies the designated fields.

## Deleting Documents and Indices
To delete a single document from the index:
```json
DELETE /products/_doc/1
```
If you prefer to delete the entire index, execute:
```json
DELETE /products/
```

## Below is a consolidated list of essential Elasticsearch CRUD commands:

```json
GET _search
{
  "query": {
    "match_all": {}
  }
}


GET /_cluster/health


PUT /products


POST /products/_doc/1
{
  "product_id": 67890,
  "name": "Cozy Winter Sweater",
  "description": "Soft and stylish sweater for cold days",
  "price": 59.99,
  "category": "Apparel",
  "brand": "Trendy Threads"
}


GET /products/_doc/1


GET /products/_search
{
  "query": {
    "match": {
      "name": "sweater"
    }
  }
}


POST /products/_doc/1/_update
{
  "doc": {
    "description": "Soft and stylish sweater for cold days. Available in multiple colors.",
    "category": "Apparel - Seasonal"
  }
}


DELETE /products/_doc/1


DELETE /products/
```