# UPC_Comparison_Analysis

UPC Comparison Analysis
This repository contains SQL queries and scripts for analyzing and comparing UPC (Universal Product Code) data from different backups of the Amazon Prime Now database.

Overview
The SQL query provided in this repository compares the UPC counts between two backup datasets (Backup_AmazonPrimeNow_03_06_2024 and Backup_AmazonPrimeNow_02_28_2024) for a specific job number. The comparison is based on ASIN (Amazon Standard Identification Number) and ZIP code.

SQL Query
_**SELECT new_asin, new_upc_count, old_upc_count
FROM (
    SELECT a.asin AS new_asin, 
           COUNT(distinct a.orig_upc) AS new_upc_count, 
           COUNT(distinct b.orig_upc) AS old_upc_count
    FROM Backup_AmazonPrimeNow_03_06_2024 AS a
    JOIN Backup_AmazonPrimeNow_02_28_2024 AS b ON a.zip = b.zip AND a.asin = b.asin 
    WHERE a.job_number ='7924966' and b.job_number ='7451359'
    GROUP BY a.asin
) AS counts
WHERE new_upc_count != old_upc_count;**_


Description
new_asin: The ASIN of the products from the latest backup.
new_upc_count: The count of distinct UPCs associated with the new ASIN.
old_upc_count: The count of distinct UPCs associated with the corresponding ASIN in the older backup.


How to Use
Clone this repository to your local machine.
Execute the provided SQL query in your SQL database environment, replacing the table names and job numbers with your actual data.
Analyze the results to identify discrepancies in UPC counts between the two backups.
