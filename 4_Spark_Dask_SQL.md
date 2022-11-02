# 🧮 DASK
- [Official documentation](https://docs.dask.org/en/stable/): including examples and tutorials
- [Dask archives](https://coiled.io/blog/tag/dask/): official blog with additional examples and tutorials
- [XGboost](https://xgboost.readthedocs.io/en/stable/tutorials/dask.html): example of a full implementation; other example can be found [here](https://github.com/coiled/coiled-resources/blob/main/blogs/dask-python-xgboost-example-100GB-synth-dataset.ipynb) and [here](https://matthewrocklin.com/blog/work/2017/03/28/dask-xgboost)
- Resource management:
  - [Best practices](https://docs.dask.org/en/stable/best-practices.html)
  - [Choosing chunk sizes](https://blog.dask.org/2021/11/02/choosing-dask-chunk-sizes)
  - [Memory usage](https://www.coiled.io/blog/dask-memory-usage)


## Notes
- Ideally we should have one partition for each worker.
- Typically 10% of RAM is used to communicate with OS. Then, around 60% of RAM is needed to manage workload (overhead). Ultimately, we only end up with  roughly 54% of initial RAM to actually perform computations.
- Typically, each chunk/ partition should be between 10 MB and 1 GB to minimize IO overhead.


## Snippets
[Adjust memory budget](https://stackoverflow.com/questions/69429950/dask-what-does-memory-limit-control#:~:text=The%20link%20you%20posted%20says,reach%2095%25%20of%20RAM%20usage.)
```python
from dask.distributed import LocalCluster, Client
cluster = LocalCluster(n_workers=2,
                       threads_per_worker=4,
                       memory_target_fraction=0.95,
                       memory_limit='8GB')
client = Client(cluster)
client
```

Missing values count
```python
mssing_count = ((df.isnull().sum() / df.index.size()) * 100)
mssing_count.compute()
```

Inspecting partitioning of dataframe
```python
df.divisions # boundaries of the partitioning scheme
df.npartitions
df.map_partitions(len).compute() # number of rows in each partition
```

How to store andd read a model
```python
import dill
with open('model.pkl', 'wb') as file:
  dill.dump(model, file)
  
 with open('model.pkl', 'rb') as file:
  model_loaded = dill.load(file)
model_loaded.predict(X_test)
```

[Assessing DataFrame partitions](https://www.coiled.io/blog/dask-memory-usage)
```python
def partition_report(ddf):
    series = ddf.memory_usage_per_partition(deep=True).compute()
    total = series.count()
    print(f"Total number of partitions: {total}")
    total_memory = format_bytes(series.sum())
    print(f"Total DataFrame memory: {total_memory}")
    total = total.astype(numpy.float64)
    lt_1kb = series.where(lambda x : x < 1000).count()
    lt_1kb_percentage = '{:.1%}'.format(lt_1kb/total)
    lt_1mb = series.where(lambda x : x < 1000000).count()
    lt_1mb_percentage = '{:.1%}'.format(lt_1mb/total)
    gt_1gb = series.where(lambda x : x > 1000000000).count()
    gt_1gb_percentage = '{:.1%}'.format(gt_1gb/total)
    print(f"Num partitions < 1 KB: {lt_1kb} ({lt_1kb_percentage})")
    print(f"Num partitions < 1 MB: {lt_1mb} ({lt_1mb_percentage})")
    print(f"Num partitions > 1 GB: {gt_1gb} ({gt_1gb_percentage})")
```

# ⚡SPARK

## Books
- [Learning Spark: Lightning-Fast Data Analytics](https://pages.databricks.com/rs/094-YMS-629/images/LearningSpark2.0.pdf) 

## 🔨 resources and tools
- [Spark SQL, DataFrames and Datasets Guide (official)](https://spark.apache.org/docs/3.3.0/sql-programming-guide.html)
-  [Spark by examples](https://sparkbyexamples.com/pyspark/): a comprehensive guide to PySpark based on examples
- [Spark tutorial](https://www.youtube.com/watch?v=zC9cnh8rJd0&list=PLYhRPCyrSUlpJTrU8CSjy94O66m-04ifn&index=2&t=343s)
- [Project pro](https://www.projectpro.io/tutorial/):
  - [Spark tutorial](https://www.projectpro.io/apache-spark-tutorial/spark-tutorial)
  - [PySpark tutorial](https://www.projectpro.io/apache-spark-tutorial/pyspark-tutorial)

## Snippets


```python
sc._conf.getAll() # check SparkContext configurations in shell

# Create an RDD
# by generating data
array = sc.parallellize(range(1,100)

array.getNumPartitions()

# by reading from file
```

# 🏁 SQL

- [SQL main tasks summarized](https://towardsdatascience.com/sql-practical-details-cheat-sheet-for-data-analysis-f98406a71a09)
- [10 most important SQL concepts](https://towardsdatascience.com/ten-sql-concepts-you-should-know-for-data-science-interviews-7acf3e428185)
