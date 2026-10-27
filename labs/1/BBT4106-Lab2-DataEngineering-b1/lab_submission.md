# Lab Submission

## Team Members

1. Alvin Michael Ogola, 137694, BBIT B
2. Ethan Olowo, 152894, BBIT B
3. Tevin Njaule, 152970, BBIT B
4. Abdalla Hafsa Fuad, 152613, BBIT B
5. Kipng'etich Gideon, 148445, BBIT B

## Section 1: Deduplication Strategies

### Introduction
In modern data warehousing environments, deduplication represents one of the most critical challenges for maintaining data quality and consistency. As data flows through complex pipelines involving multiple systems, transformations, and real-time processing, the likelihood of duplicate records increases significantly. This essay examines deduplication strategies specifically within the context of data warehouses, with particular emphasis on ClickHouse implementations and their relationship to underlying storage engines.

### The Importance of Upsert Operations
The concept of "upsert" (a blend of "update" and "insert") forms the foundation of effective deduplication strategies. An upsert operation intelligently determines whether to insert a new record or update an existing one based on the presence of a matching key. This approach is particularly valuable in data warehousing scenarios where data arrives from multiple sources with varying frequencies and potential overlaps.

In traditional relational databases, upsert operations are relatively straightforward due to built-in constraints and referential integrity mechanisms. However, data warehouses often prioritize performance and scalability over transactional consistency, creating unique challenges for implementing effective upsert logic. The importance of upsert operations becomes even more pronounced in real-time data processing environments where **Change Data Capture (CDC)** systems continuously stream modifications from source systems.

Consider a scenario where customer data flows from multiple sources; web applications, mobile apps, and point-of-sale systems. Without proper upsert mechanisms, the same customer could appear multiple times in the warehouse with slightly different information, leading to inaccurate analytics and business intelligence insights. Effective upsert strategies ensure that each entity maintains a single, authoritative record while preserving the ability to track historical changes when necessary.

### Deduplication Strategies in Data Warehouses
Data warehouses employ several sophisticated deduplication strategies, each with distinct advantages and use cases. The primary approaches include replacing table engines, collapsing merge strategies, and query-time deduplication techniques.

**Replacing Table Engines** represent the most straightforward deduplication approach. These engines automatically replace duplicate records based on primary key values, maintaining only the most recent version of each record. This strategy works exceptionally well for scenarios where historical versions are not required and storage efficiency is paramount.

**Collapsing Merge Strategies** offer more sophisticated control over deduplication behavior. Unlike simple replacement, collapsing strategies can apply custom logic to determine how duplicate records should be merged. This approach enables businesses to implement complex deduplication rules, such as preserving specific field values from different versions or applying mathematical operations to numeric fields.

**Query-time Deduplication** provides the most flexible approach by maintaining all record versions in storage but applying deduplication logic during query execution. This strategy preserves complete data lineage while allowing different deduplication rules for different analytical use cases.

### ClickHouse Engine Integration
ClickHouse's deduplication capabilities are intimately tied to its underlying table engines, each designed for specific use cases and performance characteristics. The relationship between deduplication strategies and storage engines is crucial for implementing effective data warehouse solutions.

**ReplacingMergeTree Engine** serves as the primary deduplication engine in ClickHouse. This engine automatically identifies and removes duplicate records based on the specified sorting key during background merge operations. The ReplacingMergeTree engine is particularly effective for scenarios requiring automatic deduplication with minimal query overhead.

**CollapsingMergeTree Engine** provides advanced deduplication capabilities through sign-based record collapsing. This engine uses a special "sign" column to determine whether records should be added or subtracted during merge operations. When records with opposite signs are merged, they cancel each other out, effectively removing duplicates while maintaining audit trails.

**VersionedCollapsingMergeTree Engine** extends the collapsing concept by adding version-based ordering. This engine ensures that only the latest version of each record remains after merge operations, making it ideal for CDC scenarios where record versions are clearly defined.

**SummingMergeTree Engine** offers specialized deduplication for aggregated data. Rather than simply removing duplicates, this engine sums numeric columns for records with identical keys, making it perfect for pre-aggregated metrics and summary tables.

### Query Modifications for Deduplication
ClickHouse provides several query-level mechanisms to retrieve deduplicated data, regardless of the underlying storage engine. These techniques are essential for ensuring consistent results across different deduplication strategies.

The `FINAL` Modifier represents the most commonly used query-time deduplication technique. When applied to `SELECT` statements, `FINAL` forces ClickHouse to return only the most recent version of each record, effectively deduplicating results at query time. For example:

```sql
SELECT * FROM customers FINAL ORDER BY customerNumber;
```
This query returns only the latest version of each customer record, filtering out historical duplicates that may exist in the underlying storage.

`OPTIMIZE TABLE` Operations provide manual control over deduplication timing. By executing `OPTIMIZE TABLE` commands, administrators can force immediate merge operations, ensuring that deduplication rules are applied without waiting for background processes.

**Custom Deduplication Logic** can be implemented using window functions and conditional expressions. This approach allows for sophisticated deduplication rules that go beyond simple key-based matching, enabling businesses to implement domain-specific deduplication logic.

### Practical Implementation Examples
Consider a retail analytics scenario where customer purchase data flows through a CDC pipeline. The source system occasionally sends duplicate records due to network retries or system failures. Implementing a VersionedCollapsingMergeTree table with appropriate version columns ensures that only the latest version of each transaction remains in the warehouse.

Another example involves financial data where transaction amounts might be corrected after initial processing. Using a CollapsingMergeTree engine with sign-based collapsing allows the system to effectively "cancel out" incorrect transactions while maintaining complete audit trails.

For high-volume streaming scenarios, ReplacingMergeTree engines provide optimal performance by automatically handling deduplication during background merge operations, eliminating the need for complex query-time logic.

### Conclusion
Effective deduplication strategies are fundamental to maintaining data quality in modern data warehouses. The choice of deduplication approach must align with specific business requirements, performance constraints, and data characteristics. ClickHouse's engine-specific deduplication capabilities provide powerful tools for implementing sophisticated deduplication logic while maintaining the performance and scalability required for enterprise-scale analytics.

Understanding the relationship between deduplication strategies and storage engines enables data engineers to design robust pipelines that maintain data integrity while supporting high-performance analytical workloads. As data volumes continue to grow and real-time processing becomes increasingly critical, mastering these deduplication techniques becomes essential for successful data warehouse implementations.


## Section 2: Additional Data Ingestion

Ingest more data into the following:

1. Fact table: `orderDetails`

2. Dimension table: `products`

![Star Schema](container-volumes/clickhouse/StarSchema2.png)

**Part A:** Add code for creating the additional fact and dimension tables in ClickHouse. The code should be added here: [container-volumes/clickhouse/ClickHouseTables.sql](container-volumes/clickhouse/ClickHouseTables.sql)

**Part B:** Update the Kafka source connector to support this ingestion using a Change Data Capture source connector. The updated code should be placed here: [kafka-connector-configs/submit_source-mysql-classicmodels-00_config.sh](kafka-connector-configs/submit_source-mysql-classicmodels-00_config.sh)

**Part C:** Add sink connectors to support the ingestion. There should be 3 sink connectors to insert, update, and delete into `orderDetails` and 3 sink connectors to insert, update, and delete into `products`. Place the 6 sink connectors in the `kafka-connector-configs` folder.

**Part D:** Provide screenshots below to show that the data pipeline has been created and the ingestion is successful.
