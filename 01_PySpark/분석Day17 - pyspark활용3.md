

# 분석Day17

>  pyspark활용3

### - 교육내용

## SparkSession 객체 생성 : Spark 기동과 초기화


```python
import pyspark
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[2]") \
                    .appName('sparkedu') \
                    .getOrCreate()
spark
```

### Spark을 사용하여 hotel.txt파일의 내용으로 텍스트 마이닝을 해보자~

#### hotel.txt 파일에서 가장 많이 등장한 명사들을 많이 등장한 순으로 30개를 출력해 본다. 


```python
hoteldf = spark.read.text("data/hotel.txt") 
hoteldf.show(3)
```


```python
print(hoteldf.take(3))
```


```python
imsi = hoteldf.collect()
print(imsi[:3])
```


```python
hotellist = [ x[0] for x in imsi ]
print(hotellist[:3])
```


```python
hotelstr = ' '.join(hotellist)
print(hotelstr[:50])
```


```python
import re

hangul = re.compile('[^ ㄱ-ㅣ가-힣]+') 
hangul.sub('', hotelstr) # 한글과 띄어쓰기를 제외한 모든 부분을 제거
```


```python
from konlpy.tag import Okt                                  ## 다른 형태소를 클래스를 가져온다. 
okt = Okt()
hotelnoun = okt.nouns(hotelstr)
print(hotelnoun[:50])
```


```python
hotelRDD = spark.sparkContext.parallelize(hotelnoun)
```


```python
wc = hotelRDD.flatMap(lambda x: x.split(' ')) \
                  .map(lambda x: (x, 1)) \
                  .reduceByKey(lambda x1, x2: x1 + x2) \
                  .map(lambda x: (x[1], x[0])) \
                  .sortByKey(ascending=False).collect()

for (count, word) in wc[:30]:
    print("{} : {}".format(word, count))
    
```

### Spark를 활용하여 product_click_new.log 파일로 날짜 데이터에 대한 전처리를 처리해보자~


```python
click = spark.read.csv("data/product_click_new.log", sep=" ", inferSchema=True)
```


```python
click.show(30)
```


```python
click = click.withColumnRenamed("_c0", "clicktime")\
       .withColumnRenamed("_c1", "pid")
click.show(30)
```


```python
click.printSchema()
```


```python
from pyspark.sql.functions import col
from pyspark.sql.functions import StringType
click = click.withColumn("clicktime",col("clicktime").cast(StringType()))
```


```python
click.printSchema()
```


```python
import pyspark.sql.functions as f
click = click.withColumn('year',f.year(f.to_timestamp('clicktime', 'yyyyMMddhhmm')))
click = click.withColumn("month",f.month(f.to_timestamp('clicktime', 'yyyyMMddhhmm')))
click = click.withColumn("day",f.dayofmonth(f.to_timestamp('clicktime', 'yyyyMMddhhmm')))
click = click.withColumn("hour",f.hour(f.to_timestamp('clicktime', 'yyyyMMddhhmm')))
click = click.withColumn("minute",f.minute(f.to_timestamp('clicktime', 'yyyyMMddhhmm')))
```


```python
click.show(100)
```


```python
click.groupby("hour").count().show()
```


```python
click.select(f.hour(f.to_timestamp(click.clicktime, 'yyyyMMddhhmm')).alias('dt')).groupby('dt').count().show()
```

## Spark을 사용하여 타이타닉 데이터셋의 데이터 전처리를 처리해보자~


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


```python
titanic_df.show(5)
```


```python
titanic_df.describe().show()
```


```python
titanic_df.printSchema()
```


```python
titanic_df.select("Survived","Pclass","Embarked").show()
```

## 자~ EDA(Exploratory Data Analysis)를 해봅시다요.


```python
titanic_df.groupBy("Survived").count().show()
```


```python
titanic_df.groupBy("Sex","Survived").count().show()
```


```python
titanic_df.groupBy("Pclass","Survived").count().show()
```


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


```python
spark.createDataFrame(null_columns_count_list, ['Column_With_Null_Value', 'Null_Values_Count']).show()
```


```python
mean_age = titanic_df.select(mean('Age')).collect()[0][0]
print(mean_age)
```


```python
titanic_df = titanic_df.withColumn("Initial",regexp_extract(col("Name"),"([A-Za-z]+)\.",1))
```


```python
aa = titanic_df.withColumn("aa",regexp_extract(col("Name"),"([A-Za-z]+)\.",0))
aa.show()
```


```python
df = spark.createDataFrame([('100-200',)], ['str'])
df.select(regexp_extract('str', r'(\d+)-(\d+)', 2).alias('d')).collect()
```


```python
titanic_df.show()
```


```python
titanic_df.select("Initial").distinct().show()
```


```python
titanic_df = titanic_df.replace(['Mlle','Mme', 'Ms', 'Dr','Major','Lady','Countess','Jonkheer','Col','Rev','Capt','Sir','Don'],
               ['Miss','Miss','Miss','Mr','Mr',  'Mrs',  'Mrs',  'Other',  'Other','Other','Mr','Mr','Mr'])
```


```python
titanic_df.show()
```


```python
titanic_df.select("Initial").distinct().show()
```


```python
titanic_df.groupby('Initial').avg('Age').collect()
```


```python
titanic_df.filter(titanic_df.Age==46).select("Initial").show()
```


```python
titanic_df.select("Age").show()
```


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


```python
titanic_df = titanic_df.na.fill({"Embarked" : 'S'})
```


```python
titanic_df = titanic_df.drop("Cabin")
```


```python
titanic_df.printSchema()
```


```python
titanic_df = titanic_df.withColumn("Family_Size",col('SibSp')+col('Parch'))
```


```python
titanic_df.show()
```


```python
titanic_df.groupBy("Family_Size").count().show()
```


```python
titanic_df = titanic_df.withColumn('Alone',lit(0))
```


```python
titanic_df = titanic_df.withColumn("Alone",when(titanic_df["Family_Size"] == 0, 1).otherwise(titanic_df["Alone"]))
```


```python
titanic_df.columns
```


```python
indexers = [StringIndexer(inputCol=column, outputCol=column+"_index").fit(titanic_df) for column in ["Sex","Embarked","Initial"]]
pipeline = Pipeline(stages=indexers)
titanic_df = pipeline.fit(titanic_df).transform(titanic_df)
```


```python
titanic_df.show()
```


```python
titanic_df.printSchema()
```


```python
titanic_df = titanic_df.drop("PassengerId","Name","Ticket","Cabin","Embarked","Sex","Initial")
```


```python
titanic_df.show()
```


```python

```