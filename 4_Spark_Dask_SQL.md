# ⚡SPARK

## Books
- [Learning Spark: Lightning-Fast Data Analytics](https://pages.databricks.com/rs/094-YMS-629/images/LearningSpark2.0.pdf) 

## 🔨 resources and tools
- [Spark by examples](https://sparkbyexamples.com/pyspark/): a comprehensive guide to PySpark based on examples
- Project
- [Project pro](https://www.projectpro.io/tutorial/):
  - [Spark tutorial](https://www.projectpro.io/apache-spark-tutorial/spark-tutorial)
  - [PySpark tutorial](https://www.projectpro.io/apache-spark-tutorial/pyspark-tutorial)

# ```SQL```

- [SQL main tasks summarized](https://towardsdatascience.com/sql-practical-details-cheat-sheet-for-data-analysis-f98406a71a09)
- [10 most important SQL concepts](https://towardsdatascience.com/ten-sql-concepts-you-should-know-for-data-science-interviews-7acf3e428185)


# ```Dask```
- [Official documentation](https://docs.dask.org/en/stable/): including examples and tutorials
- [Dask archives](https://coiled.io/blog/tag/dask/): official blog with additional examples and tutorials
- [XGboost](https://xgboost.readthedocs.io/en/stable/tutorials/dask.html): example of a full implementation; another example can be found [here](https://github.com/coiled/coiled-resources/blob/main/blogs/dask-python-xgboost-example-100GB-synth-dataset.ipynb)


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

