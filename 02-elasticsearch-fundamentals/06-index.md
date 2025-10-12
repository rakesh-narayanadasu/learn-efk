# Index in Elasticsearch

For example, logs from a web application might be stored in an index called ```web_app_logs```. Similarly, a separate index named ```login_app_logs``` could house logs from a Login App microservice. This clear segregation ensures that data from various sources is managed efficiently, simplifying search operations and maintenance. When documents are stored, Elasticsearch leverages its inverted index structure to guarantee rapid search performance, a key benefit for real-time data querying.

## Logical Container

An index functions as a logical container, similar to how a database serves in SQL systems. It comprises a collection of documents that share common attributes. For instance, a library catalog might have separate indices for books, magazines, and digital media, which simplifies data management and querying.

## Documents

Within an index, each document is the fundamental unit of information, typically stored in JSON format. Documents can include multiple fields—ranging from basic details like schema definitions to various metadata. One of Elasticsearch’s strengths is the default ability to index every field, which enhances its advanced search capabilities.

## Schema Flexibility

Documents within an index do not necessarily need to follow a strict schema, which adds considerable versatility. This feature is especially useful in scenarios such as a Login App where log fields may change over time. While Elasticsearch supports schema flexibility, it also provides mechanisms to enforce specific schemas when required.

## Summary

Each index in Elasticsearch serves as a container for documents that share similar characteristics. This design not only optimizes search performance by utilizing an inverted index structure but also provides the flexibility to adapt to varying data schemas.
