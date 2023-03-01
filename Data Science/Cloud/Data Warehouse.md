
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

## **Internals**

![](https://lh4.googleusercontent.com/jivvoB5JmA5-svAbHYAW2dkigc3Ti-mZS2G4MQCzG4ZA9OxD5-GQdmuy2TxJpfErBMj9HEEW4W-pB5B4_vGPZMUkrBve-u9AFbOI78wVfxoFmCFCuxgIka4YQRl8J0GK57UZnBXAM3CaEtg8xpRglf1h_g=s2048)

![](https://lh6.googleusercontent.com/wrItTVBkixIdk2LkxnXeR8JDkFZ9tklxNuxCBRp2EMa-oYnhoO0BqeHREqgWhZ0GpFcF_JR6L5vrGZYxiTNTEWlINu9Qawcr6APcfw9artUZ8b_J4BhINN2V1zHCSkqKZudMaypC6uK3pOJvhmuDffEjGQ=s2048)

![](https://lh3.googleusercontent.com/PpEJ_G9ra--bpzYNYzKcxjg4t1nmh9Sdqe4zCBRP0jF3nNCQ4EplRvEPSPECbjFpn2um_E9qlPEpXhFe4q6LCXeuiDmePdP4EZ218JhOn6gQCZ5_FWL9tpxnccraSbvTO5NOQ8wMJLC5xZis3ImvO1a4HA=s2048)


## **ML in BigQuery**

* Target audience Data analysts, managers
* No need for Python or Java knowledge
* No need to export data into a different system

**Pricing**
* Free
	* 10 GB per month of data storage
	* 1 TB per month of queries processed
	* ML Create model step: First 10 GB per month is free

![](https://lh3.googleusercontent.com/LPeQQ166E9aJQ-GYGNHwF5dzajSCyqpOlck1cQt2VHngpUQOvJU6voel-CFd85fcunwAES4T_LBiliJ1XydamASRiprVFj7ZZ0WSUH2Q2W3qEE63R_Wv5v508bHvsKbtj4WZSUQd2RxfA91XX9KCGm7xWA=s2048)

**Flow**
![](https://lh5.googleusercontent.com/9Dt6RzToEVXlpjOjDsiJMQ1ubE-SMLF5H96Hj_bSsjC5i5xNJTq4YeoQnCAxQdDZlmwEt8PB8OWWfScwK2YkBRTiQwx0SV4SlG-n4KCTuZHAuNW1FNd_kDVv1BEH_X62SvzpKSx6L9MmElijY1xDe-UEkg=s2048)

**![](https://lh5.googleusercontent.com/qKRHiZUHJqXkPy1Ri9nXo9n_GoW8qJz7wiPuR6q3q392vQ0_BvCF4KF9G8ZlXPmLD2ZzI8pnHLmfSPvKDspw9HcQZ2S_0t7Z_cE93xh-w4zDR0nmnvGcEluYzcPtVk4cvfa3uvJGPuEqvUO_qYI6b2i15A=s2048)**

## **Reference**
https://cloud.google.com/bigquery/docs/how-to
https://research.google/pubs/pub36632/
https://panoply.io/data-warehouse-guide/bigquery-architecture/
http://www.goldsborough.me/distributed-systems/2019/05/18/21-09-00-a_look_at_dremel/

