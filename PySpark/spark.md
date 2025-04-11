# Spark Learning 

### Spark Session
A SparkSession is the entry point to using Apache Spark in Databricks or any other Spark environment. It provides a single point of access to Spark's functionalities, including reading data, running queries, and managing configurations.

```from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MySparkApp") \
    .config("spark.some.config.option", "some-value") \
    .getOrCreate()

```

### SELECT IN PySPARK
- using col() function
```
result_df = df.select(col('col1'), col('col2'), ... col('coln'))
result_df.show()
```
- Simple Way
```
result_df = df.select(df['col1'], df['col2'], ... df['coln'])
result_df.show()
```
- Select * in pyspark
```
1. df.select([col for col in df.columns]).show()
2. df.select("*").show()
```


### Filter and Where
```
from pyspark.sql.functions import col

filtered_df = df.where((col("age") > 30) & (col("gender") == "male"))

```
 On Multiple Condition
```
filtered_df = df.where((col("age") > 30) | (col("gender") == "male"))

filtered_df = df.filter((col("age") > 30) & (col("gender") == "male"))
```

FIlter 

```
filtered_df = df.filter(col("address.city") == "New York")

filtered_df = df.where((col("address.city") == "New York") & (col("address.zipcode") > 10001))
```

### GroupBy and Having
```
df.groupBy('department').count()
df.groupBy('department').sum('salary')
df.groupBy('department').avg('salary')
df.groupBy('department').max('salary')
df.groupBy('department').min('salary')]
```
 - Group By on Multiple Column

```
df.groupBy("department", "city") \
    .agg(sum("salary").alias("sum_salary"), \
         avg("salary").alias("avg_salary"), \
         sum("bonus").alias("sum_bonus"), \
         max("bonus").alias("max_bonus") \
     ) \
    .show(truncate=False)
``` 

- Using filter on aggregate data: This is like Having in SQL
```
df.groupBy("department") \
    .agg(sum("salary").alias("sum_salary"), \
      avg("salary").alias("avg_salary"), \
      sum("bonus").alias("sum_bonus"), \
      max("bonus").alias("max_bonus")) \
    .where(col("sum_bonus") >= 50000) \
    .show(truncate=False)
```

- Next Topics
1. OrderBy and Sort
2. window func
3. Joins
4. drop, dropDuplicates, 
5. dropna, fillna
6. explode()
7. cache and persist
8. UDFs
