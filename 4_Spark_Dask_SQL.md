# 🧮 DASK
- [Official documentation](https://docs.dask.org/en/stable/): including examples and tutorials
- [Dask archives](https://coiled.io/blog/tag/dask/): official blog with additional examples and tutorials
- [XGboost](https://xgboost.readthedocs.io/en/stable/tutorials/dask.html): example of a full implementation; other example can be found [here](https://github.com/coiled/coiled-resources/blob/main/blogs/dask-python-xgboost-example-100GB-synth-dataset.ipynb) and [here](https://matthewrocklin.com/blog/work/2017/03/28/dask-xgboost)
- Resource management:
  - [Best practices](https://docs.dask.org/en/stable/best-practices.html)
  - [Choosing chunk sizes](https://blog.dask.org/2021/11/02/choosing-dask-chunk-sizes)
  - [Memory usage](https://www.coiled.io/blog/dask-memory-usage)
  - [General guidelines](https://docs.nersc.gov/analytics/dask/)
  - [Difference between processes and threads](https://towardsdatascience.com/which-is-faster-python-threads-or-processes-some-insightful-examples-26074e90848f)
    - [Configuration of LocalCluster](https://stackoverflow.com/questions/57760475/difference-between-dask-distributed-localcluster-with-threads-vs-processes)
   - [Threads per core](https://discourse.prefect.io/t/what-is-the-difference-between-a-daskexecutor-and-a-localdaskexecutor/374)
   - [Reduce memory usage by selecting "smaller" datatypes (ex. int8)](https://www.coiled.io/blog/dask-dtype-astype)


## Notes
- **Number of workers**
  - Ideally we should have one partition for each worker. 
  - Rule of thumb: square root of the number of cores per worker. 
  - In general more threads per worker are good for a program that spends most of its time in NumPy, SciPy, Numba, etc.
- **Number/ size of partitions**
  - Each chunk/ partition size should be between 100MB and 1GB to minimize I/O overhead.
    - Going over 1GB or 2GB means you have a really big dataset and/or a lot of memory available per core.
    - Partitions should be small enough so that many of them fit in a worker’s available memory at once.
  - Number of partitions should equal at least 2 - 3 times number of worker cores, otherwise some workers will stay idle.
    - At minimum shold equal the number of worker cores available.
    - \> 10,000 or 100,000 partitions may start to perform poorly.
    - Dask manipulates as many chunks in parallel as you have cores on that machine (ex. 1 GB chunks and 10 cores, will use at least 10 GB of memory).
    - Example: machine with 100 GB and 10 cores, should have partition in the 1GB range, allowing 10 chunks per core and preventing from being too small.
- **Number of threads per core**
  - If you use NumPy, Pandas, Scikit-learn, Numba that release the global interpreter lock (GIL): (1) the default number of threads (1 thread per core) works fine (i.e. you won’t benefit from multiple threads per core); (2) use mostly threads (fewer workers)
  - If you’re on larger machines with a high thread count (\> 10), you should split things up into a few processes (workers). 
      - Python can be highly productive with 10 threads per process (worker) with numeric work, but not 50 threads.
  - If you’re doing work on text data or Python collections like lists and dicts then use mostly processes (i.e. fewer threads per core, more workers).
- **Storge**
  - Store  data in formats that are optimized for random access, metadata storage, and binary encoding/ serialized (ex. Parquet, Zarr, HDF5). 
- **Diagnostic**
  - If workers are under memory pressure: repartition your dataset and increase the number of partitions. 
    - Smaller chunks of data will fit in memory easier and lowers the need to spill to disk.
- **Other**
  - Typically 10% of RAM is used to communicate with OS. Then, around 60% of RAM is needed to manage workload (overhead). Ultimately, we only end up with  roughly 54% of initial RAM to actually perform computations.
  - Accessing data from RAM is often much faster than accessing it from disk. Once you have your dataset in a clean state that both: (1) fits in memory, (2) is clean enough that you will want to try many different analyses, then it is a good time to persist your data in RAM.
  - Partition/ chunk data in alignment with common queries (ex. choose a dataframe column to sort by for fast selection and joins).


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

[Repartition DataFrame to get even-sized partitions](https://stackoverflow.com/questions/52642966/repartition-dask-dataframe-to-get-even-partitions)
```python
def _rebalance_ddf(ddf):
    """Repartition dask dataframe to ensure that partitions are roughly equal size.

    Assumes `ddf.index` is already sorted.
    """
    if not ddf.known_divisions:  # e.g. for read_parquet(..., infer_divisions=False)
        ddf = ddf.reset_index().set_index(ddf.index.name, sorted=True)
    index_counts = ddf.map_partitions(lambda _df: _df.index.value_counts().sort_index()).compute()
    index = np.repeat(index_counts.index, index_counts.values)
    divisions, _ = dd.io.io.sorted_division_locations(index, npartitions=ddf.npartitions)
    return ddf.repartition(divisions=divisions)
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

## Resources
- [SQL main tasks summarized](https://towardsdatascience.com/sql-practical-details-cheat-sheet-for-data-analysis-f98406a71a09)
- [10 most important SQL concepts](https://towardsdatascience.com/ten-sql-concepts-you-should-know-for-data-science-interviews-7acf3e428185)
- [Connecting PostgreSQL to Visual Studio Code](https://ryanhutzley.medium.com/getting-started-with-the-postgresql-extension-for-vscode-d666c281ec72)
- [Importing data from a PostgreSQL database to a Pandas DataFrame](https://medium.com/@alestamm/importing-data-from-a-postgresql-database-to-a-pandas-dataframe-5f4bffcd8bb2): alternative [source](https://www.geeksforgeeks.org/python-postgresql-select-data/)

## Snippets
Alternative to LIMIT
```SQL
SELECT TOP (10) product_id, year_intro
FROM products
```

Declaring and using variables
```SQL
-- DECLARE @variablename data_type: VARCHAR(n), INT, DECIMAL(p ,s), NUMERIC(p ,s)
-- where p : number of decimal digits that will be stored, both to the left and to the right of
-- the decimal point; s : number of decimal digits that will be stored to the right of the decimal point

DECLARE @my_artist VARCHAR(100)
DECLARE @test_int INT
SET @test_int = 5
SET @my_artist = 'AC/DC'
```

Filtering
```SQL
WHERE
  artist IN ('Van Halen', 'ZZ Top')
  description LIKE '%storm'
  demand_loss_mw IS NOT NULL
  name = @my_artist
  country IN
    (SELECT name
    FROM states
    WHERE indep_year < 1800);
 -- Filtering for GROUP BY
 HAVING SUM(demand_loss_mw) > 1000
```

Replacing NULL
```SQL
SELECT TradeGDPPercent, ImportGoodPercent,
ISNULL(Country, 'Unknown') AS NewCountry -- specify a value
ISNULL(TradeGDPPercent, ImportGoodPercent) AS NewPercent -- use value from another columns
FROM EconomicIndicators

-- Note: a blank is not the same as a NULL; empty string '' can be used to find blanks
```

Replacing NULL with COALESCE
```SQL
-- returns the first non-missing value
SELECT TradeGDPPercent, ImportGoodPercent,
COALESCE(TradeGDPPercent, ImportGoodPercent, 'N/A') AS NewPercent
FROM EconomicIndicators
```

Change column values based on conditions
```SQL
SELECT name, continent, indep_year,
  CASE WHEN ___ < ___ THEN 'before 1900'
       WHEN indep_year <= 1930 THEN '___'
       ELSE '___' 
       END AS indep_year_group
FROM states
ORDER BY indep_year_group;
```

Concatenating two tables
```SQL
SELECT country
FROM prime_ministers
-- Alternatives
UNION -- Duplicate rows are excluded
UNION ALL -- Includes duplicate rows
INTERSECT
EXCEPT
--
SELECT country
FROM presidents;
```

Temporary tables
```SQL
SELECT col1, col2, col3 
INTO #my_temp_table
FROM my_existing_table

#my_temp_table -- exists until connection or session ends
-- Remove table manually
DROP TABLE #my_temp_table
```

Join
```SQL
SELECT p1.country, p1.continent,
prime_minister, president
FROM prime_ministers AS p1
INNER JOIN presidents AS p2
ON p1.country = p2.country;
ON p1.continent = p2.continent AND p1.country <> p2.country;
-- or if the key is the same
USING (country);
```

Anti-join
```SQL
SELECT president, country, continent
FROM presidents
WHERE ___ LIKE '___'
  AND country ___ NOT IN
  (SELECT name
  FROM states
  WHERE indep_year < 1800);
```

Subquery
```SQL
SELECT DISTINCT monarchs.continent, subquery.max_perc
FROM monarchs,
(SELECT continent, MAX(women_parli_perc) AS max_perc
FROM states
GROUP BY continent) AS subquery
WHERE monarchs.continent = subquery.continent
ORDER BY continent;
```

Subquery inside SELECT clause
```SQL
SELECT DISTINCT continent,
  (SELECT COUNT(*)
  FROM states
  WHERE prime_ministers.continent = states.continent) AS countries_num
FROM prime_ministers;
```

Dates
```SQL
-- DATEPART: DD for Day, MM for Month, YY for Year, HH for Hour
-- DATEADD (DATEPART, number, date)
-- DATEDIFF (datepart, startdate, enddate)

SELECT DATEADD(DD, -30, '2020-06-21') AS Addition,
       DATEDIFF(DD, '2020-07-21', '2020-06-21') AS Difference
```

WHILE loop
```SQL
-- Declare ctr as an integer
DECLARE @ctr INT
-- Assign 1 to ctr
SET @ctr = 1
-- Specify the condition of the WHILE loop
WHILE @ctr < 10
-- Begin the code to execute inside WHILE loop
BEGIN
-- Keep incrementing the value of @ctr
SET @ctr = @ctr + 1
-- Check if ctr is equal to 4
IF @ctr = 4
-- When ctr is equal to 4, the loop will break
BREAK
-- End WHILE loop
END
```

Derived tables
```SQL
SELECT a.* FROM Kidney a
-- This derived table computes the Average age joined to the actual table
JOIN (SELECT AVG(Age) AS AverageAge
FROM Kidney) b
ON a.Age = b.AverageAge
```

Common Table Expressions (CTE)
```SQL
-- CTE definitions start with the keyword WITH
-- Followed by the CTE names and the columns it contains
-- Create a CTE to get the Maximum BloodPressure by Age
WITH BloodPressureAge(Age, MaxBloodPressure)
AS
(SELECT Age, MAX(BloodPressure) AS MaxBloodPressure
FROM Kidney
GROUP BY Age)
-- Create a query to use the CTE as a table
SELECT a.Age, MIN(a.BloodPressure), b.MaxBloodPressure
FROM Kidney a
-- Join the CTE with the table
JOIN BloodpressureAge b
ON a.Age = b.Age
GROUP BY a.Age, b.MaxBloodPressure
```

Window syntax
```SQL
-- Create the window with OVER clause
-- PARTITION BY creates the frame
-- If you do not include PARTITION BY the frame is the entire table
-- For FIRST_VALUE and LAST_VALUE the ORDER BY command is required
SELECT SalesPerson, SalesYear, CurrentQuota,
-- First value from every window
FIRST_VALUE(CurrentQuota)
OVER (PARTITION BY SalesYear ORDER BY ModifiedDate) AS StartQuota,
-- Last value from every window
LAST_VALUE(CurrentQuota)
OVER (PARTITION BY SalesYear ORDER BY ModifiedDate) AS EndQuota,
ModifiedDate as ModDate
FROM SaleGoal
```

Window syntax - lag and lead
```SQL
SELECT SalesPerson, SalesYear, CurrentQuota,
-- Create a window function to get the values from the next row
LEAD(CurrentQuota)
-- Create a window function to get the values from the previous row
LAG(CurrentQuota)
OVER (PARTITION BY SalesYear ORDER BY ModifiedDate) AS NextQuota,
ModifiedDate AS ModDate
FROM SaleGoal
```

Row numbers
```SQL
-- Sequentially numbers the rows in the window
-- ORDER BY is required when using ROW_NUMBER()
SELECT SalesPerson, SalesYear, CurrentQuota,
ROW_NUMBER()
OVER (PARTITION BY SalesPerson ORDER BY SalesYear) AS QuotabySalesPerson
FROM SaleGoal
```

[Standardize text: lowercase, unaccented, no special characters](https://www.codefari.com/2019/11/removereplace-special-characters-from.html)
```SQL
regexp_replace(lower(unaccent(column)), '[^\w]+',' ','g') AS new_column
```
