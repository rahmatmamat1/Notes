## **ML in BigQuery**

BigQuery ML is a BQ feature which allows us to create and execute Machine Learning models using standard SQL queries, without additional knowledge of Python nor any other programming languages and without the need to export data into a different system.

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

We will now create a few example queries to show how BQ ML works. Let's begin with creating a custom table:
```sql
CREATE OR REPLACE TABLE `taxi-rides-ny.nytaxi.yellow_tripdata_ml` (
  `passenger_count` INTEGER,
  `trip_distance` FLOAT64,
  `PULocationID` STRING,
  `DOLocationID` STRING,
  `payment_type` STRING,
  `fare_amount` FLOAT64,
  `tolls_amount` FLOAT64,
  `tip_amount` FLOAT64
) AS (
  SELECT passenger_count, trip_distance, CAST(PULocationID AS STRING), CAST(DOLocationID AS STRING), CAST(payment_type AS STRING), fare_amount, tolls_amount, tip_amount
  FROM `taxi-rides-ny.nytaxi.yellow_tripdata_partitoned`
  WHERE fare_amount != 0
);
```

-   BQ supports [_**feature preprocessing**_](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-preprocess-overview), both _**manual**_ and _**automatic**_.
-   A few columns such as `PULocationID` are categorical in nature but are represented with integer numbers in the original table. We _**cast**_ them as strings in order to get BQ to automatically preprocess them as categorical features that will be one-hot encoded.
-   Our target feature for the model will be `tip_amount`. We drop all records where `tip_amount` equals zero in order to improve training.

Let's now create a simple linear regression model with default settings:

```sql
CREATE OR REPLACE MODEL `taxi-rides-ny.nytaxi.tip_model`
OPTIONS (
	model_type='linear_reg',
	input_label_cols=['tip_amount'],
	DATA_SPLIT_METHOD='AUTO_SPLIT'
) AS
SELECT
	*
FROM
	`taxi-rides-ny.nytaxi.yellow_tripdata_ml`
WHERE
	tip_amount IS NOT NULL;
```

* The `CREATE MODEL` clause will create the `taxi-rides-ny.nytaxi.tip_model` model
* The `OPTIONS()` clause contains all of the necessary arguments to create our model/
	* `model_type='linear_reg'` is for specifying that we will create a linear regression model.
	* `input_label_cols=['tip_amount']` lets BQ know that our target feature is `tip_amount`. For linear regression models, target features must be real numbers.
	* `DATA_SPLIT_METHOD='AUTO_SPLIT'` is for automatically splitting the dataset into train/test datasets.
* The `SELECT` statement indicates which features need to be considered for training the model.
	* Since we already created a dedicated table with all of the needed features, we simply select them all.
* Running this query may take several minutes.
* After the query runs successfully, the BQ explorer in the side panel will show all available models (just one in our case) with a special icon. Selecting a model will open a new tab with additional info such as model details, training graphs and evaluation metrics.

We can also get a description of the features with the following query:

```sql
SELECT * FROM ML.FEATURE_INFO(MODEL `taxi-rides-ny.nytaxi.tip_model`);
```

* The output will be similar to `describe()` in Pandas.

Model evaluation against a separate dataset is as follows:

```sql
SELECT
	*
FROM
ML.EVALUATE(
	MODEL `taxi-rides-ny.nytaxi.tip_model`, (
		SELECT
			*
		FROM
			`taxi-rides-ny.nytaxi.yellow_tripdata_ml`
		WHERE
			tip_amount IS NOT NULL
	)
);
```

* This will output similar metrics to those shown in the model info tab but with the updated values for the evaluation against the provided dataset.
* In this example we evaluate with the same dataset we used for training the model, so this is a silly example for illustration purposes.

The main purpose of a ML model is to make predictions. A `ML.PREDICT` statement is used for doing them:
```sql
SELECT
	*
FROM
ML.PREDICT(
	MODEL `taxi-rides-ny.nytaxi.tip_model`, (
		SELECT
			*
		FROM
			`taxi-rides-ny.nytaxi.yellow_tripdata_ml`
		WHERE
			tip_amount IS NOT NULL
	)
);
```

* The `SELECT` statement within `ML.PREDICT` provides the records for which we want to make predictions.

* Once again, we're using the same dataset we used for training to calculate predictions, so we already know the actual tips for the trips, but this is just an example.

Additionally, BQ ML has a special `ML.EXPLAIN_PREDICT` statement that will return the prediction along with the most important features that were involved in calculating the prediction for each of the records we want predicted.

```sql
SELECT
*
FROM
ML.EXPLAIN_PREDICT(
	MODEL `taxi-rides-ny.nytaxi.tip_model`,(
		SELECT
			*
		FROM
			`taxi-rides-ny.nytaxi.yellow_tripdata_ml`
		WHERE
			tip_amount IS NOT NULL
	), STRUCT(3 as top_k_features)
);
```

* This will return a similar output to the previous query but for each prediction, 3 additional rows will be provided with the most significant features along with the assigned weights for each feature.

Just like in regular ML models, BQ ML models can be improved with ***hyperparameter tuning***. Here's an example query for tuning:

```sql
CREATE OR REPLACE MODEL `taxi-rides-ny.nytaxi.tip_hyperparam_model`
OPTIONS (
	model_type='linear_reg',
	input_label_cols=['tip_amount'],
	DATA_SPLIT_METHOD='AUTO_SPLIT',
	num_trials=5,
	max_parallel_trials=2,
	l1_reg=hparam_range(0, 20),
	l2_reg=hparam_candidates([0, 0.1, 1, 10])
) AS
SELECT
	*
FROM
	`taxi-rides-ny.nytaxi.yellow_tripdata_ml`
WHERE
	tip_amount IS NOT NULL;
```

* We create a new model as normal but we add the `num_trials` option as an argument.

* All of the regular arguments used for creating a model are available for tuning. In this example we opt to tune the L1 and L2 regularizations.

All of the necessary reference documentation is available [in this link](https://cloud.google.com/bigquery-ml/docs/reference).

## BigQuery ML deployment

_[Video source](https://www.youtube.com/watch?v=BjARzEWaznU&list=PL3MmuxUbc_hJed7dXYoJw8DoCuVHhGEQb&index=30)_

ML models created within BQ can be exported and deployed to Docker containers running TensorFlow Serving.

The following steps are based on [this official tutorial](https://cloud.google.com/bigquery-ml/docs/export-model-tutorial). All of these commands are to be run from a terminal and the gcloud sdk must be installed.

1. Authenticate to your GCP project.
```sh
gcloud auth login
```

2. Export the model to a Cloud Storage bucket.
```sh
bq --project_id taxi-rides-ny extract -m nytaxi.tip_model gs://taxi_ml_model/tip_model
```

3. Download the exported model files to a temporary directory.
```sh
mkdir /tmp/model
gsutil cp -r gs://taxi_ml_model/tip_model /tmp/model
```

4. Create a version subdirectory
```sh
mkdir -p serving_dir/tip_model/1
cp -r /tmp/model/tip_model/* serving_dir/tip_model/1
# Optionally you may erase the temporary directoy
rm -r /tmp/model
```

5. Pull the TensorFlow Serving Docker image
```sh
docker pull tensorflow/serving
```

6. Run the Docker image. Mount the version subdirectory as a volume and provide a value for the `MODEL_NAME` environment variable.
```sh
# Make sure you don't mess up the spaces!
docker run \
-p 8501:8501 \
--mount type=bind,source=`pwd`/serving_dir/tip_model,target=/models/tip_model \
-e MODEL_NAME=tip_model \
-t tensorflow/serving &
```

7. With the image running, run a prediction with curl, providing values for the features used for the predictions.
```sh
curl \
-d '{"instances": [{"passenger_count":1, "trip_distance":12.2, "PULocationID":"193", "DOLocationID":"264", "payment_type":"2","fare_amount":20.4,"tolls_amount":0.0}]}' \
-X POST http://localhost:8501/v1/models/tip_model:predict
```

