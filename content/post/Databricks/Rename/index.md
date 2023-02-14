---
title: Renaming Multiple Columns using PySpark
summary: An introduction to different strategies for renaming multiple columns using PySpark
tags:
  - Intro
  - Databricks
  - PySpark
date: 2023-02-14
ShowToc: true
UseHugoToc: true
TocOpen: true
draft: false

image:
  filename: featured
  focal_point: Smart
  preview_only: false
weight: 10

---

As a Data Engineer, a common task is to rename columns from the source system into more clear and readable names. Often multiple renames are required. In this demo I will walk through a few options that aim to solve this.

{{toc}}

## Creating demo data

Lets first create some dummy data


```python
from pyspark.sql.types import StructType,StructField, StringType, IntegerType

data = [("James","","Smith","36636","M",3000),
    ("Michael","Rose","","40288","M",4000),
    ("Robert","","Williams","42114","M",4000),
    ("Maria","Anne","Jones","39192","F",4000),
    ("Jen","Mary","Brown","","F",-1)
  ]
schema = StructType([ \
    StructField("fname",StringType(),True), \
    StructField("mname",StringType(),True), \
    StructField("lname",StringType(),True), \
    StructField("id", StringType(), True), \
    StructField("gen", StringType(), True), \
    StructField("sal", IntegerType(), True) \
  ])

df = spark.createDataFrame(data=data,schema=schema)
display(df)
```


<style scoped>
  .table-result-container {
    max-height: 300px;
    overflow: auto;
  }
  table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
  }
  th, td {
    padding: 5px;
  }
  th {
    text-align: left;
  }
</style><div class='table-result-container'><table class='table-result'><thead class='table-result-head'><tr><th>fname</th><th>mname</th><th>lname</th><th>id</th><th>gen</th><th>sal</th></tr></thead><tbody><tr><td>James</td><td></td><td>Smith</td><td>36636</td><td>M</td><td>3000</td></tr><tr><td>Michael</td><td>Rose</td><td></td><td>40288</td><td>M</td><td>4000</td></tr><tr><td>Robert</td><td></td><td>Williams</td><td>42114</td><td>M</td><td>4000</td></tr><tr><td>Maria</td><td>Anne</td><td>Jones</td><td>39192</td><td>F</td><td>4000</td></tr><tr><td>Jen</td><td>Mary</td><td>Brown</td><td></td><td>F</td><td>-1</td></tr></tbody></table></div>


Assuming you want to rename the following columns:
- fname -> FirstName
- mname -> MiddleName
- lname -> LastName
- id -> ID
- gen -> Gender
- sal -> Salary

There are numerous ways do so, some more suitable for more columns. I have listed a few alternatives that only add one step to the physical execution plan.

**Option 1)** Using .withColumnRenamed

- Quick and easy for one or more columns. Tedious for multiple.


```python
df_renamed_opt1 = (df
                   .withColumnRenamed('fname', 'FirstName')
                   .withColumnRenamed('mname', 'MiddleName')
                   .withColumnRenamed('lname', 'LastName')
                   .withColumnRenamed('id', 'ID')
                   .withColumnRenamed('gen', 'Gender')
                   .withColumnRenamed('sal', 'Salary')
                  )
# Display data
display(df_renamed_opt1)
# Explain physical execution plan
df_renamed_opt1.explain()
```


<style scoped>
  .table-result-container {
    max-height: 300px;
    overflow: auto;
  }
  table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
  }
  th, td {
    padding: 5px;
  }
  th {
    text-align: left;
  }
</style><div class='table-result-container'><table class='table-result'><thead class='table-result-head'><tr><th>FirstName</th><th>MiddleName</th><th>LastName</th><th>ID</th><th>Gender</th><th>Salary</th></tr></thead><tbody><tr><td>James</td><td></td><td>Smith</td><td>36636</td><td>M</td><td>3000</td></tr><tr><td>Michael</td><td>Rose</td><td></td><td>40288</td><td>M</td><td>4000</td></tr><tr><td>Robert</td><td></td><td>Williams</td><td>42114</td><td>M</td><td>4000</td></tr><tr><td>Maria</td><td>Anne</td><td>Jones</td><td>39192</td><td>F</td><td>4000</td></tr><tr><td>Jen</td><td>Mary</td><td>Brown</td><td></td><td>F</td><td>-1</td></tr></tbody></table></div>



    == Physical Plan ==
    *(1) Project [fname#525 AS FirstName#685, mname#526 AS MiddleName#692, lname#527 AS LastName#699, id#528 AS ID#706, gen#529 AS Gender#713, sal#530 AS Salary#720]
    +- *(1) Scan ExistingRDD[fname#525,mname#526,lname#527,id#528,gen#529,sal#530]
    
    
    


**Option 2.a)** Using a zipped dictionary; key, value lists

- Great for a list of columns


```python
from pyspark.sql.functions import col

mapping = dict(zip(['fname', 'mname', 'lname', 'id', 'gen', 'sal'], # keys: original col(s) name
                   ['FirstName', 'MiddleName', 'LastName', 'ID', 'Gender', 'Salary'] # value: new col(s) name
                  ))

# Transform
df_renamed_opt2a = df.select([col(c).alias(mapping.get(c, c)) for c in df.columns])
# Display data
display(df_renamed_opt2a)
# Explain physical execution plan
df_renamed_opt2a.explain()
```


<style scoped>
  .table-result-container {
    max-height: 300px;
    overflow: auto;
  }
  table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
  }
  th, td {
    padding: 5px;
  }
  th {
    text-align: left;
  }
</style><div class='table-result-container'><table class='table-result'><thead class='table-result-head'><tr><th>FirstName</th><th>MiddleName</th><th>LastName</th><th>ID</th><th>Gender</th><th>Salary</th></tr></thead><tbody><tr><td>James</td><td></td><td>Smith</td><td>36636</td><td>M</td><td>3000</td></tr><tr><td>Michael</td><td>Rose</td><td></td><td>40288</td><td>M</td><td>4000</td></tr><tr><td>Robert</td><td></td><td>Williams</td><td>42114</td><td>M</td><td>4000</td></tr><tr><td>Maria</td><td>Anne</td><td>Jones</td><td>39192</td><td>F</td><td>4000</td></tr><tr><td>Jen</td><td>Mary</td><td>Brown</td><td></td><td>F</td><td>-1</td></tr></tbody></table></div>



    == Physical Plan ==
    *(1) Project [fname#525 AS FirstName#740, mname#526 AS MiddleName#741, lname#527 AS LastName#742, id#528 AS ID#743, gen#529 AS Gender#744, sal#530 AS Salary#745]
    +- *(1) Scan ExistingRDD[fname#525,mname#526,lname#527,id#528,gen#529,sal#530]
    
    
    


**Option 2.b)** Using a dictionary
- Great for multiple columns. Readable.


```python
mapping = {
    #'original' : 'renamed',
    'fname' : 'FirstName',
    'mname' : 'MiddleName',
    'lname' : 'LastName',
    'id' : 'ID',
    'gen' : 'Gender',
    'sal' : 'Salary'
}

# Transform
df_renamed_opt2b = df.select([col(c).alias(mapping[c]) for c in df.columns])
# Display data
display(df_renamed_opt2b)
# Explain physical execution plan
df_renamed_opt2b.explain()
```


<style scoped>
  .table-result-container {
    max-height: 300px;
    overflow: auto;
  }
  table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
  }
  th, td {
    padding: 5px;
  }
  th {
    text-align: left;
  }
</style><div class='table-result-container'><table class='table-result'><thead class='table-result-head'><tr><th>FirstName</th><th>MiddleName</th><th>LastName</th><th>ID</th><th>Gender</th><th>Salary</th></tr></thead><tbody><tr><td>James</td><td></td><td>Smith</td><td>36636</td><td>M</td><td>3000</td></tr><tr><td>Michael</td><td>Rose</td><td></td><td>40288</td><td>M</td><td>4000</td></tr><tr><td>Robert</td><td></td><td>Williams</td><td>42114</td><td>M</td><td>4000</td></tr><tr><td>Maria</td><td>Anne</td><td>Jones</td><td>39192</td><td>F</td><td>4000</td></tr><tr><td>Jen</td><td>Mary</td><td>Brown</td><td></td><td>F</td><td>-1</td></tr></tbody></table></div>



    == Physical Plan ==
    *(1) Project [fname#132 AS FirstName#384, mname#133 AS MiddleName#385, lname#134 AS LastName#386, id#135 AS ID#387, gen#136 AS Gender#388, sal#137 AS Salary#389]
    +- *(1) Scan ExistingRDD[fname#132,mname#133,lname#134,id#135,gen#136,sal#137]
    
    
    


Note: df.columns assumes all columns. You can do select only on the specified columns in the zipped list or dictionary mapping by using this instead:
```python
df.select([col(c).alias(mapping[c]) for c in mapping])
```

**Option 3.a)** Using SQL

If you are familiar with SQL you can query the data with the appropriate renaming of the columns.


```python
# Create a temp view to query against
df.createOrReplaceTempView('employees')

# Query data
df_renamed_opt3a = spark.sql(
    """
    SELECT
        fname AS FirstName,
        mname AS MiddleName,
        lname AS LastName,
        id AS ID,
        gen AS Gender,
        sal AS Salary
    FROM 
        employees
    """
)

# Display data
display(df_renamed_opt3a)
# Explain physical execution plan
df_renamed_opt3a.explain()
```


<style scoped>
  .table-result-container {
    max-height: 300px;
    overflow: auto;
  }
  .table-result-head {
    background-color: black;
    text-color: white;
  }
  table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
  }
  th, td {
    padding: 5px;
  }
  th {
    text-align: left;
  }
</style><div class='table-result-container'><table class='table-result'><thead class='table-result-head'><tr><th>FirstName</th><th>MiddleName</th><th>LastName</th><th>ID</th><th>Gender</th><th>Salary</th></tr></thead><tbody><tr><td>James</td><td></td><td>Smith</td><td>36636</td><td>M</td><td>3000</td></tr><tr><td>Michael</td><td>Rose</td><td></td><td>40288</td><td>M</td><td>4000</td></tr><tr><td>Robert</td><td></td><td>Williams</td><td>42114</td><td>M</td><td>4000</td></tr><tr><td>Maria</td><td>Anne</td><td>Jones</td><td>39192</td><td>F</td><td>4000</td></tr><tr><td>Jen</td><td>Mary</td><td>Brown</td><td></td><td>F</td><td>-1</td></tr></tbody></table></div>



    == Physical Plan ==
    *(1) Project [fname#132 AS FirstName#500, mname#133 AS MiddleName#501, lname#134 AS LastName#502, id#135 AS ID#503, gen#136 AS Gender#504, sal#137 AS Salary#505]
    +- *(1) Scan ExistingRDD[fname#132,mname#133,lname#134,id#135,gen#136,sal#137]
    
    
    

