

# 분석Day14

>  pymysql을 이용한 MariaDB 연동

### - 교육내용

# **pymysql을 이용한 MariaDB 연동**

### connect() 함수를 이용하면 MySQL host내 DB와 직접 연결할 수 있다.

###    user: user name

###    passwd: 설정한 패스워드

###    host: DB가 존재하는 host

###    db: 연결할 데이터베이스 이름

###    charset: 인코딩 설정


```python
import pymysql
conn = pymysql.connect(host='multi-bigdata.cljkqcsbb9ok.ap-northeast-2.rds.amazonaws.com',port=3306,user='edu02',passwd='edu02', db='unicodb')
print(conn)
```


```python
import pymysql
conn = pymysql.connect(host='multi-bigdata.cljkqcsbb9ok.ap-northeast-2.rds.amazonaws.com',port=3306,user='edu02',passwd='edu02', db='unicodb')
try:
    cur = conn.cursor()
    print(type(cur))
    print("-----------------------")
    sql = 'SELECT * FROM emp'
    cur.execute(sql)
    result = cur.fetchall()
    print(type(result))
    print(result)
    print("----------------------------------------------")
    print(type(result[0]))
    print(result[0])
    print("----------------------------------------------")
    print(len(result))
    print(len(result[0]))
    print("----------------------------------------------")
    for row in result:        
        print(f'{row[0]} {row[1]} {row[2]} {row[3]} {row[4]} {row[5]} {row[6]} {row[7]}')
finally:
    conn.close()
```

## Cursor 객체 생성

### 연결한 DB와 상호작용하기 위해 cursor 객체를 생성해주어야 한다.

### 다양한 커서의 종류가 있지만,

### 데이터 분석가에게 익숙한 데이터프레임 형태로 결과를 쉽게 변환할 수 있도록

### **딕셔너리** 형태로 결과를 반환해주는 **DictCursor**객체를 주로 사용한다.

### 일반 **Cursor**객체를 사용하면 결과가 일반적으로는 **튜플** 형태로 리턴된다.

----

### SELECT 명령을 위해 SQL 문을 따로 변수에 넣어주고 cursor.execute(sql) 을 사용해 SQL를 실행한다.

### 실행한 결과를 fetchall(), fetchone() 등으로 받아 온다.

### **fetchall()** - 모든 데이터를 한 번에 가져올 때 사용

### **fetchone()** - 한 번 호출에 하나의 행만 가져올 때 사용

### **fetchmany(n)** - n개만큼의 데이터를 가져올 때 사용


```python
import pymysql
conn = pymysql.connect(host='multi-bigdata.cljkqcsbb9ok.ap-northeast-2.rds.amazonaws.com',port=3306,user='edu02',passwd='edu02', db='unicodb', cursorclass=pymysql.cursors.DictCursor)
try:
    cur = conn.cursor()
    print(type(cur))
    print("-----------------------")
    sql = 'SELECT * FROM emp'
    cur.execute(sql)
    result = cur.fetchall()
    print(type(result))
    print(result)
    print("----------------------------------------------")
    print(type(result[0]))
    print(result[0])
    print("----------------------------------------------")
    print(len(result))
    print(len(result[0]))
    print("----------------------------------------------")
    for row in result:        
        print(f'{row["empno"]} {row["ename"]} {row["job"]} {row["mgr"]} {row["hiredate"]} {row["sal"]} {row["comm"]} {row["deptno"]}')
finally:
    conn.close()
```


```python
import pandas as pd
```


```python
df = pd.DataFrame(result)
df
```


```python
import pymysql

dbServerName    	= "multi-bigdata.cljkqcsbb9ok.ap-northeast-2.rds.amazonaws.com"
dbUser          	= "edu02"
dbPassword      	= "edu02"
dbName          	= "edudb01"
charSet         	= "utf8"
cusrorType      	= pymysql.cursors.DictCursor

connectionObject   = pymysql.connect(host=dbServerName, user=dbUser, password=dbPassword,
                                     db=dbName, charset=charSet,cursorclass=cusrorType)

try:
    cursorObject = connectionObject.cursor()                                     
    sqlQuery = "CREATE TABLE IF NOT EXISTS Employee(id int, LastName varchar(32), FirstName varchar(32), DepartmentCode int)"   
    cursorObject.execute(sqlQuery)
    sqlQuery = "show tables"   
    cursorObject.execute(sqlQuery)
    rows = cursorObject.fetchall()
    for row in rows:
        print(row)

    insertStatement = "INSERT INTO Employee (id, LastName, FirstName, DepartmentCode) VALUES (1,'KIM','JUNGHYUN',10)"   
    cursorObject.execute(insertStatement)
    insertStatement = "INSERT INTO Employee (id, LastName, FirstName, DepartmentCode) VALUES (1,'GO','GILDONG',10)"   
    cursorObject.execute(insertStatement)
    connectionObject.commit()

    sqlQuery = "select * from Employee"   
    cursorObject.execute(sqlQuery)
    rows = cursorObject.fetchall()

    for row in rows:
        print(row)

except Exception as e:
    print("Exeception occured:{}".format(e))
finally:    
    connectionObject.close()
```


```python
import pymysql
conn = pymysql.connect(host='multi-bigdata.cljkqcsbb9ok.ap-northeast-2.rds.amazonaws.com',port=3306,user='edu02',passwd='edu02', db='unicodb')
try:
    cur = conn.cursor()
    sql = 'SELECT * FROM emp'
    cur.execute(sql)
    result = cur.fetchall()
    print(result)
    print("----------------------------------------------")
    sql = 'SELECT * FROM dept'
    cur.execute(sql)
    result = cur.fetchall()
    print(result)
    print("----------------------------------------------")
    sql = 'SELECT * FROM edudb.Employee'
    cur.execute(sql)
    result = cur.fetchall()
    print(result)   
finally:
    conn.close()
```


```python
# 교재 224 페이지 예제 시작
import pymysql
conn = pymysql.connect(host='multi-bigdata.cljkqcsbb9ok.ap-northeast-2.rds.amazonaws.com',port=3306,user='edu02',passwd='edu02', db='edudb')

cur = conn.cursor()
sql = 'SELECT * FROM dataset4'
cur.execute(sql)
result = cur.fetchone()
print(result)
```


```python
#sql = 'SELECT * FROM dataset4'
#cur.execute(sql)
alldata = cur.fetchall()
print(alldata)
```


```python
data = pd.read_sql_query(sql,conn)
```


```python
data
```


```python
data['Sex'] = [1 if x == 'female' else 0 for x in data['Sex']]
```


```python
data
```


```python
M = data.loc[:, ['Survived','Age','SibSp','Parch','Fare','Sex']]
```


```python
M
```


```python
M.corr()
```


```python
import matplotlib.pyplot as plt 
import seaborn as sns  
```


```python
plt.figure(figsize=(15,15))
sns.heatmap(data = M.corr(), annot=True, 
fmt = '.2f', linewidths=.5, cmap='Blues')
plt.show()
```


```python
from matplotlib import font_manager, rc
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
```


```python
plt.figure(figsize=(15,15))
data1=data[data['Survived'] == 1]
ax=sns.countplot(x='Sex',data=data1)
ax.set_title("타이타닉호의 성별 생존자 수", fontsize= 30)
ax.set_xticklabels(['남성','여성'], fontsize=15)
ax.set_xlabel('성별', fontsize= 20) 
ax.set_ylabel('생존자 수', fontsize= 20)  
plt.show()
```


```python
fig, ax = plt.subplots(1,2, figsize = (12, 8))

sns.kdeplot(data[data['Survived'] == 0]['Age'], ax = ax[0])
sns.kdeplot(data[data['Survived'] == 1]['Age'], ax = ax[1])
plt.show()
```


```python
fig, ax = plt.subplots(2,2, figsize = (12, 8))

sns.kdeplot(data[(data['Survived'] == 1) & (data['Sex'] == 0)]['Age'], ax = ax[0,0])
sns.kdeplot(data[(data['Survived'] == 0) & (data['Sex'] == 0)]['Age'], ax = ax[0,1])
sns.kdeplot(data[(data['Survived'] == 1) & (data['Sex'] == 1)]['Age'], ax = ax[1,0])
sns.kdeplot(data[(data['Survived'] == 0) & (data['Sex'] == 1)]['Age'], ax = ax[1,1])
ax[0,0].set_title("여성의 나이별 생존자")
ax[0,1].set_title("여성의 나이별 사망자")
ax[1,0].set_title("남성의 나이별 생존자")
ax[1,1].set_title("남성의 나이별 사망자")
plt.show()
```


```python
sql = 'SELECT Sex, count(*) cnt FROM dataset4 where Survived = 1.0 group by Sex'
data = pd.read_sql_query(sql,conn)
data
```


```python
plt.figure(figsize=(15,15))
ax=sns.barplot(data=data, x="Sex", y= "cnt")
ax.set_title("타이타닉호의 성별 생존자 수", fontsize= 30)
ax.set_xticklabels(['여성','남성'], fontsize=15)
ax.set_xlabel('성별', fontsize= 20) 
ax.set_ylabel('생존자 수', fontsize= 20)  
plt.show()
```


```python
conn = pymysql.connect(host='multi-bigdata.cljkqcsbb9ok.ap-northeast-2.rds.amazonaws.com',port=3306,user='edu21',passwd='edu21', db='edudb')

cur = conn.cursor()
sql = 'SELECT * FROM dataset4'
cur.execute(sql)
result = cur.fetchone()
print(result)
```