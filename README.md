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

Eventual consistency level. This is the lowest consistency level available and will result in as little latency as possible, without the guarantee of reading operations using the latest committed write. 

Azure Cosmos DB has five levels of data consistency options: 
• Strong 
• Bounded staleness 
• Session 
• Consistent prefix 
• Eventual 

Higher consistency levels guarantee that the latest committed write was read by the application, but you have a performance tradeoff of a few milliseconds using a higher consistency level. 

You should use a collection for the container type and document for the item type. Cosmos DB refers to container and item types according to which API is used in your account. The **MongoDB API refers to the container as a collection and document for each item inside a collection. **

You should not use a table for the container type. A table is the container type if you are using the Cassandra API or the Table API in Cosmos DB. 
You should not use a graph for the container type or edge for the item type. A graph is used as a container type and edge is used as an item type if you are using the Gremlin API in Cosmos DB.

You should use region with pre-calculated suffx based on sensorld. This partition key will distribute all the documents evenly across logical partitions. Including a pre-calculated suffx based on a known value (sensorld, for example) will greatly improve both write and read throughput across the partitions. 

You should not use region. This field contains only five possible values, resulting in a small number of logical partitions and a low read and write throughput. 

You should not use sensorld. This field is unique across all documents and will result in millions of logical partitions with a single document, impacting the read and write throughput. 

You should not use timestamp with a random SUffX. This partition key will distribute all documents across logical partitions evenly, greatly increasing the write throughput. However, reading a specific item will become harder because you do not know which suffx was used, impacting the read throughput. 

You should use GlobalDocumentDB to provision a Cosmos DB with the Core (SQL) API as required by the application. 

You should use the BoundedStaleness consistency level. This level is guaranteed to return the most recent committed version of a record in a multi-region write Cosmos DB database. 

You should enable multiple write locations to provision Cosmos DB in multi-regions with multiple write regions to satisfy the application requirements. 

You should perform the following steps in order: 
1. Create a database master key. 
2. Create a database scoped credential. 
3. Create an external data source and external file format. 
4. Create an external table. 

To access Azure Data Lake Storage Gen2, Azure Synapse Analytics can use a service principal credentials. However, it requires the creation of the master key (an operation that is required only once per database), which is then used to encrypt those credentials and store them as a database scoped credential. 

Relevant credentials will then be referenced in the newly created external data sources, which are used along with the external file formats to create external tables in the target Synapse SQL pool. 

You should not create a clustered columnstore index. A columnstore index is an in-memory table used in operational analytics. It is not relevant to the setup of external tables. 

You should not execute DBCC OPEN TRAN. It is a database command-line utility, which helps to identify active transactions that may be preventing log truncation.

You should run the New-AzSqlServerFirewallRule PowerShell cmdlet. This cmdlet creates a firewall rule that protects the logical server instance and database from unauthorized access. Only the IP addresses specified as parameters to the cmdlet can access the database from the internet. By default, internet access to Azure SQL Database is prohibited.

You should not set the Allow access to Azure services setting to off in the Azure portal. This setting allows you to execute queries and commands within the Azure portal. This does not affect external access. 

You should not run the az sql db audit-policy Azure CLI command. This command allows you to manage the audit policy for an Azure SQL Database instance. 

You should not add role assignments on the Access control (IAM) page of the Azure portal. Role assignments allow you to grant access to Azure resources to specific users or groups. In this scenario, you only want to ensure that users cannot access Azure SQL Database from the internet. Firewall settings provide this functionality.

You should use an Azure SQL Database managed instance deployment. This deployment option is almost 100% compatible with an on-premises instance, including the ability to use CLR features. When you back up the databases on-premises, you can execute a restore command to migrate the databases in Azure. This is referred to as lift and shift. 

You should not use an Azure Cosmos DB with the Core (SQL) API deployment. Cosmos DB is a multimodel database that supports five APIs for storage and queries, including Core (SQL), Table, Cassandra, Gremlin, and MongoDB. The Core API allows you to access data by using SQL-like queries. You cannot restore SQL Server databases to Cosmos DB by using SQL commands. 

You should not use an Azure Cosmos DB with the Table API deployment. The Table API is similar to Azure Tables. This deployment is useful if you are migrating an application from Azure Tables to Cosmos DB. With Azure Tables, you can access data by using Language Integrated Query (LINQ) and OData. You cannot restore SQL Server databases to Cosmos DB by using SQL commands. 

You should not use an Azure SQL Database with an elastic pool deployment. An elastic pool allows you to deploy multiple databases to a single logical instance and have all databases share a pool of resources. You configure the resource usage upfront by choosing a purchasing model. You cannot take advantage of CLR features with an elastic pool.

You should use the following command: 

ALTER ROLE db_owner ADD MEMBER SAM 

This statement adds Sam as the database owner (db_owner). The db_owner role has administrative access over the database, including the ability to add or remove other users. 

The CREATE command allows you to create database objects, such as tables, logins, and users. 

The GRANT command grants permissions to a user. For example, GRANT ALTER ANY USER TO Sam gives Sam permission to create and remove other users. However, by adding Sam to the db_owner role, Sam automatically inherits that permission. 

The db_datareader role allows a user to query database objects. The db_datawriter role allows a user to write and update database objects.


This creates a replicated table. A **replicated table** is copied across all the compute nodes in a data warehouse. This improves the performance of queries for data in **small tables**. In this scenario, the Store table is small. It is less than 200 MB. 

You should not specify HASH as the distribution type. This uses hash distribution. Data is sharded across compute nodes by a column that you specify. 

This creates a hash-distributed table that uses Storeld as the distribution column. This allows the table to be distributed by each store. Parallel queries can be run for different stores on different compute nodes. 

You should not use Sku as the distribution column. This would distribute data across every SKU, making parallel queries that read the inventory position for all SKUs in a given store slow. 

This uses **replicated distribution**, which copies the same data across compute nodes. This is beneficial for **small tables**. 

**A round-robin distribution shards data evenly**. 

**Performance is better when using hash distribution. **

You should use hash distribution on Storeld for both FactSalesByStore and DimStore. Hash distribution shards data across compute nodes by placing all data that uses the same hash key on the same compute node. This improves the performance of the query in the scenario. 

You should use replicated distribution for the DimStore table. Replicated distribution copies the same data to all the compute nodes. This is useful when you want to read data from small fact tables. 

You should not use an outer join instead of an inner join. This would return more rows than necessary, and it would not improve performance. 

You should perform the following steps in order: 
1. Create a failover group and add the original Azure SQL Database. 
2. Monitor the sync process with the Get-AzSqlDatabaseFailoverGroup cmdlet and verify that its ReplicationState is equal to 2. 
3. Execute the Switch-AzSqlDatabaseFailoverGroup cmdlet by using the failover group's read-only listener endpoint. 
4. With the NSLOOKUP command, verify the swap of IP addresses between the failover group's read-write and read-only listeners. 
5. Delete the failover group and the original Azure SQL Database. 

You should start with the creation of the failover group and adding the original Azure SQL Database. This will initiate the deployment and the synchronization of the Azure SQL Database in the secondary Azure location. 

You should then monitor the sync process by using the Get-AzSqlDatabaseFailoverGroup cmdlet. When its output parameter ReplicationState returns 2 ("CATCH UP"), this indicates that the databases are in sync and can be safely failed over. 

You should then execute the Switch-AzSqlDatabaseFailoverGroup cmdlet. It needs to be executed against a secondary database server (represented by the failover group's read-only listener endpoint) that should become primary with full sync. 

Once the failover process is completed, you should use the NSLOOKUP command to confirm that the primary and secondary databases switched their geographical IP addresses. 

Finally, you should delete the failover group and the original Azure SQL Database. Their contents have now been successfully moved to the new region. 

You should not monitor the sync process with the Get-AzSqlDatabaseFailoverGroup cmdlet and verify that its ReplicationState is equal to O. Status O ("SEEDING") indicates that the secondary database is not yet seeded and that is why attempts to failover will fail. 

You should not execute the Switch-AzSqlDatabaseFailoverGroup cmdlet by using the failover group's read-write listener endpoint. This endpoint represents the primary database server, while this cmdlet should be executed against a secondary database server (represented by the failover group's read-only listener endpoint).

You should use Azure SQL Data Sync. Data Sync is a service that lets you synchronize data across multiple Azure SQL Databases and on-premises SQL Server instances bi-directionally. 

You should not use Azure SQL active geo-replication. Active geo-replication is a disaster recovery solution for Azure SQL Database that allows replicating a database to another Azure region. The synchronization direction is only from the master to the replica database, and you only have read access to the replica database.

You should not use DMA. DMA is an assessment tool for migrating SQL Server instances to Azure SQL Database. It evaluates incompatibilities and recommends performance improvements for the target database. 

You should not use Azure Database Migration Service. This is a fully managed service to migrate multiple database sources to Azure with minimal downtime. It does not support bi-directional synchronization or migration.

You should perform the following actions in order: 
1. Create a scoped credential with the Azure storage account key. 
2. Create an external data source with the HADOOP type and an external file format. 
3. Create an external table. 
4. Load the data into the FactCarSales table. 

You should create a scoped credential with the Azure storage account key. Azure Data Lake Storage Gen2 supports the use of storage account keys for Polybase access. 

You should create an external data source with the HADOOP type using the scoped credential created to connect Azure Synapse Analytics with the Azure Data Lake Store, and an external file format to configure the file format of the data stored in Azure Data Lake Store, such as a field delimiter for the source files, Next, you should create an external table using the external data source and the external file format previously defined to create a table representation of the data for Azure Synapse Analytics. 

You should then load the data into the FactCarSales table. You can use SQL queries to load the data from the external table into the FactCarSales table. 

You should not create a scoped credential with the Client Id and OAuth 2.0 token endpoint. You could use this option when you are connecting with Azure Data Lake Store. However, this would require a service principal in Azure AD to generate the Client Id and the token. 

You should not create an external data source with the BLOB_STORAGE type. This type is used when executing bulk operations with an on-premises SQL Server or Azure SQL Database.

You should use the hash-distributed distribution method for the FactSales table. **Hash-distributed tables achieve the highest query performance for large tables**, splitting the work across multiple compute nodes. 

You should use the replicated table option for the DimBusinessUnits table. This is a **small table in size, and replicating its content across all compute nodes will improve performance when joining with other tables**. 

You should use **round-robin** distribution for the StagingFactTable table. This method **distributes table rows evenly across all distributions and improves loading performance** during the ETL process. 

You should perform the following actions in any order: 
• Create a database master key. 
• Create an external data source for Azure Blob Storage. 
• Create an external file format from parquet file. 
• Create an external table. 
• Load the data in the FactSaleOrders table using T -SQL. 

You should first create a database master key. This master key stores shared keys to access Azure Blob Storage. 

You should create an external data source for Azure Blob Storage to allow the connection between the Azure SQL Data Warehouse and Azure Blob Storage. 

You should create an external file format for the parquet file to configure how PolyBase will import the data using the parquet files. 

You should create an external table. The external table is a representation of the data stored in Azure Blob Storage as a table. You need to use the external data source and the external file format previously defined with the parquet file to create this table. 

You should load the data in the FactSaleOrders table using T-SQL. The external table created previously supports common T -SQL queries. You could use an INSERT INTO SELECT statement to load data from the external table to the FactSaleOrders table. 

You should not enable PolyBase support with the sp_configure command. Enabling PolyBase support is only required for an on-premises SQL Server. Azure Synapse Analytics support for PolyBase is enabled by default. 

You should not enable T DE. T DE is used to encrypt data in rest. T DE should not be enabled to use PolyBase. 

You should not load the parquet file into a staging table. You can directly use the data in the parquet file using the T -SQL statements from the external table. You do not need to create a staging table to load the data. 

You should complete the cmdlet as shown below: 
New-AzSqlDatabaselnstanceFailoverGroup 
-Name AutoFailoverGroup 
-ResourceGroupName AutoProduction 
-PrimaryManagedlnstanceName Autolndustry 
-PartnerRegion EastUS 
-PartnerManagedlnstanceName Autolndustry Secondary 
-FailoverPolicy Automatic 

You should use New-AzSqlDatabaselnstanceFailoverGroup to create a failover group between Azure SQL Managed Instances. This command has four required parameters, the failover group Name, PrimaryManagedlnstanceName, PartnerManagedlnstanceName and PartnerRegion. You need to properly configure these properties to create the failover group as specified. 

You should configure ResourceGroupName for AutoProduction. This resource group will be used to provision your failover group. 

You should configure PrimaryManagedlnstanceName for Autolndustry. This is the primary managed instance as specified in requirements. 

You should configure PartnerManagedlnstanceName for AutolndustrySecondary. This is the secondary database as specified in requirements. 

You should configure PartnerRegion as EastUS. This is the region where AutolndustrySecondary is provisioned. 

You should not use Set-AzSqlDatabaseFailoverGroup. This command is used to modify a failover group configuration, like setting a new failover group policy. 

You should not use New-AzSqlDatabaseFailoverGroup. This command creates a failover group for Azure SQL Databases. You need to create a failover group for Azure SQL Managed Instances. 

For a large fact table, you should create a hash-distributed table. Query performance improves when the table is joined with a replicated table or with a table that is distributed on the same column. This avoids data movement. 

For a staging table with unknown data, you should create a round-robin distributed table. The data will be evenly distributed across the nodes, and no distribution column needs to be chosen. 

For a small dimension table, you should use a replicated table. No data movement is involved when the table is joined with another table on any column. 

For a table that has queries that scan a date range, you should create a partitioned table. Partition elimination can improve the performance of the scans when the scanned range is a small part of the table. 

You should not create a temporary table. A temporary table is only visible to the session that creates it and will be deleted when the session ends. 

You need the following catalog views: 
sys.tables - Gives the tables, including the name. 
sys.columns - Gives the columns, including the name. 
sys.pdw_column_distribution_properties - Gives the distribution information. 

Example of a query: 
SELECT t.name AS [tablename], c.name AS [columnname] 
FROM sys.tables AS t 
JOIN sys.columns AS c ON c.object_id = t.object_id 
JOIN sys.pdw_column_distribution_properties AS d ON d.object_id = t.object_id AND d.column_id : 
c.column_id 
WHERE d.distribution_ordinal = 1 

You do not need the following catalog views: 
• sys.pdw_distributions - Gives information about the distributions on the appliance. 
• sys.pdw_table_distribution_properties - Gives the distribution information for the tables. 
• sys.pdw_nodes_columns - Gives columns for user-defined objects. 

You need to perform the following steps in order: 
1. Assign an Azure AD identity to the Azure SQL Database server. 
2. Grant Key Vault permissions to the Azure SQL Database server. 
3. Add the Key Vault key to the Azure SQL Database server and set it as T DE Protector. 
4. Turn on T DE. 

When you configure Azure SQL TDE in the Azure portal, you get an Azure AD identity assigned and relevant permissions set to the Azure SQL Database server via the Azure Key Vault access policy automatically. 

However, when you use PowerShell, you need to perform these two steps manually. 

Next, you retrieve your custom key from the Azure Key Vault and add it to your Azure SQL Database server, and afterwards set that key as a TDE protector for all server resources. 

And finally, you use the Set-AzSqlDatabaseTransparentDataEncryption cmdlet to turn on TDE again, which will re-encrypt your Azure SQL Database, switching from the Microsoft-managed key to your own custom managed key. 

You should not export or import the contents of your Azure SQL Database in BACPAC format. You would do that to move the contents of an Azure SQL Database between cloud and on-premises SQL instances. 
