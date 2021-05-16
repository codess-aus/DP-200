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

You cannot query data by using Gremlin API. The --kind parameter of the az cosmosdb create command specifies the API used by the Cosmos DB account. The value GlobalDocumentDB means that the account uses the Core API. 

A client cannot see partial writes of a sales data record by default. This is because the account uses a strong consistency level, as indicated by the --default-consistency-level parameter. With a strong consistency level, reads are guaranteed to return the most recently committed version of a data record. 

A client can set the consistency level to Eventual Consistency at connection time. This allows the client to specify a consistency level different from the default. Eventual consistency is the weakest consistency level. It means that data reads and writes in a distributed system will be in sync eventually. 

A client can set a different consistency level during each request to sales data. This allows the client to specify a consistency level different from the default level depending on the type of request being made. 

With the session consistency level, the same user is guaranteed to read the same value within a single session. Even before replication occurs, the user that writes the data can read the same value. 

Only the same user within the same session is guaranteed to read the same value within a single session. This is because the data has not yet replicated.

File permissions consist of three digits: Owner (The user who created the item automatically becomes an Owner), Owner Group, and Everyone Else. In Azure Data Lake Storage Gen2, the Owner Group is inherited from the parent folder. 

Azure Data Lake Storage Gen2 supports settings ACLs in the POSIX-compatible format, which assigns the following numbers to the different permission combinations: 

* Read Only: 4 
* Write Only: 2 
* Execute Only: 1 
* No Access: O 
* read + write: 4 + 2 = 6 
* Read + Execute: 4 + 1 = 5 

The 640 permission set to the text file created by Kerry can be translated as: 
• Owner (Kerry): Read + Write (6) 
• Owner Group (Finance, which includes David): Read Only (4) 
• Everyone Else (Alan): No Access (O) 

With the **strong consistency level**, reads are guaranteed to return the most **committed version** of an item. Even if Employee A is the user that changed the attribute, that employee still reads the original value until the item is committed and synchronization takes place. Therefore, Employee A, Employee B, and Employee C all read Pending until the item is committed and synchronization takes place.

You should choose the **Core (SQL) API**. This API is recommended because it supports a *schema-less data store*. In this scenario, different types of products can have different attributes. This is indicated by the fact that not all columns in the existing database are used. Some products can have different columns populated. This is referred to as semi-structured data. This API allows you to use SQL-like queries to access and filter data. The data is returned as JavaScript Object Notation (JSON) documents. 

You should not use the Gremlin API. This API does not support SQL-like queries. This API uses the Gremlin Graph Traversal Language to query data from a graph database. 

You should not use the Table API. This API allows you to query data by using OData and Language Integrated Query (LINQ). It does not support SQL-like queries from web applications. 

You should not use the MongoDB API. This API does not allow you to use SQL-like queries to access and filter data.

You should use Gremlin API because it is based on the Apache TinkerPop graph database standard and meets the solution's requirements. 



