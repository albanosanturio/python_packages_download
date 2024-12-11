# python_packages_download
analyzing trends in python packages downloads

1.using initially pypi dataset:               https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=pypi&page=dataset
querying wanted packages, pulling info until today

Initial query to start going for: 

```sql
SELECT project, count(1) FROM `bigquery-public-data.pypi.file_downloads` 
WHERE 
DATE(timestamp)
BETWEEN DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY) AND CURRENT_DATE()
AND project IN (
                "pandas"
                "polars"
                "poetry"
                "great-expectations"
                "kafka-python",
                "boto3",
                "google-api-core",
                "azure-core",
                "google-cloud-bigquery",
                "sqlalchemy",
                "redis",
                "pyspark",
                "beautifulsoup4",
                "scikit-learn",
                "tensorflow",
                "torch",
                "kubernetes",
                "docker",
                "dask",
                "jenkinsapi",
                "apache-airflow",
                "airbyte"
                )
GROUP BY 1
```


2.then feeding data through pypi stats api:   https://pypistats.org/api/
set frecuency, and method (cloud function? CRON job?)
feeding all info since last day with data.

3.creating an easy visualzation to track this. line graph. know packages with more %up and more %down
