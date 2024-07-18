# MIE1628_Assignment_4

Getting Familiar with Azure Cloud Platform 

1. Create a resource group in your Azure portal and deploy three resources. Azure Data Factory, Azure SQL DB, and Blob storage account.

![image](https://github.com/user-attachments/assets/772e8b5b-7517-4014-8baf-fd7f8729068d)

2. Now create a pipeline in Azure Data Factory and copy the gender_jobs_data.csv file from the Blob storage account to Azure SQL DB. (First copy this file from your local machine to Blob Storage).

![image](https://github.com/user-attachments/assets/e6f169d3-03ed-435d-b5f8-6215cb7f030b)

3. Trigger Options: Used to schedule a Data pipeline run without any interventions. 

- Schedule: Can run a Data pipeline according to a predetermined schedule with different scheduling intervals. Can choose the start and end dates, and specific future calendar dates.
- Tumbling Window: Executes Data pipelines at a specified time slice or predetermined periodic time interval. The tumbling window sends the start and end times for each time window in the Database, returning all data between those periods.
- Storage Event-based: Triggers occur in response to blob-related events such as generating or deleting a blob event in an Azure blob storage. These are also compatible with Azure Data Lakes.

4. A client needs to replicate objects from ADLS Gen 2 in Canada Central to ADLS Gen 2 in West Europe. Let’s say they want to do this in a bi-directional way. How can you set this up?
 
Cross-regional replication provides data recovery in cases of failure and allows staggered times for updates which will minimize downtimes, and reduce the chances of regional disaster network outages. Azure storage accounts are used to deploy storage resources such as blob containers, file shares, tables, or queues.

We want Geo-redundancy Storage (GRS) or Geo-Zone-redundant storage (GZRS), replication between different regions. Can change the replication setting using the portal “Storage -> Data Management -> Redundancy -> Update settings to Geo-redundant storage and choose “West Europe”.

Need to perform a manual migration, which allows us to move a storage account to another region, although this may have downtime in which a conversion option is an in-place migration with no downtime. However, with the GRS or GZRS options, the data in the secondary region isn’t available for read/write access.

Using the Azure portal will need to export the storage account template (resources –> automation - > export template), modify the template with the new storage account name and location in the JSON file, and move/deploy the storage account to create a new storage in the target location. Configure the new storage account, copy the data, there are many tools to copy data such as AzCopy. To copy the data, the ADLS Gen 2 Canada Central will be used as a source type and the ADLS Gen 2 West Europe will be used as a sink type.

Need to make sure that the storage in West Europe supports the desired replication settings (Also Geo-redundancy). Azure storage redundancy becomes more expensive when moving to geo-redundancy since it’s a more sophisticated redundancy level.

Bi-directional sync is ideal for complex scenarios that involve many pipelines and dependencies. Need to create replication rules that determine the directory in the file system that will be replicated and the Zones that will be used in that replication. Without replication rules defined, each Zone’s file system operates independently of the other. A tool such as WANdisco Fusion allows users control over how data is replicated between file systems and object stores.

Need to set up event triggers such that if there’s a new blob in one Zone, it will replicate objects from ADLS Gen 2 Canada Central to ADLS Gen 2 in West Europe using the steps shown above. Another event trigger such that if there’s a new blob in one Zone, will be used to replicate the object from ADLS Gen 2 West Europe to ADLS Gen 2 in Canada Central using the steps shown above.

**Part B: Using SQL in Azure SQL Database**

Select, from, where, groupby, orderby. Most calculations in the select statement.

![Part B-7 Code](https://github.com/user-attachments/assets/16ddd606-8db0-41f4-9ad8-01960fae6ff8)



