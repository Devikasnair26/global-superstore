# Global Superstore
- The main file uploaded is a text for the sql code.

STEP 1: Create Dimension Tables

This step creates dimension tables to store reference data for customers, calendar dates, products, locations, and orders.
Each table has a primary key and relevant attributes.
Additionally, indexes are created on frequently used columns for faster querying.
STEP 2: Stage Data

A temporary table named STAGE_Orders is created to hold the raw data from the source system (GroupOP.dbo.Orders).
Data is loaded into STAGE_Orders for orders between specific dates (2011-01-01 to 2011-12-31).
This step also calculates the difference between Order Date and Ship Date and stores it in the Response column.
The table includes additional flags (Record_Customer_Exists, etc.) to track whether corresponding records exist in dimension tables.
Finally, the OrderDate and ShipDate columns are linked to the DIM_Calendar table using foreign keys.
STEP 3: Populate Dimension Tables

This step identifies and inserts distinct records from STAGE_Orders into the dimension tables (Customer, Location, Product, Order) if they don't already exist.
Identity insert is turned off to prevent gaps in the auto-incrementing primary key columns.
STEP 4: Update Stage Table and Populate Fact Table

This step updates the STAGE_Orders table by linking each record to its corresponding dimension table record using foreign keys.
The Customer_WK, Location_WK, Product_WK, and Order_WK columns are populated based on matches in the dimension tables.
Flags (Record_Customer_Exists, etc.) are updated to indicate successful linking.
Finally, data from STAGE_Orders is inserted into the fact table FACT_Orders. This table stores detailed sales information with foreign key references to the dimension tables.
In summary, this script demonstrates the ETL (Extract, Transform, Load) process for populating a data warehouse with dimensional and factual data.
