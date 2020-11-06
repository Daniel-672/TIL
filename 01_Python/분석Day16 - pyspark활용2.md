

# 분석Day16

>  pyspark활용2

### - 교육내용

# **pyspark 패키지를 활용한 Spark 프로그래밍**



### [PySpark API 도큐먼트](https://spark.apache.org/docs/latest/api/python/index.html)

# **pyspark 패키지를 활용한 Spark 프로그래밍(2)**

## SparkSession 객체 생성


```python
import pyspark
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[2]") \
                    .appName('sparkedu') \
                    .getOrCreate()
spark
```


```python
# print(spark.stop())
```

## <span style='color:red'>**RDD**</span>

### Resilient Distributed Dataset의 약자(탄력 분산 데이터셋)

### 분산되어 존재하는 데이터들의 모임, 즉 클러스터에 분배되어 있는 데이터들을 하나로 관리하는 개념

### 스파크의 모든 데이터 타입들은 RDD를 기반으로 만들어지고 데이터끼리의 연산들은 RDD의 연산으로 이루어져 있음


```python
greetRDD = spark.sparkContext.textFile('data/greeting.txt')
print(greetRDD)
greetRDD.collect()
print(type(greetRDD))
```


```python
goodLines = greetRDD.filter(lambda x : "Good" in x)
goodLines.collect()
# print(type(goodLines.collect()))
```


```python
goodLines.count()
```


```python
numbers = spark.sparkContext.parallelize(list(range(5)))
squared = numbers.map(lambda x : x * x).collect()
squared
```


```python
strings = spark.sparkContext.parallelize(["hello spark", "hi python"])
splitted = strings.flatMap(lambda x : x.split(" ")).collect()
print(splitted)
splitted1 = strings.map(lambda x : x.split(" ")).collect()
print(splitted1)
```


```python
numbers = spark.sparkContext.parallelize(list(range(1, 30, 3)))
result = numbers.filter(lambda x : x % 2 == 0).collect()
result
```


```python
linesRDD = spark.sparkContext.parallelize(["test", "this is a test rdd"])
linesRDD
```

## <span style='color:red'>**페어 RDD**</span>

### 페어 RDD란 key-value쌍으로 이루어진 RDD

### 파이썬에서는 Tuple로 이뤄진 RDD가 곧 페어 RDD가 됨


```python
examplePairRDD = spark.sparkContext.parallelize([(1, 3), (1, 5), (2, 4), (3, 3), (4, 8), (4, 2), (3, 1)])
print(examplePairRDD)
examplePairRDD.collect()
```

## *- PairRDD에서 주로 사용하는메소드* 

- reduceByKey(func) : 동일 키에 대한 값들을 reduce(예 : rdd.reduceByKey(lambda x, y: x + y))
- mapValues(func) : 각 키에 대해 연산을 적용(예 : rdd.mapValues(lambda x : x + 1))
- sortByKey() : 키로 정렬한 RDD 리턴(예 : rdd.sortByKey())
- groupByKey() : 키로 grouping
- keys() : 키값들을 리턴(예 : rdd.keys())
- values() : value값들을 리턴(예 : rdd.values())


```python
examplePairRDD.reduceByKey(lambda x, y : x + y).collect()
```


```python
examplePairRDD.mapValues(lambda x: x**2).collect()
```


```python
customerLines = spark.sparkContext.textFile("data/name-customers.csv")
print(type(customerLines))
customerLines.take(2)
```


```python
customerPairs = customerLines.map(lambda x: (x.split(",")[1], x.split(",")[0]))
customerPairs.take(2)
```


```python
customerPairCollected = customerPairs.groupByKey().collect()
print(customerPairCollected)
# print(customers)
customerDict = {
    country : [c for c in customers]
        for country, customers in customerPairCollected
}
print(customerDict)
customerDict['UK']
```


```python
[k for k in customerPairs.sortByKey().keys().collect()][:10]
```


```python
mapReduced = customerPairs.mapValues(lambda x : 1).reduceByKey(lambda x, y: x + y)
print(mapReduced.collect())
{
    i:j for i, j in mapReduced.collect()
}
```

## RDD를 가지고 워드카운팅하는 예제


```python
lines = spark.sparkContext.textFile("data/greeting.txt")
sorted(lines.flatMap(lambda line: line.split()).map(lambda w: (w,1)).reduceByKey(lambda v1, v2: v1+v2).collect())
```


```python
rdd1 = spark.sparkContext.textFile("data/greeting.txt")
print(type(rdd1))
print(rdd1)
print(rdd1.collect())
print("--------------------------------------1----------------------------------------")
rdd2 = rdd1.flatMap(lambda line: line.split())
print(type(rdd2))
print(rdd2)
print(rdd2.collect())
print("--------------------------------------2----------------------------------------")
rdd3 = rdd2.map(lambda w: (w,1))
print(type(rdd3))
print(rdd3)      
print(rdd3.collect())
print("-------------------------------------3-----------------------------------------")
rdd4 = rdd3.reduceByKey(lambda v1, v2: v1+v2)
print(type(rdd4))
print(rdd4)
print(rdd4.collect())
print("-------------------------------------4-----------------------------------------")
result = rdd4.collect()
print(type(result))
print(result)
print("-------------------------------------5-----------------------------------------")
print(sorted(result))
```

## 파일 로딩(JSON, CSV)


```python
import json
carsJson = spark.sparkContext.textFile("./data/cars.json") \
              .map(lambda x: json.loads(x))
carsJson
```


```python
carsJson.first()
```


```python
carsJson.collect()
```

## RDD를 가지고 Hive가상테이블 생성 ~> SQL을 사용해서 데이터 처리


```python
emp = spark.read.csv("data/emp.csv", header=True, inferSchema=True)
print(type(emp))
```


```python
from pyspark.sql import HiveContext
hiveCtx = HiveContext(spark.sparkContext)
```


```python
emp.registerTempTable("hiveemp")
emp
```


```python
empResult = hiveCtx.sql("SELECT ename, sal FROM hiveemp")
empResult.collect()[:5]
```


```python
empResult = hiveCtx.sql("SELECT * FROM hiveemp order by sal")
empResult.collect()
```


```python
empResult.filter(empResult.empno==7369).show()
```

## RDD를 가지고 임시뷰 생성 ~> SQL을 사용해서 데이터 처리


```python
emp.createOrReplaceTempView("empview")
```


```python
sparkdf = spark.sql("select * from empview")
print(type(sparkdf))
sparkdf.show()
```


```python
spark.sql("select * from empview where sal > 2000").show()
```


```python
spark.sql("select deptno, sum(sal), max(sal) from empview group by deptno").show()
```


```python
spark.sql("select * from empview where sal > 2000").show()
```


```python
spark.sql("select * from empview order by sal desc").show()
```


```python
spark.sql("select * from empview order by sal desc").take(1)
```


```python
spark.sql("select * from empview order by sal desc").take(2)[0][1]
```


```python
spark.sql("select * from empview order by sal desc").take(1)[0]['ename']
```

![이미지](C:/Users/Daniel/Downloads/images/spark_df.png)

## Row 객체


```python
from pyspark.sql import Row
row=Row("James",40)
print(row[0] +","+str(row[1]))
```


```python
row=Row(name="Alice", age=11)
print(row.name)
```


```python
Person = Row("name", "age")
p1=Person("James", 40)
p2=Person("Alice", 35)
print(p1.name +","+ str(p2.age))
```


```python
from pyspark.sql import Row

data = [Row(name="James,,Smith",lang=["Java","Scala","C++"],state="CA"), 
    Row(name="Michael,Rose,",lang=["Spark","Java","C++"],state="NJ"),
    Row(name="Robert,,Williams",lang=["CSharp","VB"],state="NV")]
rdd=spark.sparkContext.parallelize(data)
print(rdd.collect())
```


```python
collData=rdd.collect()
for row in collData:
    print(row.name + "," +str(row.lang))
```

## 날짜데이터를 처리하자


```python
import pyspark.sql.functions as f
```


```python
# f.mean(1, 2, 3,)
```


```python
l1 = [('2019-05-22',342),('2020-06-02',334),('2019-09-30',269),('2020-10-10',342),('2020-12-25',342)]
dfl1 =  spark.createDataFrame(l1).toDF("dates","sum")
dfl1.show()
```


```python
from pyspark.sql.functions import col
dfl2 = dfl1.withColumn('years',f.year(f.to_timestamp('dates', 'yyyy-MM-dd')))
dfl2 = dfl2.withColumn("month",f.month(f.to_timestamp('dates', 'yyyy-MM-dd')))
dfl2 = dfl2.withColumn("dayofmonth",f.dayofmonth(f.to_timestamp('dates', 'yyyy-MM-dd')))
dfl2.show()
```


```python
dfl2 = dfl1.withColumn('years',f.year(f.to_timestamp('dates')))
dfl2 = dfl2.withColumn("month",f.month(f.to_timestamp('dates')))
dfl2 = dfl2.withColumn("dayofmonth",f.dayofmonth(f.to_timestamp('dates')))
dfl2.show()
```


```python
dfl2.groupBy('years').sum('sum').show()
```

## NoneType 필터링

### pyspark에서 drop method는 NULL을 가진 행을 제거하는데 가장 간단한 함수다. 

### [drop 메소드에 인수]

### any: 모든 행의 컬럼값 중 하나라도 NULL의 값을 가지면 해당 행을 제거

### all: 모든 컬럼 값이 NULL이거나 NaN인 경우에만 해당 행을 제거


```python
import pyspark.sql.functions as f

```


```python
df = spark.createDataFrame([
    (1,'A','X1'),(2,None,'X2'),(2,'B','X2'),(2,'','X1'),(None,'','X3'),(1,'C','X1'),(2,None,'X1'),(2,'D',None),(None,None,None)
], ["ID", "TYPE", "CODE"])
df.show()
```


```python
df.na.drop('any').show()
```


```python
df.na.drop('all').show()
```


```python
df.na.drop('all', subset=['TYPE', 'CODE']).show()
```


```python
df.na.drop('any', subset=['TYPE', 'CODE']).show()
```


```python
df.show()
```


```python
from decimal import Decimal

data = [{"Category": 'Category A', "ID": 1, "Value": Decimal(12.40)},
        {"Category": 'Category B', "ID": 2, "Value": Decimal(30.10)},
        {"Category": 'Category C', "ID": 3, "Value": None},
        {"Category": 'Category D', "ID": 4, "Value": Decimal(1.0)},
        ]

# Create data frame
df = spark.createDataFrame(data)
df.show()
```


```python
from decimal import Decimal

data = [Row(Category='Category A', ID=1, Value= Decimal(12.40)),
        Row(Category='Category B', ID=2, Value= Decimal(30.10)),
        Row(Category='Category C', ID=3, Value= None),
        Row(Category='Category D', ID=4, Value= Decimal(1.0)),
        ]

# Create data frame
df = spark.createDataFrame(data)
df.show()
```


```python
df.filter("Value is not null").show()
```


```python
df.where("Value is null").show()
```


```python
df.filter(df['Value'].isNull()).show()
```


```python
df.where(df.Value.isNotNull()).show()
```

## 날짜타입 데이터 처리


```python
emp = spark.read.csv("data/emp.csv", header=True, inferSchema=True)
```


```python
emp.columns
```


```python
emp.dtypes
```


```python
from pyspark.sql.functions import col
newemp = emp.withColumn("hiredate",col("hiredate").cast("Date"))
newemp.printSchema()
```


```python
newemp.select(f.year(newemp["hiredate"])).show()
```


```python
newemp.select(f.month(newemp["hiredate"])).show()
```


```python
newemp.select(f.dayofmonth(newemp["hiredate"])).show()
```

## 날짜타입 데이터 처리


```python
flightData2015 = spark\
          .read\
          .option("inferSchema", "true")\
          .option("header", "true")\
          .csv("data/flight-data/csv/2015-summary.csv")
```


```python
flightData2015.createOrReplaceTempView("flight_data_2015")
```


```python
sqlWay = spark.sql("""
SELECT DEST_COUNTRY_NAME, count(*)
FROM flight_data_2015
GROUP BY DEST_COUNTRY_NAME
""")
sqlWay.show()
```


```python
dataFrameWay = flightData2015\
  .groupBy("DEST_COUNTRY_NAME")\
  .count()
dataFrameWay.show()
```


```python
from pyspark.sql.functions import max

flightData2015.select(max("count")).take(1)
```


```python
maxSql = spark.sql("""
SELECT DEST_COUNTRY_NAME, sum(count) as destination_total
FROM flight_data_2015
GROUP BY DEST_COUNTRY_NAME
ORDER BY sum(count) DESC
LIMIT 5
""")

maxSql.show()
```


```python
from pyspark.sql.functions import desc

flightData2015\
  .groupBy("DEST_COUNTRY_NAME")\
  .sum("count")\
  .withColumnRenamed("sum(count)", "destination_total")\
  .sort(desc("destination_total"))\
  .limit(5)\
  .show()
```

## 다중 파일도 한방에 읽을 수 있지요...


```python
staticDataFrame = spark.read.format("csv")\
  .option("header", "true")\
  .option("inferSchema", "true")\
  .load("data/retail-data/by-day/*.csv")

staticDataFrame.createOrReplaceTempView("retail_data")
staticSchema = staticDataFrame.schema
```


```python
staticSchema
```


```python
staticDataFrame.count()
```


```python
spark.sql("select * from retail_data").show()
```


```python
spark.sql("select * from retail_data where InvoiceDate > ''").show()
```

## 윈도우함수(랭킹함수) 활용


```python
simpleData = (("James", "Sales", 3000), \
    ("Michael", "Sales", 4600),  \
    ("Robert", "Sales", 4100),   \
    ("Maria", "Finance", 3000),  \
    ("Scott", "Finance", 3300),  \
    ("Jen", "Finance", 3900),    \
    ("Jeff", "Marketing", 3000), \
    ("Kumar", "Marketing", 2000),\
    ("Saif", "Sales", 4100) \
  )
 
columns= ["employee_name", "department", "salary"]
df = spark.createDataFrame(data = simpleData, schema = columns)
df.printSchema()
df.show(truncate=False)
```


```python
from pyspark.sql.window import Window
from pyspark.sql.functions import row_number
windowSpec  = Window.partitionBy("department").orderBy("salary")

df.withColumn("row_number",row_number().over(windowSpec)) \
    .show(truncate=False)
```


```python
from pyspark.sql.functions import rank
df.withColumn("rank",rank().over(windowSpec)) \
    .show()
```


```python
from pyspark.sql.functions import dense_rank
df.withColumn("dense_rank",dense_rank().over(windowSpec)) \
    .show()
```

## 웹사이트에서 데이터 읽어오기


```python
from pyspark import SparkFiles

spark.sparkContext.addFile("https://raw.githubusercontent.com/guru99-edu/R-Programming/master/adult_data.csv")
df = spark.read.csv(SparkFiles.get("adult_data.csv"), header=True, inferSchema=True)
```


```python
df.printSchema ()
```


```python
df.show(5, truncate = False)
```


```python
df.select('age','fnlwgt').show(5)
```


```python
df.groupBy("education").count().sort("count",ascending=True).show()
```


```python
df.describe().show()
```


```python
df.describe("capital-gain").show()
```


```python
df.filter(df.age > 40).count()
```

## 다양한 집계(aggregation) 함수들


```python
import pyspark
from pyspark.sql import SparkSession
from pyspark.sql.functions import approx_count_distinct,collect_list
from pyspark.sql.functions import collect_set,sum,avg,max,countDistinct,count
from pyspark.sql.functions import first, last, kurtosis, min, mean, skewness 
from pyspark.sql.functions import stddev, stddev_samp, stddev_pop, sumDistinct
from pyspark.sql.functions import variance,var_samp,  var_pop

simpleData = [
    ("Michael", "Sales", 4600),
    ("Robert", "Sales", 4100),
    ("Maria", "Finance", 3000),
    ("James", "Sales", 3000),
    ("Scott", "Finance", 3300),
    ("Jen", "Finance", 3900),
    ("Jeff", "Marketing", 3000),
    ("Kumar", "Marketing", 2000),
    ("Saif", "Sales", 4100)
  ]
schema = ["employee_name", "department", "salary"]
  
df = spark.createDataFrame(data=simpleData, schema = schema)
df.printSchema()
df.show(truncate=False)

print("approx_count_distinct: " + \
      str(df.select(approx_count_distinct("salary")).collect()[0][0]))

print("avg: " + str(df.select(avg("salary")).collect()[0][0]))

df.select(collect_list("salary")).show(truncate=False)

df.select(collect_set("salary")).show(truncate=False)

df2 = df.select(countDistinct("department", "salary"))
df2.show(truncate=False)
print("Distinct Count of Department & Salary: "+str(df2.collect()[0][0]))

print("count: "+str(df.select(count("salary")).collect()[0]))
df.select(first("salary")).show(truncate=False)
df.select(last("salary")).show(truncate=False)
df.select(kurtosis("salary")).show(truncate=False)
df.select(max("salary")).show(truncate=False)
df.select(min("salary")).show(truncate=False)
df.select(mean("salary")).show(truncate=False)
df.select(skewness("salary")).show(truncate=False)
df.select(stddev("salary"), stddev_samp("salary"), \
    stddev_pop("salary")).show(truncate=False)
df.select(sum("salary")).show(truncate=False)
df.select(sumDistinct("salary")).show(truncate=False)
df.select(variance("salary"),var_samp("salary"),var_pop("salary")) \
  .show(truncate=False)
```

## UDF(User Defined Function) 활용


```python
emp
```


```python
def detGreade(sal):
    Q = 'E'
    if(sal > 4000):
        Q = 'A'
    elif(sal > 3000):
        Q = 'B'
    elif(sal > 2000):
        Q = 'C'
    elif(sal > 1000):
        Q = 'D'
    return Q
```


```python
from pyspark.sql.functions import udf
from pyspark.sql.types import StringType

grade = udf(detGreade, StringType())                # 2번째 argument는 return type
```


```python
newemp = emp.withColumn("grade", grade('sal'))
newemp.show()
```


```python
columns = ["Seqno","Name"]
data = [("1", "john jones"),
    ("2", "tracey smith"),
    ("3", "amy sanders")]

df = spark.createDataFrame(data=data,schema=columns)

df.show(truncate=False)
```


```python
def convertCase(str):
    resStr=""
    arr = str.split(" ")
    for x in arr:
       resStr= resStr + x[0:1].upper() + x[1:len(x)] + " "
    return resStr 

convertUDF = udf(lambda z: convertCase(z))

df.select(col("Seqno"), \
    convertUDF(col("Name")).alias("Name") ) \
.show(truncate=False)
```