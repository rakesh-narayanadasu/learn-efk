# Exploring KQL (Kibana Query Language) in Kibana

Kibana Query Language (**KQL**) integrates seamlessly with **Kibana** to query **Elasticsearch** data efficiently.  
Whether you're troubleshooting error logs or building advanced dashboards, KQL offers a **user-friendly syntax** that simplifies complex **Elasticsearch Query DSL** requests.



## What is KQL?

KQL is a vital component of Kibana, enabling you to **filter and search datasets with ease**.  
The language translates your queries into **Elasticsearch Query DSL** requests behind the scenes, ensuring you harness the full power of Elasticsearch's search capabilities while maintaining simplicity in query construction.  

Once Elasticsearch processes these queries, the matching data is immediately returned to Kibana, providing a **real-time interactive data analysis experience**.



## A Practical Look at KQL

Let’s take a closer look at how a simple KQL query is automatically converted into an Elasticsearch Query DSL request.

### Example KQL Query

```
status: "200" AND extension: "php"
```

### Equivalent Elasticsearch Query DSL

```
{
  "query": {
    "bool": {
      "must": [
        { "match": { "status": "200" }},
        { "match": { "extension": "php" }}
      ]
    }
  }
}
```

This translation **abstracts away the complexity**, allowing you to focus on constructing effective queries for your data.



## Types of Queries in KQL

### 1. Field Queries

Field queries use a straightforward syntax by specifying both **field name** and **value**.

```
status: "200"
```

Ideal for monitoring specific HTTP responses, such as identifying successful transactions.

---

### 2. Wildcard Queries

Wildcard queries enable **partial matching** using wildcard characters (`*`).

```
user: "joh*"
```

Matches any username beginning with "joh", including variations like `john123` or `john_doe`.

---

### 3. Logical Operators

KQL supports logical operators such as **AND**, **OR**, and **NOT** to combine multiple conditions.

```
status: "404" OR status: "500"
```

Retrieves records where the status is either 404 or 500, offering flexible filtering options.

---

### 4. Range Queries and Existence Checks

KQL also supports **range queries** and **existence checks** for filtering numerical values or verifying if a field exists.

```
bytes > 1000
_exists_: user_agent
```

Useful for filtering data based on file size and ensuring certain fields are present in your documents.

---

### 5. Complex Queries

You can combine multiple conditions using parentheses for advanced filtering logic.

```
(status: "200" AND extension: "php") OR (bytes > 1000 AND _exists_: user_agent)
```

Retrieves records that either:
- Match a `200` status with a `php` extension, **or**
- Have a `bytes` size greater than 1000 and an existing `user_agent` field.

---

## Advanced Capabilities: Nested Fields

KQL is robust enough to handle **complex nested JSON documents**.

### Example JSON Data

```
{
  "user": {
    "address": {
      "city": "San Francisco"
    }
  },
  "message": "User encountered an error on the login page",
  "host": "server1",
  "timestamp": "2024-06-20T12:00:00Z",
  "url": "https://example.com/user/login",
  "status": "200",
  "bytes": 1500
}
{
  "user": {
    "address": {
      "city": "San Francisco"
    }
  },
  "message": "Admin error while trying to login",
  "host": "server2",
  "timestamp": "2024-06-20T12:05:00Z",
  "url": "https://example.com/admin/login",
  "status": "200",
  "bytes": 1800
}
```

### Querying Nested Fields

```
user.address.city: "San Francisco"
```

Simplifies working with deeply nested JSON structures, allowing you to extract data without manually writing complex DSL queries.



## Summary Table

| Query Type | Example | Description |
|-------------|----------|-------------|
| **Field Query** | `status: "200"` | Filter specific field values |
| **Wildcard Query** | `user: "joh*"` | Match patterns using wildcards |
| **Logical Operators** | `status: "404" OR status: "500"` | Combine multiple conditions |
| **Range Query** | `bytes > 1000` | Filter based on numeric ranges |
| **Existence Check** | `_exists_: user_agent` | Ensure a field exists |
| **Complex Query** | `(status: "200" AND extension: "php") OR (bytes > 1000)` | Combine multiple conditions logically |
| **Nested Field Query** | `user.address.city: "San Francisco"` | Query data inside nested JSON fields |

---

**Tip:**  
KQL is designed to be intuitive — it’s case-insensitive, doesn’t require quotes for simple text values, and supports autocompletion in Kibana’s query bar for faster query building.


