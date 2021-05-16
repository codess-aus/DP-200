# DP-200 Implementing an Azure Data Solution

**Cosmos DB** is a non-relational data store that allows you to query data by using one of five APIs. The Table API allows you to use OData and Language Integrated Query (LINQ) to query data. You can issue LINQ queries with .NET. The Table API is best used to migrate applications using Table Storage without needing to update the code. You should consider using the Core (SQL) API for a new application using Cosmos DB.

An Azure SQL Database account is Microsoft's Platform-as-a-Service (PaaS) offering equivalent to on-premises SQL Server. With Azure SQL Database, you do not have to manage the physical infrastructure for SQL Server. However, **Azure SQL Database is a relational database**. This means that *every row in each table must have identical columns* (or attributes). In this scenario, you need to allow varying attributes. The managed instance deployment option is useful if you have an on-premises SQL Server instance with multiple databases that must all be moved to the cloud. All databases in a managed instance deployment share the same resources. 

