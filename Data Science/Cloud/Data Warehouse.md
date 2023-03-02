# Data Warehouse

![[Pasted image 20230225205525.png]]

![[Pasted image 20230225205613.png]]

## **What is a data warehouse?**
* OLAP solution
* Used for reporting and data analysis 

**![](https://lh5.googleusercontent.com/wEtpZ5p7N4rhsgeL1RPAh6b4zCvOJCXJiWvqRy6jhdwtLshXndBqKmeijgm0hJHaKVLJlkZPz8qKyDUdvhbdnTvDWaoOKNLYVm0Zbw-NX7cT50IZ8Vw2Iy9p6dB_7SWj8txCqozZgKdkdPcljd9f8nKFUQ=s2048)

## **BigQuery**
* Serverless data warehouse 
	* There are no servers to manage or database software to install
* Software as well as infrastructure including 
	* scalability and high-availability
* Built-in features like 
	* machine learning
	* geospatial analysis
	* business intelligence
* BigQuery maximizes flexibility by separating the compute engine that analyzes your data from your storage


## **BigQuery Cost**
* On demand pricing
	* 1 TB of data processed is $5
* Flat rate pricing
	* Based on number of pre requested slots
	* 100 slots → $2,000/month = 400 TB data processed on demand pricing


## **Partition in BQ**

![](https://lh3.googleusercontent.com/hfozJQXhmNPx34N0rvsGfU_rT2b83GkJAqkKSp8XVvoK9EF8sI4dNo0d3XTl4wuTk4Rtl_JBf7e2lR-WISKGDZBIm3MPNtiyDBPwYaeWb_iI0KSrfE_EYQVFYmNHNT4bfPxIC6DWmjkYG1k3T9nVJosXSQ=s2048)


## **Clustering in BigQuery**

![](https://lh6.googleusercontent.com/OMptV73oL4sKu8bx1zAw9kBZSqXaYoNrq5_HT3VTJDInQ-9f2qpDaFykBQE4nnTtDiBroYu2GTa0vCtRiBAIQq3cpwTeIRvYd5-lr4DpL4M6ch_WKjNG0BH-TegLHr34rWIzmKHfMuEhWpVicp2iAJrSLw=s2048)


## **BigQuery partition**
* Time-unit column
* Ingestion time (_PARTITIONTIME)
* Integer range partitioning
* When using Time unit or ingestion time
	* Daily (Default)
	* Hourly
	* Monthly or yearly
* Number of partitions limit is 4000

Resource: https://cloud.google.com/bigquery/docs/partitioned-tables

## **BigQuery Clustering**
* Columns you specify are used to colocate related data
* Order of the column is important
* The order of the specified columns determines the sort order of the data.
* Clustering improves
	* Filter queries
	* Aggregate queries
* Table with data size < 1 GB, don’t show significant improvement with partitioning and clustering
* You can specify up to four clustering columns

Clustering columns must be top-level, non-repeated columns
* DATE
* BOOL
* GEOGRAPHY
* INT64
* NUMERIC
* BIGNUMERIC
* STRING
* TIMESTAMP
* DATETIME


## **Partitioning vs Clustering**

![[Pasted image 20230225210732.png]]

## **Clustering over paritioning**
* Partitioning results in a small amount of data per partition (approximately less than 1 GB)
* Partitioning results in a large number of partitions beyond the limits on partitioned tables
* Partitioning results in your mutation operations modifying the majority of partitions in the table frequently (for example, every few minutes)

## **Automatic reclustering**

As data is added to a clustered table
* the newly inserted data can be written to blocks that contain key ranges that overlap with the key ranges in previously written blocks
* These overlapping keys weaken the sort property of the table

To maintain the performance characteristics of a clustered table
* BigQuery performs automatic re-clustering in the background to restore the sort property of the table
* For partitioned tables, clustering is maintained for data within the scope of each partition.

## **BigQuery-Best Practice**

**Cost reduction**
* Avoid `SELECT *`
* Price your queries before running them
* Use clustered or partitioned tables
* Use streaming inserts with caution
* Materialize query results in stages

**Query performance**
* Filter on partitioned columns
* Denormalizing data
* Use nested or repeated columns
* Use external data sources appropriately
* Don't use it, in case u want a high query performance
* Reduce data before using a `JOIN`
* Do not treat `WITH` clauses as prepared statements
* Avoid oversharding tables
* Avoid JavaScript user-defined functions
* Use approximate aggregation functions (HyperLogLog++)
* Order Last, for query operations to maximize performance
* Optimize your join patterns
	* As a best practice, place the table with the largest number of rows first, followed by the table with the fewest rows, and then place the remaining tables by decreasing size.

## **Code**

```sql
-- Query public available table
SELECT station_id, name FROM
    bigquery-public-data.new_york_citibike.citibike_stations
LIMIT 100;
```
Query public dataset in BigQuery

```sql
-- Creating external table referring to gcs path
CREATE OR REPLACE EXTERNAL TABLE `taxi-rides-ny.nytaxi.external_yellow_tripdata`
OPTIONS (
  format = 'CSV',
  uris = ['gs://nyc-tl-data/trip data/yellow_tripdata_2019-*.csv', 'gs://nyc-tl-data/trip data/yellow_tripdata_2020-*.csv']
);

-- Check yellow trip data
SELECT * FROM `taxi-rides-ny.nytaxi.external_yellow_tripdata` limit 10;
```
Create `external_yellow_tripdata` table  in `nytaxi` database on `taxi-rides-ny` project id.

```sql
-- Create a non partitioned table from external table
CREATE OR REPLACE TABLE taxi-rides-ny.nytaxi.yellow_tripdata_non_partitoned AS
SELECT * FROM taxi-rides-ny.nytaxi.external_yellow_tripdata;

-- Create a partitioned table from external table
CREATE OR REPLACE TABLE taxi-rides-ny.nytaxi.yellow_tripdata_partitoned
PARTITION BY
  DATE(tpep_pickup_datetime) AS
SELECT * FROM taxi-rides-ny.nytaxi.external_yellow_tripdata;
```
Create partitioned and non partitioned table to compare both of them

```sql
-- Impact of partition
-- Scanning 1.6GB of data
SELECT DISTINCT(VendorID)
FROM taxi-rides-ny.nytaxi.yellow_tripdata_non_partitoned
WHERE DATE(tpep_pickup_datetime) BETWEEN '2019-06-01' AND '2019-06-30';

-- Scanning ~106 MB of DATA
SELECT DISTINCT(VendorID)
FROM taxi-rides-ny.nytaxi.yellow_tripdata_partitoned
WHERE DATE(tpep_pickup_datetime) BETWEEN '2019-06-01' AND '2019-06-30';
```
Partitioned table give query optimization

```sql
-- Let's look into the partitons
SELECT table_name, partition_id, total_rows
FROM `nytaxi.INFORMATION_SCHEMA.PARTITIONS`
WHERE table_name = 'yellow_tripdata_partitoned'
ORDER BY total_rows DESC;
```
Take a look at the information schema and see partition.

```sql
-- Creating a partition and cluster table
CREATE OR REPLACE TABLE taxi-rides-ny.nytaxi.yellow_tripdata_partitoned_clustered
PARTITION BY DATE(tpep_pickup_datetime)
CLUSTER BY VendorID AS
SELECT * FROM taxi-rides-ny.nytaxi.external_yellow_tripdata;

-- Query scans 1.1 GB
SELECT count(*) as trips
FROM taxi-rides-ny.nytaxi.yellow_tripdata_partitoned
WHERE DATE(tpep_pickup_datetime) BETWEEN '2019-06-01' AND '2020-12-31'
  AND VendorID=1;

-- Query scans 864.5 MB
SELECT count(*) as trips
FROM taxi-rides-ny.nytaxi.yellow_tripdata_partitoned_clustered
WHERE DATE(tpep_pickup_datetime) BETWEEN '2019-06-01' AND '2020-12-31'
  AND VendorID=1;
```
Create Cluster table and compare to the partitioned table.



## **Reference**
https://cloud.google.com/bigquery/docs/how-to
https://research.google/pubs/pub36632/
https://panoply.io/data-warehouse-guide/bigquery-architecture/
http://www.goldsborough.me/distributed-systems/2019/05/18/21-09-00-a_look_at_dremel/

