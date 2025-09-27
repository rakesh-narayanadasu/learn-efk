# Fundamentals of Elasticsearch

## Cluster Architecture

An Elasticsearch cluster is a collection of one or more nodes that work together to store data and deliver high-performance indexing and search capabilities. Clusters enhance scalability by adding more nodes, which increases both storage capacity and search throughput.

Data within Elasticsearch is stored as JSON documents, with each document acting as an individual searchable unit. These documents are organized into **indices**, similar to tables in traditional SQL databases.

## Indexing and Searching

**Indexing** involves storing documents in Elasticsearch to enable rapid retrieval. When a document is indexed, Elasticsearch creates an **inverted index** that facilitates fast, full-text search operations. Leveraging the robust **Lucene** search library, Elasticsearch ensures that searches are both efficient and scalable.

Elasticsearch supports a variety of query types, including:

- **Term queries**
- **Match queries**
- **Boolean queries**

To handle large datasets, each index is divided into **shards**. Each shard functions as an independent index that can reside on any node in the cluster. Additionally, **replicas** (copies of shards) are maintained to ensure high availability and enhanced fault tolerance.

## Mapping

**Mapping** in Elasticsearch serves a similar purpose as a schema in traditional databases. It defines how documents and their fields are stored, indexed, and analyzed. Through proper mapping, you can:

- Specify data types,
- Determine how fields are processed during storage and retrieval.

## CRUD Operations

Elasticsearch offers robust support for **CRUD** (Create, Read, Update, and Delete) operations, making it easy to manage documents within your cluster. These operations are fundamental for:

- Inserting new data,
- Retrieving existing information,
- Modifying records,
- Removing documents as needed.
