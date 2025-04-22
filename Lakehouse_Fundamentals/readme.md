# Data LakeHosue Architecture

- Before we learn data lake house architecture we nee to leanr following things

    ### Why Diff Architercture ?
    - we require data management

    ### Why Data Management ?
    - for analytical process
    - to feed data to AI
    - to train business model

    ### There are diff type of architecture
    - OLTP System
    - OLAP System
    - DataWare House
    - Data Lake
    - Data Lake House

## Data Warehouse
- Before dataware hosue companies are using DBMS which are not good for analytical processing.
- So we require some architecture which can can make data retrival faster
- Dataware house store data such that data retrival become more faster than DBMS
- For this it is using storage formate like parquet etc...

    ### Evolution of Data Warehousing
    1. The Problem: Data Silos
    Before centralized systems, companies struggled with data silos—decentralized and fragmented stores of data scattered across departments. This made it difficult to access and unify information for decision-making.

    2. The Solution: Data Warehouses
    To address this, data warehouses were introduced in the late 1980s. They provided an architectural model for transferring structured data from operational systems into decision-support environments. Early versions were on-premises, relying on company-managed hardware.

    3. The Shift to Cloud Warehousing
    By the early 2010s, a shift began toward cloud-based data warehouses. Major cloud providers like Amazon, Google, and Microsoft started offering hosted solutions. This transition brought several key advantages:

            Lower upfront costs (OpEx vs. CapEx)

            Faster setup and deployment

            Greater scalability

            Global accessibility

    4. Limitations of Traditional Warehouses
    Despite their usefulness, traditional data warehouses struggled with:

        Handling massive data volumes

        Managing unstructured data efficiently These limitations pushed organizations to seek more modern, flexible data management (DM) solutions.

    5. The Modern Data Management Era
    Today’s solutions go beyond just structured data. They can store, manage, and govern a variety of data formats, addressing both structured and unstructured data needs—offering speed, scalability, and flexibility.
<br><br>

# Query Caching in Databricks DWH

- reduce time to recalculate
- no need to fetch same data multiple time 
- reduce compute usage
- speed up execution task

    ![types-of-caching](https://docs.databricks.com/aws/en/assets/images/query-cache-1fbc56f8427dfea88a949ec7441fdabd.png)

### Types of caching
1. UI Cache
2. Local Cache
3. Remote Cache
4. Disk Cache

    
## Databricks SQL UI cache
 The Databricks SQL UI cache displays **the most recent query result**, including the results from **scheduled executions**.

 The Databricks SQL UI cache has at most a **7-day life cycle**. 
 
 The cache is located within your **Databricks filesystem** in your account.
 
 When u re-run query then u lost the result.
 
 In Databricks SQL with Delta Lake, any UPDATE, DELETE, or MERGE operation on a cached Delta table triggers automatic cache invalidation.

## Result Cache in Databricks SQL

**Result cache** enables per-cluster caching of query results for all queries executed through SQL warehouses. It includes both **local** and **remote** result caches, which together help improve query performance by storing query results either in memory or in remote storage.


### 🔹 Local Cache

- **In-memory cache** tied to the lifetime of the cluster.
- Stores query results until:
  - The cache is full, or
  - The cluster is stopped or restarted.
- Benefits:
  - Speeds up repetitive queries.
  - Avoids recomputation of previously computed results.
- **Note**: Once the cluster restarts, all local cached results are cleared.


### 🔹 Remote Result Cache

- A **serverless-only** persistent cache system.
- Stores query results as **workspace system data**.
- **Persists through** warehouse stop/restart operations.
- Shared across **all SQL warehouses** in the workspace.
- Addresses limitations of in-memory caching that depends on cluster uptime.
- Access requires a **running warehouse**.

---

### 🛠 Cache Lookup Order

1. **Local cache** is checked first.
2. If not found, **remote result cache** is checked.
3. If still not found, the query is executed and the result is cached.


### 📅 Cache Lifecycle

- Both **local** and **remote** result caches:
  - Have a **24-hour lifecycle** from the time of cache entry.
- Both caches are **automatically invalidated** when:
  - The **underlying tables are updated**.



> 💡 Tip: Use result caching to optimize performance for repeated, read-heavy queries—especially in BI dashboards and reports.

## Disk Cache

**Disk cache** in Databricks SQL is a local SSD-based caching system used to speed up data reads from storage during query execution. It works by storing copies of data files on the local disks attached to the compute nodes.

- Disk cache is automatically used when files are fetched for the first time.
- It uses a fast intermediate format to store data efficiently.
- The cached data is stored locally on SSDs, which are much faster than reading from remote cloud storage like S3 or ADLS.
- By keeping data close to the workers, disk caching significantly improves query performance.
- Unlike result caching (which caches query outputs), disk cache works at the **file level**, making it ideal for repeated reads of the same data.
- It is especially helpful for large datasets and frequently accessed tables.