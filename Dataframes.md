<h2>Querying Files with Dataframes</h2>

Apache Spark™ and Databricks® allow you to use DataFrames to query large data files.

<h2>Introducing DataFrames</h2>
Under the covers, DataFrames are derived from data structures known as Resilient Distributed Datasets (RDDs). RDDs and DataFrames 
are immutable distributed collections of data. Let's take a closer look at what some of these terms mean before we understand how 
they relate to DataFrames:

<b>Resilient:</b> They are fault tolerant, so if part of your operation fails, Spark quickly recovers the lost computation.

<b>Distributed:</b> RDDs are distributed across networked machines known as a cluster.

<b>DataFrame:</b> A data structure where data is organized into named columns, like a table in a relational database, but with richer 
           optimizations under the hood.
           
Without the named columns and declared types provided by a schema, Spark wouldn't know how to optimize the executation of any computation. 
Since DataFrames have a schema, they use the Catalyst Optimizer to determine the optimal way to execute your code.

DataFrames were invented because the business community uses tables in a relational database, Pandas or R DataFrames, or Excel worksheets. 
A Spark DataFrame is conceptually equivalent to these, with richer optimizations under the hood and the benefit of being distributed 
across a cluster.

<h2>DataFrames and SQL</h2>
DataFrame syntax is more flexible than SQL syntax. Here we illustrate general usage patterns of SQL and DataFrames.

Suppose we have a data set we loaded as a table called myTable and an equivalent DataFrame, called df. We have three fields/columns called col_1 (numeric type), col_2 (string type) and col_3 (timestamp type) Here are basic SQL operations and their DataFrame equivalents.



| SQL                                         | DataFrame (Python)                    |  DataFrame (Scala)                |    
| ------------------------------------------- | ------------------------------------- | ----------------------------------|
| `SELECT col_1 FROM myTable`                 | `df.select(col("col_1"))`             | `df.select($"col_1")`             |
| `DESCRIBE myTable`                          | `df.printSchema()`                    | `df.printSchema`                  |
| `SELECT * FROM myTable WHERE col_1 > 0`     | `df.filter(col("col_1") > 0)`         | `df.filter($"col_1" > 0)`         |
| `..GROUP BY col_2`                          | `..groupBy(col("col_2"))`             | `..groupBy($"col_2")`             |
| `..ORDER BY col_2`                          | `..orderBy(col("col_2"))`             | `..orderBy($"col_2")`             |
| `..WHERE year(col_3) > 1990`                | `..filter(year(col("col_3")) > 1990)` | `..filter(year($"col_3") > 1990)` |
| `SELECT * FROM myTable LIMIT 10`            | `df.limit(10)`                        | `df.limit(10)`                    |
| `display(myTable)` (text format)            | `df.show()`                           | `df.show()`                       |
| `display(myTable)` (html format)            | `display(df)`                         | `display(df)`                     |

<img alt="Hint" title="Hint" style="vertical-align: text-bottom; position: relative;" width="30" height="30" src="https://files.training.databricks.com/static/images/icon-light-bulb.svg"/>&nbsp;**Hint:** You can also run SQL queries with the special syntax `spark.sql("SELECT * FROM myTable")`
