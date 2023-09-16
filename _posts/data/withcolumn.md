# withcolumn

## Change datatype

```scala
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types._

df.printSchema()
df = df.withColumn("salary", col("salary").cast(DoubleType))
       .withColumn("date of joining", (col("date of joining").cast(DateType)))
df.printSchema()
```

date of joining: string -> date
salary: integer -> double


## Adding a new column

```scala
df = df.withColumn("increment_in_salary", col("salary").multiply(5).divide(100))
```

## Updating the value of an existing column

```scala
df = df.withColumn("salary", col("salary").plus(col("increment_in_salary")))
```

## Dropping an unwanted column

df = df.drop(col("increment_in_salary"))

## edit

```scala
df = df.withColumn("salary", col("salary").plus(col("increment_in_salary")))
```

## Conditional

```scala
df = df.withColumn("gender",when(col("gender").equalTo("M"),lit("Male"))
                           .when(col("gender").equalTo("F"),lit("Female"))
                           .otherwise(lit("")))
```


## Rename col name

```scala
df = df.withColumnRenamed("gender","gender/sex")   
```

