# Mapping in Elasticsearch

## What Is Mapping in Elasticsearch?

**Mapping** in Elasticsearch is the process of defining how documents and their individual **fields are stored, indexed, and analyzed**. It plays a critical role in determining how data can be searched and retrieved within your Elasticsearch cluster.


## Types of Mapping

There are two primary approaches to mapping in Elasticsearch:


### 1. Dynamic Mapping

- **Description**: Elasticsearch automatically detects new fields in incoming documents and adds them to the index mapping.
- **Key Benefit**: Reduces manual configuration, making it easier to handle unstructured or changing data.
- **Ideal For**: 
  - Evolving schemas
  - Logs or documents with unknown fields
  - Rapid development environments

---

### 2. Explicit Mapping

- **Description**: Fields and their data types are manually defined before indexing documents.
- **Key Benefit**: Provides precision and optimization for search and storage.
- **Ideal For**: 
  - Applications requiring performance tuning
  - Strict data models
  - Known and consistent field structures



## Comparison: Dynamic vs. Explicit Mapping

| Mapping Type     | Description                                                  | Use Case                                                    |
|------------------|--------------------------------------------------------------|-------------------------------------------------------------|
| **Dynamic Mapping**  | Automatically detects and indexes new fields dynamically     | Best for unstructured data or evolving schemas              |
| **Explicit Mapping** | Manual definition of each field’s type and indexing method | Best for strict search performance and precise configurations |



## Summary

- **Dynamic Mapping** offers flexibility and convenience, especially for unstructured or rapidly changing data sources.
- **Explicit Mapping** gives you control over field behavior, enabling high-performance querying and tailored data handling.

> Choosing the right mapping strategy depends on your data structure, application needs, and performance requirements.

---
# Dynamic and Explicit Mapping in Elasticsearch

In this, we will dive into the two primary mapping strategies in Elasticsearch: **dynamic mapping** and **explicit mapping**.


## Dynamic Mapping

Dynamic mapping allows Elasticsearch to **automatically detect and assign data types** as new documents are ingested.  
This feature enables you to deploy data without predefined schemas, as Elasticsearch intelligently infers the data types for each field.

### Example JSON Document

```json
{
  "product_id": "12345",
  "name": "Awesome Sneakers",
  "description": "The most comfortable shoes ever!",
  "price": 99.99,
  "in_stock": true,
  "release_date": "2023-12-15"
}
```

When this document is indexed with **dynamic mapping** enabled, Elasticsearch may generate a mapping similar to this:

```json
{
  "mappings": {
    "_doc": {
      "properties": {
        "product_id": { "type": "long" },
        "name": { "type": "text" },
        "description": { "type": "text" },
        "price": { "type": "float" },
        "in_stock": { "type": "boolean" },
        "release_date": { "type": "date" }
      }
    }
  }
}
```

In this process, Elasticsearch infers that:
- The `product_id` is best stored as a `long`.
- The `price` as a `float`.
- The `release_date` as a `date`, etc.

This **schema-less approach** offers rapid development by removing the need for explicit schema definitions.

> **Note:**  
> Dynamic mapping is ideal for rapid prototyping and agile development since it seamlessly handles changes and automatically adjusts to new data structures.

### Benefits of Dynamic Mapping

- **Automatic Detection:** New fields are automatically recognized and assigned appropriate data types (e.g., string, number, date, boolean).  
- **Real-Time Updates:** The index mapping is updated on the fly, enabling immediate queries on newly added fields.  
- **Data Type Inference:** Elasticsearch employs intelligent algorithms to determine the correct data type, ensuring optimal indexing and query speed.  
- **Evolving Schemas:** As your data evolves, Elasticsearch adapts without requiring manual intervention.  



## Explicit Mapping

While dynamic mapping offers excellent flexibility, there are scenarios where **precise control** over data indexing is necessary.  
**Explicit mapping** provides this control by allowing you to define the schema before inserting any data, ensuring that each field is mapped exactly as intended.

### Example Explicit Mapping

```json
PUT /product_index
{
  "mappings": {
    "_doc": {
      "properties": {
        "product_id": { "type": "keyword" },
        "name": {
          "type": "text",
          "analyzer": "english"
        },
        "description": { "type": "text" },
        "price": { "type": "float" },
        "in_stock": { "type": "boolean" },
        "release_date": {
          "type": "date",
          "format": "yyyy-MM-dd"
        }
      }
    }
  }
}
```

### Key Aspects of This Mapping

- The **`product_id`** field is set as a `keyword` to ensure exact matching.  
- The **`name`** field utilizes the **English analyzer** to enhance search relevancy.  
- The **`release_date`** field is precisely defined as a `date` following the `yyyy-MM-dd` format.  

Once the mapping is created, you can index documents that match this schema:

```json
{
  "product_id": "12345",
  "name": "Awesome Sneakers",
  "description": "The most comfortable shoes ever!",
  "price": 99.99,
  "in_stock": true,
  "release_date": "2023-12-15"
}
```


### Advantages of Explicit Mapping

- **Control and Precision:** Complete control over field storage and indexing, which can enhance search performance.  
- **Accurate Data Types:** Manually defining data types reduces the risk of type inference errors.  
- **Customized Analyzers:** Tailor text analyzers to meet your specific search and relevancy requirements.  
- **Schema Evolution Management:** Updates must be made manually, ensuring consistency and accuracy as your data evolves.  

> **Note:**  
> Dynamic mapping is typically the default approach, particularly when setting up a new Elasticsearch cluster.  
> As your application scales and demands more refined search capabilities, transitioning to explicit mapping can significantly improve search accuracy and performance.


**Summary**

| Mapping Type     | Flexibility | Control | Best For |
|------------------|-------------|----------|-----------|
| **Dynamic Mapping** | High | Low | Rapid prototyping, evolving data |
| **Explicit Mapping** | Moderate | High | Production systems, precise indexing |

---
