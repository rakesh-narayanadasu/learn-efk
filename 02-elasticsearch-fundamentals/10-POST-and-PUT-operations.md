# Difference between POST and PUT operations

Elasticsearch supports both PUT and POST operations, each suited to different use cases:

- **PUT Operation:**
The PUT method is designed to create a new document or completely replace an existing one. It requires you to explicitly specify the document ID. If a document with that specific ID already exists, it will be entirely overwritten.

- **POST Operation:**
The POST method can be used to create new documents without specifying a document ID, as Elasticsearch will automatically generate one for you. Moreover, POST is commonly used for partial updates to an existing document, making it more flexible compared to PUT.

## Demonstration
Follow these steps to see the practical differences between PUT and POST in action.

### 1. Checking Cluster Health
Before making any modifications, verify the health of your Elasticsearch cluster:
```
GET _cluster/health
```
When you run this command in the developer tool, you should receive a status code of 200 and see that the cluster status is "yellow," which is perfectly acceptable.

### 2. Creating an Index with PUT
Create an index called "school" using the PUT method:
```
PUT /school
```
A successful acknowledgment in the response indicates that the index has been created.

### 3. Inserting Documents Using PUT
Since PUT requires an explicit document ID, insert a document with a specified ID. For example, to add a document with ID 1:
```
PUT /school/_doc/1
{
  "name": "Alice",
  "grade": 12,
  "subject": "Mathematics"
}
```
After the insertion, retrieve the document to verify its contents:
```
GET /school/_doc/1
```

### 4. Creating a Document Using POST
If you prefer Elasticsearch to generate the document ID automatically, use the POST method:
```
POST /school/_doc
{
  "name": "Bob",
  "grade": 10,
  "subject": "History"
}
```
Elasticsearch will return a response with an auto-generated ID. You can use this ID to fetch the document:
```
GET /school/_doc/{auto-generated-id}
```
Remember to replace `{auto-generated-id}` with the actual ID returned in the response.

### 5. Updating a Document
For updating an existing document—for instance, changing the grade for the document with ID 1—use the update API with a POST request:
```
POST /school/_doc/1/_update
{
  "doc": {
    "grade": 11
  }
}
```
Afterward, retrieve the document to confirm the update:
```
GET /school/_doc/1
```

### 6. Retrieving Document IDs
To list all document IDs in the "school" index without retrieving the full document details, execute the following search query:
```
GET /school/_search
{
  "_source": false,
  "query": {
    "match_all": {}
  },
  "fields": ["_id"]
}
```
If you want to view every detail stored in the index, modify the query by setting `_source: true`:

```
GET /school/_search
{
  "_source": true,
  "query": {
    "match_all": {}
  },
  "fields": ["_id"]
}
```

**Note**

When using POST to create documents, executing the POST command multiple times will insert new records each time, **potentially leading to duplicate entries**. In contrast, using PUT with the same document ID **replaces the existing document**.

For example:

```
POST /school/_doc
{
  "name": "Bob",
  "grade": 10,
  "subject": "History"
}


POST /school/_doc/1/_update
{
  "doc": {
    "grade": 11
  }
}


GET /school/_doc/1


GET /school/_search
{
  "_source": true,
  "query": {
    "match_all": {}
  },
  "fields": ["_id"]
}
```

**Choose the method that aligns with your use case:**

Use POST when you want Elasticsearch to handle ID generation and support partial updates, and use PUT when you need to explicitly define the document ID and guarantee document replacement.

The essential differences between POST and PUT in Elasticsearch are:

- **PUT:**

    - Requires an explicitly defined document ID.
    - Completely replaces the document if it already exists.
- **POST:**

    - Automatically generates a document ID when one is not provided.
    - Supports partial updates, but repeated POST requests can lead to duplicate documents.