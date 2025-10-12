# Visualization in Kibana

There are three essential topics for data analysis in Kibana: **Basic Charts**, **Time Series Visualization**, and **Geospatial Visualization**.  
These techniques help transform raw Elasticsearch data into actionable insights that can drive more informed operational decisions.

---

## 1. Basic Charts

Basic charts in Kibana provide simple yet effective ways to visually represent your data.  
They are ideal for comparing metrics across different dimensions and spotting trends at a glance.

### Table Visualization
Tables organize data into rows and columns, allowing for detailed inspection and analysis.  
In software engineering, tables are commonly used to list **error logs**, **user activities**, or **server metrics**.  

**Example use case:**  
Display the number of web server requests per minute along with details such as IP addresses, response types, and status codes.

---

### Area Chart
Area charts are excellent for visualizing trends over time, with the area below the line filled to emphasize the magnitude.  
They are particularly useful for monitoring performance metrics such as **CPU and memory usage in real time**.  

**Example:**  
An area chart can show how memory utilization increases during peak hours, helping to detect when additional resources might be needed.

---

### Bar Chart
Bar charts enable easy comparison across different categories.  
They are ideal when you need to compare values such as **error rates across services** or **track the number of bugs** in various software versions.

**Example:**  
Quickly identify which version performs more reliably by comparing the number of reported issues across releases.

---

### Line Chart
Line charts are essential for tracking changes in metrics over time.  
They are particularly useful for **monitoring system uptime or application response times**.

**Example:**  
A line chart can reveal fluctuations in database query latency throughout the day, highlighting periods of high load or potential performance issues.

---

### Scatter Plot
Scatter plots are used to investigate the **relationship between two variables**.  

**Example:**  
By plotting metrics such as CPU usage against response time, you can determine if higher CPU utilization correlates with slower response times — providing valuable insights into system performance and resource allocation.

---

### Pie Chart
Pie charts visually depict proportions within a whole.  
They are beneficial for showing **how resources are distributed** across different services or departments.  

**Example:**  
A pie chart can illustrate the percentage of total disk space used by each department, offering a clear view of resource allocation.



## 2. Time Series Visualization

**Time Series Visual Builder (TSVB)** is tailored for analyzing **data trends, seasonality, and anomalies** over time.  
This tool allows you to perform complex aggregations on your metrics and is particularly useful for monitoring **server health indicators** like CPU and memory usage.

A key element in time series analysis is the **gauge visualization**, which displays a single value on a circular scale.  
This is ideal for observing performance metrics — for example, showing the **current system load as a percentage of maximum capacity**.



## 3. Geospatial Visualization

Geospatial visualization in Kibana is designed to **map data geographically**, making it exceptionally useful for examining **user distribution or server locations**.

By using a **region map**, you can visualize where your application users are located across the globe, helping to identify **key regions** and **potential areas for expansion**.

**Example:**  
A regional map may show heavy traffic from the USA and Japan while indicating normal levels in Europe — assisting in **targeted marketing** and **resource allocation**.



**Summary Table**

| Visualization Type | Purpose | Example Use Case |
|---------------------|----------|------------------|
| **Table** | Display detailed data in tabular format | View server logs or user activity |
| **Area Chart** | Show trends over time | Monitor resource utilization |
| **Bar Chart** | Compare categories | Track bugs across versions |
| **Line Chart** | Track changes over time | Monitor response times |
| **Scatter Plot** | Explore variable relationships | Correlate CPU and response time |
| **Pie Chart** | Show proportions | Visualize disk usage by department |
| **Time Series** | Analyze metrics over time | View system health trends |
| **Geospatial** | Visualize data on maps | Track user locations |


**Tip:**  
Kibana visualizations can be combined in **dashboards**, allowing you to monitor system health, performance, and user behavior — all in one place.
