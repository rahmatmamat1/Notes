## **Internals**

### BigQuery Architecture

BigQuery is built on 4 infrastructure technologies.
-   _**Dremel**_: the _compute_ part of BQ. It executes the SQL queries.
    -   Dremel turns SQL queries into _execution trees_. The leaves of these trees are called _slots_ and the branches are called _mixers_.
    -   The _slots_ are in charge of reading data from storage and perform calculations.
    -   The _mixers_ perform aggregation.
    -   Dremel dinamically apportions slots to queries as needed, while maintaining fairness for concurrent queries from multiple users.
-   _**Colossus**_: Google's global storage system.
    -   BQ leverages a _columnar storage format_ and compression algorithms to store data.
    -   Colossus is optimized for reading large amounts of structured data.
    -   Colossus also handles replication, recovery and distributed management.
-   _**Jupiter**_: the network that connects Dremel and Colossus.
    -   Jupiter is an in-house network technology created by Google which is used for interconnecting its datacenters.
-   _**Borg**_: an orchestration solution that handles everything.
    -   Borg is a precursor of Kubernetes.

![](https://lh4.googleusercontent.com/jivvoB5JmA5-svAbHYAW2dkigc3Ti-mZS2G4MQCzG4ZA9OxD5-GQdmuy2TxJpfErBMj9HEEW4W-pB5B4_vGPZMUkrBve-u9AFbOI78wVfxoFmCFCuxgIka4YQRl8J0GK57UZnBXAM3CaEtg8xpRglf1h_g=s2048)

### Column-oriented vs record-oriented storage

Traditional methods for tabular data storage are _**record-oriented**_ (also known as _row-oriented_). Data is read sequentially row by row and then the columns are accessed per row. An example of this is a CSV file: each new line in the file is a record and all the info for that specific record is contained within that line.

BigQuery uses a _**columnar storage format**_. Data is stored according to the columns of the table rather than the rows. This is beneficial when dealing with massive amounts of data because it allows us to discard right away the columns we're not interested in when performing queries, thus reducing the amount of processed data.

![](https://lh6.googleusercontent.com/wrItTVBkixIdk2LkxnXeR8JDkFZ9tklxNuxCBRp2EMa-oYnhoO0BqeHREqgWhZ0GpFcF_JR6L5vrGZYxiTNTEWlINu9Qawcr6APcfw9artUZ8b_J4BhINN2V1zHCSkqKZudMaypC6uK3pOJvhmuDffEjGQ=s2048)

When performing queries, Dremel modifies them in order to create an _execution tree_: parts of the query are assigned to different mixers which in turn assign even smaller parts to different slots which will access Colossus and retrieve the data.

The columnar storage format is perfect for this workflow as it allows very fast data retrieval from colossus by multiple workers, which then perform any needed computation on the retrieved datapoints and return them to the mixers, which will perform any necessary aggregation before returning that data to the root server, which will compose the final output of the query.

![](https://lh3.googleusercontent.com/PpEJ_G9ra--bpzYNYzKcxjg4t1nmh9Sdqe4zCBRP0jF3nNCQ4EplRvEPSPECbjFpn2um_E9qlPEpXhFe4q6LCXeuiDmePdP4EZ218JhOn6gQCZ5_FWL9tpxnccraSbvTO5NOQ8wMJLC5xZis3ImvO1a4HA=s2048)
