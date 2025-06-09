🚀 Incremental Load Project using Azure Data Factory
This project demonstrates how to implement an incremental load architecture using Azure Data Factory, where data is fetched from a REST API (JSON format) and loaded into an Azure SQL Database using a stored procedure to handle upserts (update/insert logic).

🔧 Technologies Used
Azure Data Factory

Azure SQL Database

REST API (HTTP Dataset)

T-SQL (Stored Procedure with MERGE)

JSON Data Handling

📁 Project Workflow
Azure SQL Database Setup

Created two tables:

Orders – stores the final, up-to-date records.

temp_Orders – staging table to temporarily hold JSON API data.

Stored Procedure for Upsert Logic

Developed a sp_upsert_orders stored procedure using the MERGE statement.

The procedure compares incoming data with existing records:

Updates existing records only if the UpdatedDate is newer.

Inserts new records not present in the Orders table.

Ensures idempotency (no duplicate inserts on reruns).

Azure Data Factory Pipeline

Created a pipeline with:

Source: Web API (HTTP connector to consume JSON data).

Sink: Azure SQL Database (temp_Orders table).

Used Copy Activity to load data from the API to the staging table.

Triggered the stored procedure as part of the pipeline (via Stored Procedure activity or post-copy script).

Incremental Load Logic

Modified records in the API were reflected accurately in the Orders table.

Old data in temp_Orders is truncated automatically on each pipeline run (via pre-copy script or explicit truncation step).

The pipeline ensures only new or changed data is updated, optimizing performance and maintaining data integrity.

✅ Features
Automated and reliable incremental loading

No duplication or overwrite of unchanged data

Easy-to-modify architecture

Can be extended to support CDC (Change Data Capture) patterns
