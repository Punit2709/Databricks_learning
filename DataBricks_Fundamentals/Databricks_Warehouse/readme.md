# SQL WAREHOUSE

What is SQL-Warehouse ?
- A SQL warehouse is a compute resource that lets you query and explore data on Databricks.
- Just like cluster but it made for sql queries
- When a notebook is attached to a SQL warehouse, you can run SQL and Markdown cells. Running a cell in any other language (such as Python or R) throws an error.

Sure! Here's a clean comparison of the **Databricks SQL warehouse types** in a single table:

| Feature / Type                  | **Serverless SQL Warehouse**         | **Pro (Classic) SQL Warehouse**     | **Multi-Cluster (High Concurrency)** |
|----------------------------------|--------------------------------------|-------------------------------------|---------------------------------------|
| **Startup Time**                | ⚡ Fast (seconds)                     | 🕒 Slower (minutes)                 | 🕒 Slower (minutes)                   |
| **Scaling**                     | Auto-scales compute & concurrency    | Manual or optional auto-scaling     | Auto-scales across clusters           |
| **Compute Management**         | Fully managed by Databricks          | User-managed                        | Partially managed                     |
| **Concurrency**                | High                                  | Medium                              | Very High                             |
| **Billing Granularity**        | Per second                            | Per DBU/hour                        | Per DBU/hour                          |
| **Cost Efficiency**            | Great for short, bursty workloads     | Better for long-running jobs        | Higher due to multiple clusters       |
| **Use Case**                   | Ad-hoc queries, dashboards, BI tools  | Scheduled jobs, ETL                 | Heavy BI usage, lots of users         |
| **Availability**               | Limited to certain regions/plans     | Widely available                    | Widely available                      |
