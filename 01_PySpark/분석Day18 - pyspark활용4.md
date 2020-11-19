

# 분석Day17

>  pyspark활용3

### - 교육내용

```python
# windows
import pyspark
from pyspark.sql import SparkSession
spark = SparkSession.builder.master('local[2]') \
                    .appName('sparkedu') \
                    .getOrCreate()
spark
```





    <div>
        <p><b>SparkSession - in-memory</b></p>

<div>
    <p><b>SparkContext</b></p>


    <p><a href="http://DESKTOP-CS5B0E0:4040">Spark UI</a></p>
    
    <dl>
      <dt>Version</dt>
        <dd><code>v3.0.1</code></dd>
      <dt>Master</dt>
        <dd><code>local[2]</code></dd>
      <dt>AppName</dt>
        <dd><code>sparkedu</code></dd>
    </dl>

</div>

    </div>





```python
################################### AWS 에서 수행하는 코드
```


```python
# AWS-LINUX

import findspark
findspark.init("/opt/spark")
```


```python
import pyspark
from pyspark.sql import SparkSession
```


```python
spark = SparkSession.builder.getOrCreate()
spark
```


```python
dataList = [("Java", 20000), ("Python", 100000), ("Scala", 3000)]
rdd=spark.sparkContext.parallelize(dataList)
print(rdd)
print(type(rdd))
print(rdd.collect())
```


```python
print(spark.version)
```


```python
################################### AWS 에서 수행하는 코드
```


```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import mean,col,split, col, regexp_extract, when, lit
from pyspark.ml.feature import StringIndexer
from pyspark.ml import Pipeline
```


```python
titanic_df = spark.read.csv("data/train.csv",header = 'True',inferSchema='True')
```


```python
passengers_count = titanic_df.count()
```


```python
print(passengers_count)
```

    891



```python
titanic_df.show(5)
```

    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+
    |PassengerId|Survived|Pclass|                Name|   Sex| Age|SibSp|Parch|          Ticket|   Fare|Cabin|Embarked|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+
    |          1|       0|     3|Braund, Mr. Owen ...|  male|22.0|    1|    0|       A/5 21171|   7.25| null|       S|
    |          2|       1|     1|Cumings, Mrs. Joh...|female|38.0|    1|    0|        PC 17599|71.2833|  C85|       C|
    |          3|       1|     3|Heikkinen, Miss. ...|female|26.0|    0|    0|STON/O2. 3101282|  7.925| null|       S|
    |          4|       1|     1|Futrelle, Mrs. Ja...|female|35.0|    1|    0|          113803|   53.1| C123|       S|
    |          5|       0|     3|Allen, Mr. Willia...|  male|35.0|    0|    0|          373450|   8.05| null|       S|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+
    only showing top 5 rows


​    


```python
titanic_df.describe().show()
```

    +-------+-----------------+-------------------+------------------+--------------------+------+------------------+------------------+-------------------+------------------+-----------------+-----+--------+
    |summary|      PassengerId|           Survived|            Pclass|                Name|   Sex|               Age|             SibSp|              Parch|            Ticket|             Fare|Cabin|Embarked|
    +-------+-----------------+-------------------+------------------+--------------------+------+------------------+------------------+-------------------+------------------+-----------------+-----+--------+
    |  count|              891|                891|               891|                 891|   891|               714|               891|                891|               891|              891|  204|     889|
    |   mean|            446.0| 0.3838383838383838| 2.308641975308642|                null|  null| 29.69911764705882|0.5230078563411896|0.38159371492704824|260318.54916792738| 32.2042079685746| null|    null|
    | stddev|257.3538420152301|0.48659245426485753|0.8360712409770491|                null|  null|14.526497332334035|1.1027434322934315| 0.8060572211299488|471609.26868834975|49.69342859718089| null|    null|
    |    min|                1|                  0|                 1|"Andersson, Mr. A...|female|              0.42|                 0|                  0|            110152|              0.0|  A10|       C|
    |    max|              891|                  1|                 3|van Melkebeke, Mr...|  male|              80.0|                 8|                  6|         WE/P 5735|         512.3292|    T|       S|
    +-------+-----------------+-------------------+------------------+--------------------+------+------------------+------------------+-------------------+------------------+-----------------+-----+--------+


​    


```python
titanic_df.printSchema()
```

    root
     |-- PassengerId: integer (nullable = true)
     |-- Survived: integer (nullable = true)
     |-- Pclass: integer (nullable = true)
     |-- Name: string (nullable = true)
     |-- Sex: string (nullable = true)
     |-- Age: double (nullable = true)
     |-- SibSp: integer (nullable = true)
     |-- Parch: integer (nullable = true)
     |-- Ticket: string (nullable = true)
     |-- Fare: double (nullable = true)
     |-- Cabin: string (nullable = true)
     |-- Embarked: string (nullable = true)


​    


```python
titanic_df.select("Survived","Pclass","Embarked").show()
```

    +--------+------+--------+
    |Survived|Pclass|Embarked|
    +--------+------+--------+
    |       0|     3|       S|
    |       1|     1|       C|
    |       1|     3|       S|
    |       1|     1|       S|
    |       0|     3|       S|
    |       0|     3|       Q|
    |       0|     1|       S|
    |       0|     3|       S|
    |       1|     3|       S|
    |       1|     2|       C|
    |       1|     3|       S|
    |       1|     1|       S|
    |       0|     3|       S|
    |       0|     3|       S|
    |       0|     3|       S|
    |       1|     2|       S|
    |       0|     3|       Q|
    |       1|     2|       S|
    |       0|     3|       S|
    |       1|     3|       C|
    +--------+------+--------+
    only showing top 20 rows


​    

## 자~ EDA(Exploratory Data Analysis)를 해봅시다요.


```python
titanic_df.groupBy("Survived").count().show()
```

    +--------+-----+
    |Survived|count|
    +--------+-----+
    |       1|  342|
    |       0|  549|
    +--------+-----+


​    


```python
titanic_df.groupBy("Sex","Survived").count().show()
```

    +------+--------+-----+
    |   Sex|Survived|count|
    +------+--------+-----+
    |  male|       0|  468|
    |female|       1|  233|
    |female|       0|   81|
    |  male|       1|  109|
    +------+--------+-----+


​    


```python
titanic_df.groupBy("Pclass","Survived").count().show()
```

    +------+--------+-----+
    |Pclass|Survived|count|
    +------+--------+-----+
    |     1|       0|   80|
    |     3|       1|  119|
    |     1|       1|  136|
    |     2|       1|   87|
    |     2|       0|   97|
    |     3|       0|  372|
    +------+--------+-----+


​    


```python
# This function use to print feature with null values and null count 
def null_value_count(df):
  null_columns_counts = []
  numRows = df.count()
  for k in df.columns:
    nullRows = df.where(col(k).isNull()).count()
    if(nullRows > 0):
      temp = k,nullRows
      null_columns_counts.append(temp)
  return(null_columns_counts)
```


```python
null_columns_count_list = null_value_count(titanic_df)
```


```python
null_columns_count_list
```




    [('Age', 177), ('Cabin', 687), ('Embarked', 2)]




```python
spark.createDataFrame(null_columns_count_list, ['Column_With_Null_Value', 'Null_Values_Count']).show()
```

    +----------------------+-----------------+
    |Column_With_Null_Value|Null_Values_Count|
    +----------------------+-----------------+
    |                   Age|              177|
    |                 Cabin|              687|
    |              Embarked|                2|
    +----------------------+-----------------+


​    


```python
mean_age = titanic_df.select(mean('Age')).collect()[0][0]
print(mean_age)
```

    29.69911764705882



```python
titanic_df = titanic_df.withColumn("Initial",regexp_extract(col("Name"),"([A-Za-z]+)\.",1))
```


```python
df = spark.createDataFrame([('100-200',)], ['str'])
df.select(regexp_extract('str', r'(\d+)-(\d+)', 0).alias('d')).collect()
```




    [Row(d='100-200')]




```python
titanic_df.show()
```

    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+-------+
    |PassengerId|Survived|Pclass|                Name|   Sex| Age|SibSp|Parch|          Ticket|   Fare|Cabin|Embarked|Initial|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+-------+
    |          1|       0|     3|Braund, Mr. Owen ...|  male|22.0|    1|    0|       A/5 21171|   7.25| null|       S|     Mr|
    |          2|       1|     1|Cumings, Mrs. Joh...|female|38.0|    1|    0|        PC 17599|71.2833|  C85|       C|    Mrs|
    |          3|       1|     3|Heikkinen, Miss. ...|female|26.0|    0|    0|STON/O2. 3101282|  7.925| null|       S|   Miss|
    |          4|       1|     1|Futrelle, Mrs. Ja...|female|35.0|    1|    0|          113803|   53.1| C123|       S|    Mrs|
    |          5|       0|     3|Allen, Mr. Willia...|  male|35.0|    0|    0|          373450|   8.05| null|       S|     Mr|
    |          6|       0|     3|    Moran, Mr. James|  male|null|    0|    0|          330877| 8.4583| null|       Q|     Mr|
    |          7|       0|     1|McCarthy, Mr. Tim...|  male|54.0|    0|    0|           17463|51.8625|  E46|       S|     Mr|
    |          8|       0|     3|Palsson, Master. ...|  male| 2.0|    3|    1|          349909| 21.075| null|       S| Master|
    |          9|       1|     3|Johnson, Mrs. Osc...|female|27.0|    0|    2|          347742|11.1333| null|       S|    Mrs|
    |         10|       1|     2|Nasser, Mrs. Nich...|female|14.0|    1|    0|          237736|30.0708| null|       C|    Mrs|
    |         11|       1|     3|Sandstrom, Miss. ...|female| 4.0|    1|    1|         PP 9549|   16.7|   G6|       S|   Miss|
    |         12|       1|     1|Bonnell, Miss. El...|female|58.0|    0|    0|          113783|  26.55| C103|       S|   Miss|
    |         13|       0|     3|Saundercock, Mr. ...|  male|20.0|    0|    0|       A/5. 2151|   8.05| null|       S|     Mr|
    |         14|       0|     3|Andersson, Mr. An...|  male|39.0|    1|    5|          347082| 31.275| null|       S|     Mr|
    |         15|       0|     3|Vestrom, Miss. Hu...|female|14.0|    0|    0|          350406| 7.8542| null|       S|   Miss|
    |         16|       1|     2|Hewlett, Mrs. (Ma...|female|55.0|    0|    0|          248706|   16.0| null|       S|    Mrs|
    |         17|       0|     3|Rice, Master. Eugene|  male| 2.0|    4|    1|          382652| 29.125| null|       Q| Master|
    |         18|       1|     2|Williams, Mr. Cha...|  male|null|    0|    0|          244373|   13.0| null|       S|     Mr|
    |         19|       0|     3|Vander Planke, Mr...|female|31.0|    1|    0|          345763|   18.0| null|       S|    Mrs|
    |         20|       1|     3|Masselmani, Mrs. ...|female|null|    0|    0|            2649|  7.225| null|       C|    Mrs|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+-------+
    only showing top 20 rows


​    


```python
titanic_df.select("Initial").distinct().show()
```

    +--------+
    | Initial|
    +--------+
    |     Don|
    |    Miss|
    |Countess|
    |     Col|
    |     Rev|
    |    Lady|
    |  Master|
    |     Mme|
    |    Capt|
    |      Mr|
    |      Dr|
    |     Mrs|
    |     Sir|
    |Jonkheer|
    |    Mlle|
    |   Major|
    |      Ms|
    +--------+


​    


```python
titanic_df = titanic_df.replace(['Mlle','Mme', 'Ms', 'Dr','Major','Lady','Countess','Jonkheer','Col','Rev','Capt','Sir','Don'],
               ['Miss','Miss','Miss','Mr','Mr',  'Mrs',  'Mrs',  'Other',  'Other','Other','Mr','Mr','Mr'])
```


```python
titanic_df.show()
```

    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+-------+
    |PassengerId|Survived|Pclass|                Name|   Sex| Age|SibSp|Parch|          Ticket|   Fare|Cabin|Embarked|Initial|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+-------+
    |          1|       0|     3|Braund, Mr. Owen ...|  male|22.0|    1|    0|       A/5 21171|   7.25| null|       S|     Mr|
    |          2|       1|     1|Cumings, Mrs. Joh...|female|38.0|    1|    0|        PC 17599|71.2833|  C85|       C|    Mrs|
    |          3|       1|     3|Heikkinen, Miss. ...|female|26.0|    0|    0|STON/O2. 3101282|  7.925| null|       S|   Miss|
    |          4|       1|     1|Futrelle, Mrs. Ja...|female|35.0|    1|    0|          113803|   53.1| C123|       S|    Mrs|
    |          5|       0|     3|Allen, Mr. Willia...|  male|35.0|    0|    0|          373450|   8.05| null|       S|     Mr|
    |          6|       0|     3|    Moran, Mr. James|  male|null|    0|    0|          330877| 8.4583| null|       Q|     Mr|
    |          7|       0|     1|McCarthy, Mr. Tim...|  male|54.0|    0|    0|           17463|51.8625|  E46|       S|     Mr|
    |          8|       0|     3|Palsson, Master. ...|  male| 2.0|    3|    1|          349909| 21.075| null|       S| Master|
    |          9|       1|     3|Johnson, Mrs. Osc...|female|27.0|    0|    2|          347742|11.1333| null|       S|    Mrs|
    |         10|       1|     2|Nasser, Mrs. Nich...|female|14.0|    1|    0|          237736|30.0708| null|       C|    Mrs|
    |         11|       1|     3|Sandstrom, Miss. ...|female| 4.0|    1|    1|         PP 9549|   16.7|   G6|       S|   Miss|
    |         12|       1|     1|Bonnell, Miss. El...|female|58.0|    0|    0|          113783|  26.55| C103|       S|   Miss|
    |         13|       0|     3|Saundercock, Mr. ...|  male|20.0|    0|    0|       A/5. 2151|   8.05| null|       S|     Mr|
    |         14|       0|     3|Andersson, Mr. An...|  male|39.0|    1|    5|          347082| 31.275| null|       S|     Mr|
    |         15|       0|     3|Vestrom, Miss. Hu...|female|14.0|    0|    0|          350406| 7.8542| null|       S|   Miss|
    |         16|       1|     2|Hewlett, Mrs. (Ma...|female|55.0|    0|    0|          248706|   16.0| null|       S|    Mrs|
    |         17|       0|     3|Rice, Master. Eugene|  male| 2.0|    4|    1|          382652| 29.125| null|       Q| Master|
    |         18|       1|     2|Williams, Mr. Cha...|  male|null|    0|    0|          244373|   13.0| null|       S|     Mr|
    |         19|       0|     3|Vander Planke, Mr...|female|31.0|    1|    0|          345763|   18.0| null|       S|    Mrs|
    |         20|       1|     3|Masselmani, Mrs. ...|female|null|    0|    0|            2649|  7.225| null|       C|    Mrs|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+-----+--------+-------+
    only showing top 20 rows


​    


```python
titanic_df.select("Initial").distinct().show()
```

    +-------+
    |Initial|
    +-------+
    |   Miss|
    |  Other|
    | Master|
    |     Mr|
    |    Mrs|
    +-------+


​    


```python
titanic_df.groupby('Initial').avg('Age').collect()
```




    [Row(Initial='Miss', avg(Age)=21.86),
     Row(Initial='Other', avg(Age)=45.888888888888886),
     Row(Initial='Master', avg(Age)=4.574166666666667),
     Row(Initial='Mr', avg(Age)=32.73960880195599),
     Row(Initial='Mrs', avg(Age)=35.981818181818184)]




```python
titanic_df.filter(titanic_df.Age==46).select("Initial").show()
```

    +-------+
    |Initial|
    +-------+
    |     Mr|
    |     Mr|
    |     Mr|
    +-------+


​    


```python
titanic_df.select("Age").show()
```

    +----+
    | Age|
    +----+
    |22.0|
    |38.0|
    |26.0|
    |35.0|
    |35.0|
    |null|
    |54.0|
    | 2.0|
    |27.0|
    |14.0|
    | 4.0|
    |58.0|
    |20.0|
    |39.0|
    |14.0|
    |55.0|
    | 2.0|
    |null|
    |31.0|
    |null|
    +----+
    only showing top 20 rows


​    


```python
titanic_df = titanic_df.withColumn("Age",when((titanic_df["Initial"] == "Miss") & (titanic_df["Age"].isNull()), 22).otherwise(titanic_df["Age"]))
titanic_df = titanic_df.withColumn("Age",when((titanic_df["Initial"] == "Other") & (titanic_df["Age"].isNull()), 46).otherwise(titanic_df["Age"]))
titanic_df = titanic_df.withColumn("Age",when((titanic_df["Initial"] == "Master") & (titanic_df["Age"].isNull()), 5).otherwise(titanic_df["Age"]))
titanic_df = titanic_df.withColumn("Age",when((titanic_df["Initial"] == "Mr") & (titanic_df["Age"].isNull()), 33).otherwise(titanic_df["Age"]))
titanic_df = titanic_df.withColumn("Age",when((titanic_df["Initial"] == "Mrs") & (titanic_df["Age"].isNull()), 36).otherwise(titanic_df["Age"]))
```


```python
titanic_df.groupBy("Embarked").count().show()
```

    +--------+-----+
    |Embarked|count|
    +--------+-----+
    |       Q|   77|
    |    null|    2|
    |       C|  168|
    |       S|  644|
    +--------+-----+


​    


```python
titanic_df = titanic_df.na.fill({"Embarked" : 'S'})
```


```python
titanic_df = titanic_df.drop("Cabin")
```


```python
titanic_df.printSchema()
```

    root
     |-- PassengerId: integer (nullable = true)
     |-- Survived: integer (nullable = true)
     |-- Pclass: integer (nullable = true)
     |-- Name: string (nullable = true)
     |-- Sex: string (nullable = true)
     |-- Age: double (nullable = true)
     |-- SibSp: integer (nullable = true)
     |-- Parch: integer (nullable = true)
     |-- Ticket: string (nullable = true)
     |-- Fare: double (nullable = true)
     |-- Embarked: string (nullable = false)
     |-- Initial: string (nullable = true)


​    


```python
titanic_df = titanic_df.withColumn("Family_Size",col('SibSp')+col('Parch'))
```


```python
titanic_df.show()
```

    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+--------+-------+-----------+
    |PassengerId|Survived|Pclass|                Name|   Sex| Age|SibSp|Parch|          Ticket|   Fare|Embarked|Initial|Family_Size|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+--------+-------+-----------+
    |          1|       0|     3|Braund, Mr. Owen ...|  male|22.0|    1|    0|       A/5 21171|   7.25|       S|     Mr|          1|
    |          2|       1|     1|Cumings, Mrs. Joh...|female|38.0|    1|    0|        PC 17599|71.2833|       C|    Mrs|          1|
    |          3|       1|     3|Heikkinen, Miss. ...|female|26.0|    0|    0|STON/O2. 3101282|  7.925|       S|   Miss|          0|
    |          4|       1|     1|Futrelle, Mrs. Ja...|female|35.0|    1|    0|          113803|   53.1|       S|    Mrs|          1|
    |          5|       0|     3|Allen, Mr. Willia...|  male|35.0|    0|    0|          373450|   8.05|       S|     Mr|          0|
    |          6|       0|     3|    Moran, Mr. James|  male|33.0|    0|    0|          330877| 8.4583|       Q|     Mr|          0|
    |          7|       0|     1|McCarthy, Mr. Tim...|  male|54.0|    0|    0|           17463|51.8625|       S|     Mr|          0|
    |          8|       0|     3|Palsson, Master. ...|  male| 2.0|    3|    1|          349909| 21.075|       S| Master|          4|
    |          9|       1|     3|Johnson, Mrs. Osc...|female|27.0|    0|    2|          347742|11.1333|       S|    Mrs|          2|
    |         10|       1|     2|Nasser, Mrs. Nich...|female|14.0|    1|    0|          237736|30.0708|       C|    Mrs|          1|
    |         11|       1|     3|Sandstrom, Miss. ...|female| 4.0|    1|    1|         PP 9549|   16.7|       S|   Miss|          2|
    |         12|       1|     1|Bonnell, Miss. El...|female|58.0|    0|    0|          113783|  26.55|       S|   Miss|          0|
    |         13|       0|     3|Saundercock, Mr. ...|  male|20.0|    0|    0|       A/5. 2151|   8.05|       S|     Mr|          0|
    |         14|       0|     3|Andersson, Mr. An...|  male|39.0|    1|    5|          347082| 31.275|       S|     Mr|          6|
    |         15|       0|     3|Vestrom, Miss. Hu...|female|14.0|    0|    0|          350406| 7.8542|       S|   Miss|          0|
    |         16|       1|     2|Hewlett, Mrs. (Ma...|female|55.0|    0|    0|          248706|   16.0|       S|    Mrs|          0|
    |         17|       0|     3|Rice, Master. Eugene|  male| 2.0|    4|    1|          382652| 29.125|       Q| Master|          5|
    |         18|       1|     2|Williams, Mr. Cha...|  male|33.0|    0|    0|          244373|   13.0|       S|     Mr|          0|
    |         19|       0|     3|Vander Planke, Mr...|female|31.0|    1|    0|          345763|   18.0|       S|    Mrs|          1|
    |         20|       1|     3|Masselmani, Mrs. ...|female|36.0|    0|    0|            2649|  7.225|       C|    Mrs|          0|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+--------+-------+-----------+
    only showing top 20 rows


​    


```python
titanic_df.groupBy("Family_Size").count().show()
```

    +-----------+-----+
    |Family_Size|count|
    +-----------+-----+
    |          1|  161|
    |          6|   12|
    |          3|   29|
    |          5|   22|
    |          4|   15|
    |          7|    6|
    |         10|    7|
    |          2|  102|
    |          0|  537|
    +-----------+-----+


​    


```python
titanic_df = titanic_df.withColumn('Alone',lit(0))
```


```python
titanic_df = titanic_df.withColumn("Alone",when(titanic_df["Family_Size"] == 0, 1).otherwise(titanic_df["Alone"]))
```


```python
titanic_df.columns
```




    ['PassengerId',
     'Survived',
     'Pclass',
     'Name',
     'Sex',
     'Age',
     'SibSp',
     'Parch',
     'Ticket',
     'Fare',
     'Embarked',
     'Initial',
     'Family_Size',
     'Alone']




```python
indexers = [StringIndexer(inputCol=column, outputCol=column+"_index").fit(titanic_df) for column in ["Sex","Embarked","Initial"]]
pipeline = Pipeline(stages=indexers)
titanic_df = pipeline.fit(titanic_df).transform(titanic_df)
```


```python
titanic_df.show()
```

    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+--------+-------+-----------+-----+---------+--------------+-------------+
    |PassengerId|Survived|Pclass|                Name|   Sex| Age|SibSp|Parch|          Ticket|   Fare|Embarked|Initial|Family_Size|Alone|Sex_index|Embarked_index|Initial_index|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+--------+-------+-----------+-----+---------+--------------+-------------+
    |          1|       0|     3|Braund, Mr. Owen ...|  male|22.0|    1|    0|       A/5 21171|   7.25|       S|     Mr|          1|    0|      0.0|           0.0|          0.0|
    |          2|       1|     1|Cumings, Mrs. Joh...|female|38.0|    1|    0|        PC 17599|71.2833|       C|    Mrs|          1|    0|      1.0|           1.0|          2.0|
    |          3|       1|     3|Heikkinen, Miss. ...|female|26.0|    0|    0|STON/O2. 3101282|  7.925|       S|   Miss|          0|    1|      1.0|           0.0|          1.0|
    |          4|       1|     1|Futrelle, Mrs. Ja...|female|35.0|    1|    0|          113803|   53.1|       S|    Mrs|          1|    0|      1.0|           0.0|          2.0|
    |          5|       0|     3|Allen, Mr. Willia...|  male|35.0|    0|    0|          373450|   8.05|       S|     Mr|          0|    1|      0.0|           0.0|          0.0|
    |          6|       0|     3|    Moran, Mr. James|  male|33.0|    0|    0|          330877| 8.4583|       Q|     Mr|          0|    1|      0.0|           2.0|          0.0|
    |          7|       0|     1|McCarthy, Mr. Tim...|  male|54.0|    0|    0|           17463|51.8625|       S|     Mr|          0|    1|      0.0|           0.0|          0.0|
    |          8|       0|     3|Palsson, Master. ...|  male| 2.0|    3|    1|          349909| 21.075|       S| Master|          4|    0|      0.0|           0.0|          3.0|
    |          9|       1|     3|Johnson, Mrs. Osc...|female|27.0|    0|    2|          347742|11.1333|       S|    Mrs|          2|    0|      1.0|           0.0|          2.0|
    |         10|       1|     2|Nasser, Mrs. Nich...|female|14.0|    1|    0|          237736|30.0708|       C|    Mrs|          1|    0|      1.0|           1.0|          2.0|
    |         11|       1|     3|Sandstrom, Miss. ...|female| 4.0|    1|    1|         PP 9549|   16.7|       S|   Miss|          2|    0|      1.0|           0.0|          1.0|
    |         12|       1|     1|Bonnell, Miss. El...|female|58.0|    0|    0|          113783|  26.55|       S|   Miss|          0|    1|      1.0|           0.0|          1.0|
    |         13|       0|     3|Saundercock, Mr. ...|  male|20.0|    0|    0|       A/5. 2151|   8.05|       S|     Mr|          0|    1|      0.0|           0.0|          0.0|
    |         14|       0|     3|Andersson, Mr. An...|  male|39.0|    1|    5|          347082| 31.275|       S|     Mr|          6|    0|      0.0|           0.0|          0.0|
    |         15|       0|     3|Vestrom, Miss. Hu...|female|14.0|    0|    0|          350406| 7.8542|       S|   Miss|          0|    1|      1.0|           0.0|          1.0|
    |         16|       1|     2|Hewlett, Mrs. (Ma...|female|55.0|    0|    0|          248706|   16.0|       S|    Mrs|          0|    1|      1.0|           0.0|          2.0|
    |         17|       0|     3|Rice, Master. Eugene|  male| 2.0|    4|    1|          382652| 29.125|       Q| Master|          5|    0|      0.0|           2.0|          3.0|
    |         18|       1|     2|Williams, Mr. Cha...|  male|33.0|    0|    0|          244373|   13.0|       S|     Mr|          0|    1|      0.0|           0.0|          0.0|
    |         19|       0|     3|Vander Planke, Mr...|female|31.0|    1|    0|          345763|   18.0|       S|    Mrs|          1|    0|      1.0|           0.0|          2.0|
    |         20|       1|     3|Masselmani, Mrs. ...|female|36.0|    0|    0|            2649|  7.225|       C|    Mrs|          0|    1|      1.0|           1.0|          2.0|
    +-----------+--------+------+--------------------+------+----+-----+-----+----------------+-------+--------+-------+-----------+-----+---------+--------------+-------------+
    only showing top 20 rows


​    


```python
titanic_df.printSchema()
```

    root
     |-- PassengerId: integer (nullable = true)
     |-- Survived: integer (nullable = true)
     |-- Pclass: integer (nullable = true)
     |-- Name: string (nullable = true)
     |-- Sex: string (nullable = true)
     |-- Age: double (nullable = true)
     |-- SibSp: integer (nullable = true)
     |-- Parch: integer (nullable = true)
     |-- Ticket: string (nullable = true)
     |-- Fare: double (nullable = true)
     |-- Embarked: string (nullable = false)
     |-- Initial: string (nullable = true)
     |-- Family_Size: integer (nullable = true)
     |-- Alone: integer (nullable = false)
     |-- Sex_index: double (nullable = false)
     |-- Embarked_index: double (nullable = false)
     |-- Initial_index: double (nullable = false)


​    


```python
titanic_df = titanic_df.drop("PassengerId","Name","Ticket","Cabin","Embarked","Sex","Initial")
```


```python
titanic_df.show()
```

    +--------+------+----+-----+-----+-------+-----------+-----+---------+--------------+-------------+
    |Survived|Pclass| Age|SibSp|Parch|   Fare|Family_Size|Alone|Sex_index|Embarked_index|Initial_index|
    +--------+------+----+-----+-----+-------+-----------+-----+---------+--------------+-------------+
    |       0|     3|22.0|    1|    0|   7.25|          1|    0|      0.0|           0.0|          0.0|
    |       1|     1|38.0|    1|    0|71.2833|          1|    0|      1.0|           1.0|          2.0|
    |       1|     3|26.0|    0|    0|  7.925|          0|    1|      1.0|           0.0|          1.0|
    |       1|     1|35.0|    1|    0|   53.1|          1|    0|      1.0|           0.0|          2.0|
    |       0|     3|35.0|    0|    0|   8.05|          0|    1|      0.0|           0.0|          0.0|
    |       0|     3|33.0|    0|    0| 8.4583|          0|    1|      0.0|           2.0|          0.0|
    |       0|     1|54.0|    0|    0|51.8625|          0|    1|      0.0|           0.0|          0.0|
    |       0|     3| 2.0|    3|    1| 21.075|          4|    0|      0.0|           0.0|          3.0|
    |       1|     3|27.0|    0|    2|11.1333|          2|    0|      1.0|           0.0|          2.0|
    |       1|     2|14.0|    1|    0|30.0708|          1|    0|      1.0|           1.0|          2.0|
    |       1|     3| 4.0|    1|    1|   16.7|          2|    0|      1.0|           0.0|          1.0|
    |       1|     1|58.0|    0|    0|  26.55|          0|    1|      1.0|           0.0|          1.0|
    |       0|     3|20.0|    0|    0|   8.05|          0|    1|      0.0|           0.0|          0.0|
    |       0|     3|39.0|    1|    5| 31.275|          6|    0|      0.0|           0.0|          0.0|
    |       0|     3|14.0|    0|    0| 7.8542|          0|    1|      1.0|           0.0|          1.0|
    |       1|     2|55.0|    0|    0|   16.0|          0|    1|      1.0|           0.0|          2.0|
    |       0|     3| 2.0|    4|    1| 29.125|          5|    0|      0.0|           2.0|          3.0|
    |       1|     2|33.0|    0|    0|   13.0|          0|    1|      0.0|           0.0|          0.0|
    |       0|     3|31.0|    1|    0|   18.0|          1|    0|      1.0|           0.0|          2.0|
    |       1|     3|36.0|    0|    0|  7.225|          0|    1|      1.0|           1.0|          2.0|
    +--------+------+----+-----+-----+-------+-----------+-----+---------+--------------+-------------+
    only showing top 20 rows


​    

## pyspark.ml 모듈의 분석 함수들은 데이터셋에 features 가 있어야 학습을 진행함

### pyspark.ml.VectorAssember를 사용해서 feature로 사용하여 컬럼들에 대한 리스트를 지정하고 features 열을 추가한다.


```python
from pyspark.ml.feature import VectorAssembler
feature = VectorAssembler(inputCols=titanic_df.columns[1:],outputCol="features")
feature_vector= feature.transform(titanic_df)
```

## 훈련데이터와 검증 데이터를 8:2로 나눈다.


```python
(trainingData, testData) = feature_vector.randomSplit([0.8, 0.2],seed = 11)
```


```python
trainingData.show()
```

    +--------+------+----+-----+-----+--------+-----------+-----+---------+--------------+-------------+--------------------+
    |Survived|Pclass| Age|SibSp|Parch|    Fare|Family_Size|Alone|Sex_index|Embarked_index|Initial_index|            features|
    +--------+------+----+-----+-----+--------+-----------+-----+---------+--------------+-------------+--------------------+
    |       0|     1| 2.0|    1|    2|  151.55|          3|    0|      1.0|           0.0|          1.0|[1.0,2.0,1.0,2.0,...|
    |       0|     1|18.0|    1|    0|   108.9|          1|    0|      0.0|           1.0|          0.0|[1.0,18.0,1.0,0.0...|
    |       0|     1|19.0|    1|    0|    53.1|          1|    0|      0.0|           0.0|          0.0|(10,[0,1,2,4,5],[...|
    |       0|     1|19.0|    3|    2|   263.0|          5|    0|      0.0|           0.0|          0.0|[1.0,19.0,3.0,2.0...|
    |       0|     1|21.0|    0|    1| 77.2875|          1|    0|      0.0|           0.0|          0.0|(10,[0,1,3,4,5],[...|
    |       0|     1|24.0|    0|    1|247.5208|          1|    0|      0.0|           1.0|          0.0|[1.0,24.0,0.0,1.0...|
    |       0|     1|25.0|    1|    2|  151.55|          3|    0|      1.0|           0.0|          2.0|[1.0,25.0,1.0,2.0...|
    |       0|     1|27.0|    0|    2|   211.5|          2|    0|      0.0|           1.0|          0.0|[1.0,27.0,0.0,2.0...|
    |       0|     1|28.0|    0|    0|    47.1|          0|    1|      0.0|           0.0|          0.0|(10,[0,1,4,6],[1....|
    |       0|     1|28.0|    1|    0| 82.1708|          1|    0|      0.0|           1.0|          0.0|[1.0,28.0,1.0,0.0...|
    |       0|     1|31.0|    0|    0| 50.4958|          0|    1|      0.0|           0.0|          0.0|(10,[0,1,4,6],[1....|
    |       0|     1|33.0|    0|    0|     0.0|          0|    1|      0.0|           0.0|          0.0|(10,[0,1,6],[1.0,...|
    |       0|     1|33.0|    0|    0|     5.0|          0|    1|      0.0|           0.0|          0.0|(10,[0,1,4,6],[1....|
    |       0|     1|33.0|    0|    0|  25.925|          0|    1|      0.0|           0.0|          0.0|(10,[0,1,4,6],[1....|
    |       0|     1|33.0|    0|    0|   26.55|          0|    1|      0.0|           0.0|          0.0|(10,[0,1,4,6],[1....|
    |       0|     1|33.0|    0|    0| 27.7208|          0|    1|      0.0|           1.0|          0.0|(10,[0,1,4,6,8],[...|
    |       0|     1|33.0|    0|    0| 27.7208|          0|    1|      0.0|           1.0|          0.0|(10,[0,1,4,6,8],[...|
    |       0|     1|33.0|    0|    0| 30.6958|          0|    1|      0.0|           1.0|          0.0|(10,[0,1,4,6,8],[...|
    |       0|     1|33.0|    0|    0|    31.0|          0|    1|      0.0|           0.0|          0.0|(10,[0,1,4,6],[1....|
    |       0|     1|33.0|    0|    0|    39.6|          0|    1|      0.0|           1.0|          0.0|(10,[0,1,4,6,8],[...|
    +--------+------+----+-----+-----+--------+-----------+-----+---------+--------------+-------------+--------------------+
    only showing top 20 rows


​    

## 모델링

### Spark ML에서 제공하는 분류 분석

### LogisticRegression

### DecisionTreeClassifier

### RandomForestClassifier

### Gradient-boosted tree classifier

### NaiveBayes

### Support Vector Machine




```python
from pyspark.ml.evaluation import MulticlassClassificationEvaluator
```

## LogisticRegression

### 로지스틱 회귀(Logistic Regression)는 회귀를 사용하여 데이터가 어떤 범주에 속할 확률에서 0 에서 1 사이의 값으로 예측하고 

### 그 확률에 따라 가능성이 더 높은 범주에 속하는 것으로 분류해주는 지도 학습 알고리즘이다


```python
from pyspark.ml.classification import LogisticRegression
lr = LogisticRegression(labelCol="Survived", featuresCol="features")
#Training algo
lrModel = lr.fit(trainingData)
lr_prediction = lrModel.transform(testData)
lr_prediction.select("prediction", "Survived", "features").show()
evaluator = MulticlassClassificationEvaluator(labelCol="Survived", predictionCol="prediction", metricName="accuracy")
```

    +----------+--------+--------------------+
    |prediction|Survived|            features|
    +----------+--------+--------------------+
    |       1.0|       0|(10,[0,1,4,6,8],[...|
    |       1.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,6],[1.0,...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       1.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       1.0|       0|(10,[0,1,3,4,5],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|[1.0,58.0,0.0,2.0...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|[2.0,19.0,1.0,1.0...|
    +----------+--------+--------------------+
    only showing top 20 rows


​    

### 평가


```python
lr_accuracy = evaluator.evaluate(lr_prediction)
print("Accuracy of LogisticRegression is = %g"% (lr_accuracy))
print("Test Error of LogisticRegression = %g " % (1.0 - lr_accuracy))
```

    Accuracy of LogisticRegression is = 0.771277
    Test Error of LogisticRegression = 0.228723 


## DecisionTreeClassifier

### 스무고개를 연상케하는 알고리즘

### 트리구조를 사용하고 각 분기점(NODE)에는 분석 대상의 속성이 위치함

### 가장 높은 정보 획득량(information gain)을 제공하는 속성을 우선적으로 선택하여 분류를 시작함

### 다른 모델들과는 다르게 결과물이 시각적으로 읽히기 쉬운형태로 나타나는 것이 장점


```python
from pyspark.ml.classification import DecisionTreeClassifier
dt = DecisionTreeClassifier(labelCol="Survived", featuresCol="features")
dt_model = dt.fit(trainingData)
dt_prediction = dt_model.transform(testData)
dt_prediction.select("prediction", "Survived", "features").show()
```

    +----------+--------+--------------------+
    |prediction|Survived|            features|
    +----------+--------+--------------------+
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       1.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       1.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,6],[1.0,...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,3,4,5],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|[1.0,58.0,0.0,2.0...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|[2.0,19.0,1.0,1.0...|
    +----------+--------+--------------------+
    only showing top 20 rows


​    

### 평가


```python
dt_accuracy = evaluator.evaluate(dt_prediction)
print("Accuracy of DecisionTreeClassifier is = %g"% (dt_accuracy))
print("Test Error of DecisionTreeClassifier = %g " % (1.0 - dt_accuracy))
```

    Accuracy of DecisionTreeClassifier is = 0.819149
    Test Error of DecisionTreeClassifier = 0.180851 


### RandomForestClassifier

### 의사결정 트리의 오버피팅 한계를 극복하기 위한 전략

### 랜덤 포레스트는 훈련을 통해 구성해놓은 다수의 나무들로부터 분류 결과를 취합해서 결론을 얻는 방식


```python
from pyspark.ml.classification import RandomForestClassifier
rf = DecisionTreeClassifier(labelCol="Survived", featuresCol="features")
rf_model = rf.fit(trainingData)
rf_prediction = rf_model.transform(testData)
rf_prediction.select("prediction", "Survived", "features").show()
```

    +----------+--------+--------------------+
    |prediction|Survived|            features|
    +----------+--------+--------------------+
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       1.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       1.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,6],[1.0,...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,3,4,5],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|[1.0,58.0,0.0,2.0...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|[2.0,19.0,1.0,1.0...|
    +----------+--------+--------------------+
    only showing top 20 rows


​    

### 평가


```python
rf_accuracy = evaluator.evaluate(rf_prediction)
print("Accuracy of RandomForestClassifier is = %g"% (rf_accuracy))
print("Test Error of RandomForestClassifier  = %g " % (1.0 - rf_accuracy))
```

    Accuracy of RandomForestClassifier is = 0.819149
    Test Error of RandomForestClassifier  = 0.180851 


## NaiveBayes

### 나이브 베이즈 분류는 베이즈 정리에 기반한 통계적 분류 기법

### feature 간의 독립성이 있어야 함


```python
from pyspark.ml.classification import NaiveBayes
nb = NaiveBayes(labelCol="Survived", featuresCol="features")
nb_model = nb.fit(trainingData)
nb_prediction = nb_model.transform(testData)
nb_prediction.select("prediction", "Survived", "features").show()
```

    +----------+--------+--------------------+
    |prediction|Survived|            features|
    +----------+--------+--------------------+
    |       1.0|       0|(10,[0,1,4,6,8],[...|
    |       1.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       1.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       1.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,6],[1.0,...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       1.0|       0|(10,[0,1,4,6],[1....|
    |       1.0|       0|(10,[0,1,4,6],[1....|
    |       1.0|       0|(10,[0,1,2,4,5],[...|
    |       1.0|       0|(10,[0,1,3,4,5],[...|
    |       1.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       1.0|       0|[1.0,58.0,0.0,2.0...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       1.0|       0|[2.0,19.0,1.0,1.0...|
    +----------+--------+--------------------+
    only showing top 20 rows


​    

### 평가


```python
nb_accuracy = evaluator.evaluate(nb_prediction)
print("Accuracy of NaiveBayes is  = %g"% (nb_accuracy))
print("Test Error of NaiveBayes  = %g " % (1.0 - nb_accuracy))
```

    Accuracy of NaiveBayes is  = 0.739362
    Test Error of NaiveBayes  = 0.260638 


## Support Vector Machine

### 주어진 데이터가 어느 카테고리에 속할지 판단하는 이진 선형 분류 모델

### 데이터군으로 부터 최대의 마진을 갖도록 결정 경계를 찾아서 분류함 


```python
from pyspark.ml.classification import LinearSVC
svm = LinearSVC(labelCol="Survived", featuresCol="features")
svm_model = svm.fit(trainingData)
svm_prediction = svm_model.transform(testData)
svm_prediction.select("prediction", "Survived", "features").show()
```

    +----------+--------+--------------------+
    |prediction|Survived|            features|
    +----------+--------+--------------------+
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,6],[1.0,...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,3,4,5],[...|
    |       0.0|       0|(10,[0,1,2,4,5],[...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|[1.0,58.0,0.0,2.0...|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6],[1....|
    |       0.0|       0|(10,[0,1,4,6,8],[...|
    |       0.0|       0|[2.0,19.0,1.0,1.0...|
    +----------+--------+--------------------+
    only showing top 20 rows


​    

### 평가


```python
svm_accuracy = evaluator.evaluate(svm_prediction)
print("Accuracy of Support Vector Machine is = %g"% (svm_accuracy))
print("Test Error of Support Vector Machine = %g " % (1.0 - svm_accuracy))
```

    Accuracy of Support Vector Machine is = 0.808511
    Test Error of Support Vector Machine = 0.191489 



```python

```