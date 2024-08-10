# AP-Morgan-Sample-ADF-Databricks-CSV-Processor

1.Data Ingestion: We need to build a proper mechanism to ingest data from various application sources into ADLS GEN2.
2.ETL System: We always get the data in raw format, so we must transform this data into usable format by using required transformations in Azure Data Factory.
3.Data lake: We get data from different sources so we need to have a centralized repo to store them. Here we are using ADLS Gen 2.
4.Scalability: You never know when we are going to get huge volumes of data, so we need to make sure that our system is able to cope up with that sudden change.
5.Cloud: When we have vast data it is always better to go with cloud because it is easy to use and scalable. Here we are using Azure cloud environment.
6.Azure DataBricks: When data is huge the first thing that should come into your mind is Azure DataBricks which is fast and can deal with huge volumes of data.

# Architecture Used

<img width="264" alt="image" src="https://github.com/user-attachments/assets/e335ce7d-6f74-426a-ad20-7c7390d51967">


# High Level Project Flow
Data comes to ADLS Landing Folder --> Goes through ADF Pipeline --> DataBricks (schema evaluation through SQL Database Schema) --> Secrets stored in Azure Key Vault --> Staging or Rejected.

# Detailed Proejct Flow

1.Ingest data into landing folder in ADLS input container. This is the source side of the ADF pipeline.
Now coming to the destination side of the ADF pipeline we need to setup a Databricks file. For that we must set up DataBricks account and then import the attched project (python) file.
2.It's time to evaluate the data in Databricks. We have two main things to focus on, Duplicate rows and Date Schema validation. For date schema evaluation we need to set up SQL database(create tables using given SQL script) and import the schema to data bricks for incoming data evaluation.
3.Lets create a Key Vault to store all the sensitive information like passwords and tokens.
4.We need to give required IAM access(like Key Vault Administrator, Key Vault Certificates Officer...etc) in KeyVault to the user to access the secrets from different Azure services.
5.Final step it to create an ADF pipeline and mount data from ADLS to Databricks to perform necessary validations to segregate data into Staging and rejected folders.
Now put a storage event trigger. So, when the data is ingested into the landing folder then the trigger automatically triggers the pipeline and data bricks evaluates data. Data will be stored in eligible folder (either staging or Rejected).
6.Now the data is enriched and available for the downstream departments.

You need to have good knowledge on Azure cloud services especially Azure Data factory, Azure SQL server, Azure databricks, Azure Key Vault to be able to perform the required ETL operations and analytics in SQL. Must be able to allow necessary permissions on the fly as required.
