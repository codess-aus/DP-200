# DP-200 Implementing an Azure Data Solution

**Cosmos DB** is a non-relational data store that allows you to query data by using one of five APIs. The Table API allows you to use OData and Language Integrated Query (LINQ) to query data. You can issue LINQ queries with .NET. The Table API is best used to migrate applications using Table Storage without needing to update the code. You should consider using the Core (SQL) API for a new application using Cosmos DB.

Cosmos DB is a non-relational data store that allows you to query data by using one of five APIs. *The Core API allows you to use SQL to query data as JavaScript Object 
Notation (JSON) documents. JSON documents allow you to work with tree-shaped data instead of rows and columns, allowing you to determine the structure of results dynamically. You can use .NET to query Cosmos DB data that uses the SQL API.* 

An Azure SQL Database account is Microsoft's Platform-as-a-Service (PaaS) offering equivalent to on-premises SQL Server. With Azure SQL Database, you do not have to manage the physical infrastructure for SQL Server. However, **Azure SQL Database is a relational database**. This means that *every row in each table must have identical columns* (or attributes). In this scenario, you need to allow varying attributes. The managed instance deployment option is useful if you have an on-premises SQL Server instance with multiple databases that must all be moved to the cloud. All databases in a managed instance deployment share the same resources. 

**Azure Table storage uses NoSQL, which allows you to store keys and attributes in a schemaless data store**. This is similar to Cosmos DB with the Table API. Each entity (row) 
can store a varying number of attributes (fields). This allows different vendors to upload products with varying attributes. You can also use .NET to query the data.

Configuring **Always Encrypted with a randomized type will encrypt the column with random generated values, preventing join operations, grouping, and indexing**.

Configuring **Always Encrypted with a deterministic type will encrypt the column and allow it to be used in join queries**. Deterministic encryption generates the same value for a given input value, allowing grouping and indexing involving this column. 

You could use **Dynamic Data Masking** (DDM) to limit data exposure to users by masking the field value, but it *does not actually encrypt the column*.

A partition key allows you to create logical partitions for data. Values that have the same partition key share the same logical partition. Partition keys improve performance by allowing data to be scaled out horizontally. 

You should specify the category as a partition key. All receipts that have the same category share the same logical partition. When you query receipts by category, you can be sure that they all are retrieved from the same partition, which improves query performance. Because 50 percent of receipts are for the 10 most popular categories, this improves performance because most queries will be performed against those receipts. 

You should specify the unique number as the row key. A row key uniquely identifies an entity. 
