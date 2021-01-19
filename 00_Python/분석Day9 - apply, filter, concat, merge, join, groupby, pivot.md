

# 분석Day09

>  apply, filter, concat, merge, join, groupby, pivot

### - 교육내용

```python
# 예제 6-1
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]
df['ten'] = 10
print(df.head())
print('\n')

# 사용자 함수 정의
def add_10(n):   # 10을 더하는 함수
    return n + 10

def add_two_obj(a, b):    # 두 객체의 합
    return a + b

print(add_10(10))
print(add_two_obj(10, 10))
print('\n')

# 시리즈 객체에 적용
sr1 = df['age'].apply(add_10)               # n = df['age']의 모든 원소
print(sr1.head())
print('\n')
  
# 시리즈 객체와 숫자에 적용 : 2개의 인수(시리즈 + 숫자)
sr2 = df['age'].apply(add_two_obj, b=10)    # a=df['age']의 모든 원소, b=10
print(sr2.head())
print('\n')

# 람다 함수 활용: 시리즈 객체에 적용
sr3 = df['age'].apply(lambda x: add_10(x))  # x=df['age']
print(sr3.head())

```


```python
# 예제 6-2
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]
print(df.head())
print('\n')

# 사용자 함수 정의
def add_10(n):   # 10을 더하는 함수
    return n + 10
    
# 데이터프레임에 applymap()으로 add_10() 함수를 매핑 적용
df_map = df.applymap(add_10)   
print(df_map.head())

```


```python
# 예제 6-3
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]
print(df.head())
print('\n')

# 사용자 함수 정의
def missing_value(series):    # 시리즈를 인수로 전달
    return series.isnull()    # 불린 시리즈를 반환
    
# 데이터프레임의 각 열을 인수로 전달하면 데이터프레임을 반환
result = df.apply(missing_value, axis=0)  
print(result.head())
print('\n')
print(type(result))
```


```python
# 예제 6-4
# 라이브러리 불러오기
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]
print(df.head())
print('\n')

# 사용자 함수 정의
def min_max(x):    # 최대값 - 최소값
    return x.max() - x.min()
    
# 데이터프레임의 각 열을 인수로 전달하면 시리즈를 반환
result = df.apply(min_max)   #기본값 axis=0 
print(result)
print('\n')
print(type(result))
```


```python
# 예제 6-5
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]
df['ten'] = 10
print(df.head())
print('\n')

# 사용자 함수 정의
def add_two_obj(a, b):    # 두 객체의 합
    return a + b
    
# 데이터프레임의 2개 열을 선택하여 적용
# x=df, a=df['age'], b=df['ten']
df['add'] = df.apply(lambda x: add_two_obj(x['age'], x['ten']), axis=1)   
print(df.head())
```


```python
# 예제 6-6
import seaborn as sns

# titanic 데이터셋에서 age, fare 2개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','fare']]

# 각 열의 NaN 찾기 - 데이터프레임 전달하면 데이터프레임을 반환
def missing_value(x):    
    return x.isnull()    

# 각 열의 NaN 개수 반환 - 데이터프레임 전달하면 시리즈 반환
def missing_count(x):    # 
    return missing_value(x).sum()

# 데이터프레임의 총 NaN 개수 - 데이터프레임 전달하면 값을 반환
def totoal_number_missing(x):    
    return missing_count(x).sum()
    
# 데이터프레임에 pipe() 메소드로 함수 매핑
result_df = df.pipe(missing_value)   
print(result_df.head())
print(type(result_df))
print('\n')

result_series = df.pipe(missing_count)   
print(result_series)
print(type(result_series))
print('\n')

result_value = df.pipe(totoal_number_missing)   
print(result_value)
print(type(result_value))
```


```python
df = pd.DataFrame({'a': [10, 20, 30], 'b': [20, 30, 40]}) 
display(df)
```


```python
def print_me(x): 
    print("\n")
    print("***"+str(x)+"***")
    print("\n")
```


```python
print(df.apply(print_me, axis=0))
```


```python
print(df.apply(print_me, axis=1))
```


```python
import seaborn as sns

titanic = sns.load_dataset("titanic")
print(titanic.info())
```


```python
import numpy as np

def count_missing(vec):
    null_vec = pd.isnull(vec)
    null_count = np.sum(null_vec)
    return null_count
```


```python
cmis_col = titanic.apply(count_missing)
print(cmis_col)
```


```python
def prop_missing(vec):
    num = count_missing(vec)
    dem = vec.size
    return num / dem
```


```python
pmis_col = titanic.apply(prop_missing)
print(pmis_col)
```


```python
# 예제 6-7
import seaborn as sns

# titanic 데이터셋의 부분을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[0:4, 'survived':'age']
print(df, '\n')

# 열 이름의 리스트 만들기
columns = list(df.columns.values)   #기존 열 이름
print(columns, '\n')

# 열 이름을 알파벳 순으로 정렬하기
columns_sorted = sorted(columns)    #알파벳 순으로 정렬
df_sorted = df[columns_sorted]
print(df_sorted, '\n')

# 열 이름을 기존 순서의 정반대 역순으로 정렬하기
columns_reversed = list(reversed(columns))  
df_reversed = df[columns_reversed]
print(df_reversed, '\n')

# 열 이름을 사용자가 정의한 임의의 순서로 재배치하기
columns_customed = ['pclass', 'sex', 'age', 'survived']  
df_customed = df[columns_customed]
print(df_customed)

```


```python
# 예제 6-8
import pandas as pd

# 데이터셋 가져오기
df = pd.read_excel('./data/주가데이터.xlsx')
print(df.head(), '\n')
print(df.dtypes, '\n')

# 연, 월, 일 데이터 분리하기
df['연월일'] = df['연월일'].astype('str')   # 문자열 메소드 사용을 자료형 변경
print(df.head(), '\n')
dates = df['연월일'].str.split('-')        # 문자열을 split() 메서드로 분리
print(dates.head(), '\n')

# 분리된 정보를 각각 새로운 열에 담아서 df에 추가하기
df['연'] = dates.str.get(0)     # dates 변수의 원소 리스트의 0번째 인덱스 값
df['월'] = dates.str.get(1)     # dates 변수의 원소 리스트의 1번째 인덱스 값 
df['일'] = dates.str.get(2)     # dates 변수의 원소 리스트의 2번째 인덱스 값
print(df.head())
```


```python
df = pd.DataFrame(np.array(([1, 2, 3], [4, 5, 6])),
                  index=['mouse', 'rabbit'],
                  columns=['one', 'two', 'three'])

df 
```


```python
df.filter(items=['one', 'three'])
```


```python
df.filter(regex='e$', axis=1)
```


```python
df.filter(regex='t$', axis=0)
```


```python
df.filter(like='bbi', axis=0)
```


```python
df.filter(like='e', axis=1)
```


```python
df.loc[[True,True], :]
```


```python
df.loc[[True,False], :]
```


```python
df.loc[[False, False], :]
```


```python
df.loc[df.one > 2, :]
```


```python
df.loc[(df.one > 2) & (df.three > 2), :]
```


```python
df.loc[(df.one < 5) | (df.three > 2), :]
```


```python
# 예제 6-9
import seaborn as sns

# titanic 데이터셋 로딩
titanic = sns.load_dataset('titanic')

# 나이가 10대(10~19세)인 승객만 따로 선택
mask1 = (titanic.age >= 10) & (titanic.age < 20)
df_teenage = titanic.loc[mask1, :]
print(df_teenage.head())
print('\n')

# 나이가 10세 미만(0~9세)이고 여성인 승객만 따로 선택
mask2 = (titanic.age < 10) & (titanic.sex == 'female')
df_female_under10 = titanic.loc[mask2, :]
print(df_female_under10.head())
print('\n')

# 나이가 10세 미만(0~9세) 또는 60세 이상인 승객의 age, sex, alone 열만 선택
mask3 = (titanic.age < 10) | (titanic.age >= 60)
df_under10_morethan60 = titanic.loc[mask3, ['age', 'sex', 'alone']]
print(df_under10_morethan60.head())
```


```python
# 예제 6-10
import seaborn as sns
import pandas as pd

# titanic 데이터셋 로딩
titanic = sns.load_dataset('titanic')

# IPyhton 디스플레이 설정 변경 - 출력할 최대 열의 개수
pd.set_option('display.max_columns', 10)  
    
# 함께 탑승한 형제 또는 배우자의 수가 3, 4, 5인 승객만 따로 추출 - 불린 인덱싱
mask3 = titanic['sibsp'] == 3
mask4 = titanic['sibsp'] == 4
mask5 = titanic['sibsp'] == 5
df_boolean = titanic[mask3 | mask4 | mask5]
print(df_boolean.head())
print('\n')

# isin() 메서드 활용하여 동일한 조건으로 추출
isin_filter = titanic['sibsp'].isin([3, 4, 5])
df_isin = titanic[isin_filter]
print(df_isin.head())

```


```python
df1 = pd.DataFrame({'key': ['a','b','c','f'], 
                    'c1':[1,2,3,5]})
df2 = pd.DataFrame({'key': ['a','b','d','f'],
                    'c2':[5,6,7,8]})
```


```python
df1.merge(df2)
```


```python
df1.merge(df2, how='left')
```


```python
df1.merge(df2, how='right')
```


```python
df1.merge(df2, how="outer")
```


```python
df3 = pd.DataFrame({'key3': ['a','b','c','f'],
                    'c1':[1,2,3,5]})
df4 = pd.DataFrame({'key4': ['a','b','d','f'],
                    'c2':[5,6,7,8]})
```


```python
df3.merge(df4, left_on='key3', right_on='key4')
```


```python
df3.merge(df4, left_index=True, right_index=True)
```


```python
df1 = pd.DataFrame({'c1': [1,2,3,4], 'c2': [5,6,7,8]})
df2 = pd.DataFrame({'c3': ['a','b','c','d'],
                    'c4': [1.2,3.4,5.5,7.6]})
```


```python
pd.concat([df1,df2], axis=1)
```


```python
pd.concat([df1,df2], axis=0)
```


```python
df1 = pd.DataFrame({'c1': [1,2,3,4], 
                    'c2': [5,6,7,8]},
                   index=[0,2,4,6])
df2 = pd.DataFrame({'c3': ['a','b','c','d'],
                    'c4': [1.2,3.4,5.5,7.6]},
                   index=[0,1,2,3])
```


```python
pd.concat([df1, df2], axis=1)
```


```python
# 예제 6-11
import pandas as pd

# 데이터프레임 만들기
df1 = pd.DataFrame({'a': ['a0', 'a1', 'a2', 'a3'],
                    'b': ['b0', 'b1', 'b2', 'b3'],
                    'c': ['c0', 'c1', 'c2', 'c3']},
                    index=[0, 1, 2, 3])
 
df2 = pd.DataFrame({'a': ['a2', 'a3', 'a4', 'a5'],
                    'b': ['b2', 'b3', 'b4', 'b5'],
                    'c': ['c2', 'c3', 'c4', 'c5'],
                    'd': ['d2', 'd3', 'd4', 'd5']},
                    index=[2, 3, 4, 5])

print(df1, '\n')
print(df2, '\n')

# 2개의 데이터프레임을 위 아래 행 방향으로 이어 붙이듯 연결하기 
result1 = pd.concat([df1, df2])
print(result1, '\n')


# ignore_index=True 옵션 설정하기 
result2 = pd.concat([df1, df2], ignore_index=True)
print(result2, '\n')

# 2개의 데이터프레임을 좌우 열 방향으로 이어 붙이듯 연결하기 
result3 = pd.concat([df1, df2], axis=1)
print(result3, '\n')

# join='inner' 옵션 적용하기(교집합)
result3_in = pd.concat([df1, df2], axis=1, join='inner')
print(result3_in, '\n')

# 시리즈 만들기
sr1 = pd.Series(['e0', 'e1', 'e2', 'e3'], name='e')
sr2 = pd.Series(['f0', 'f1', 'f2'], name='f', index=[3, 4, 5])
sr3 = pd.Series(['g0', 'g1', 'g2', 'g3'], name='g')

# df1과 sr1을 좌우 열 방향으로 연결하기
result4 = pd.concat([df1, sr1], axis=1)
print(result4, '\n')

# df2과 sr2을 좌우 열 방향으로 연결하기
result5 = pd.concat([df2, sr2], axis=1, sort=True)
print(result5, '\n')

# sr1과 sr3을 좌우 열 방향으로 연결하기
result6 = pd.concat([sr1, sr3], axis=1)
print(result6, '\n')

result7 = pd.concat([sr1, sr3], axis=0)
print(result7, '\n')

```


```python
# 예제 6-12
import pandas as pd

# IPyhton 디스플레이 설정 변경 
pd.set_option('display.max_columns', 10)                  # 출력할 최대 열의 개수
pd.set_option('display.max_colwidth', 20)                 # 출력할 열의 너비
pd.set_option('display.unicode.east_asian_width', True)   # 유니코드 사용 너비 조정

# 주식 데이터를 가져와서 데이터프레임 만들기
df1 = pd.read_excel('./data/stock price.xlsx')
df2 = pd.read_excel('./data/stock valuation.xlsx')

print(df1)
print('\n')
print(df2)
print('\n')

# 데이터프레임 합치기 - 교집합
merge_inner = pd.merge(df1, df2)
print(merge_inner)
print('\n')

# 데이터프레임 합치기 - 합집합
merge_outer = pd.merge(df1, df2, how='outer', on='id')
print(merge_outer)
print('\n')

# 데이터프레임 합치기 - 왼쪽 데이터프레임 기준, 키 값 분리
merge_left = pd.merge(df1, df2, how='left', left_on='stock_name', right_on='name')
print(merge_left)
print('\n')

# 데이터프레임 합치기 - 오른쪽 데이터프레임 기준, 키 값 분리
merge_right = pd.merge(df1, df2, how='right', left_on='stock_name', right_on='name')
print(merge_right)
print('\n')

# 불린 인덱싱과 결합하여 원하는 데이터 찾기
price = df1[df1['price'] < 50000]
print(price.head())
print('\n')

value = pd.merge(price, df2)
print(value)

```


```python
# 예제 6-13
import pandas as pd

# IPyhton 디스플레이 설정 변경 
pd.set_option('display.max_columns', 10)                  # 출력할 최대 열의 개수
pd.set_option('display.max_colwidth', 20)                 # 출력할 열의 너비
pd.set_option('display.unicode.east_asian_width', True)   # 유니코드 사용 너비 조정

# 주식 데이터를 가져와서 데이터프레임 만들기
df1 = pd.read_excel('./data/stock price.xlsx', index_col='id')
df2 = pd.read_excel('./data/stock valuation.xlsx', index_col='id')

# 데이터프레임 결합(join)
df3 = df1.join(df2)
print(df3)
print('\n')

# 데이터프레임 결합(join) - 교집합
df4 = df1.join(df2, how='inner')
print(df4)
```


```python
import pandas as pd
import numpy as np
df = pd.DataFrame({
    'city': ['부산', '부산', '부산', '부산', '서울', '서울', '서울'],
    'fruits': ['apple', 'orange', 'banana', 'banana', 'apple', 'apple', 'banana'],
    'price': [100, 200, 250, 300, 150, 200, 400],
    'quantity': [1, 2, 3, 4, 5, 6, 7]
})
df
```


```python
df.groupby('city')
```


```python
df.groupby('city').mean()
```


```python
df.groupby('city').agg('mean')
```


```python
df.groupby('city').transform('mean')
```


```python
df.groupby('city').agg(['mean', 'max', 'min'])
```


```python
df.groupby(['city', 'fruits']).mean()
```


```python
df.groupby(['city', 'fruits']).mean()
```


```python
df.groupby('city').get_group('부산')
```


```python
df.groupby('city').size()
```


```python
df.groupby('city').size()['부산']
```


```python

```


```python
# 예제 6-14
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]

print('승객 수:', len(df))
print(df.head())
print('\n')

# class 열을 기준으로 분할
grouped = df.groupby(['class']) 
print(grouped)
print('\n')

# 그룹 객체를 iteration으로 출력: head() 메소드로 첫 5행만을 출력
for key, group in grouped:
    print('* key :', key)
    print('* number :', len(group))    
    print(group.head())
    print('\n')
    
# 연산 메소드 적용
average = grouped.mean()
print(average)
print('\n')

# 개별 그룹 선택하기
group3 = grouped.get_group('Third')
print(group3.head())
print('\n')

# class 열, sex 열을 기준으로 분할
grouped_two = df.groupby(['class', 'sex']) 

# grouped_two 그룹 객체를 iteration으로 출력
for key, group in grouped_two:
    print('* key :', key)
    print('* number :', len(group))    
    print(group.head())
    print('\n')
    
# grouped_two 그룹 객체에 연산 메소드 적용
average_two = grouped_two.mean()
print(average_two)
print('\n')
print(type(average_two))

# grouped_two 그룹 객체에서 개별 그룹 선택하기
group3f = grouped_two.get_group(('Third','female'))
print(group3f.head())
```


```python
# 예제 6-15
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]

# class 열을 기준으로 분할
grouped = df.groupby(['class']) 

# 각 그룹에 대한 모든 열의 표준편차를 집계하여 데이터프레임으로 반환
std_all = grouped.std()  
print(std_all)
print('\n')
print(type(std_all))
print('\n')

# 각 그룹에 대한 fare 열의 표준편차를 집계하여 시리즈로 반환 
std_fare = grouped.fare.std()  
print(std_fare)
print('\n')
print(type(std_fare))
print('\n')

# 그룹 객체에 agg() 메소드 적용 - 사용자 정의 함수를 인수로 전달
def min_max(x):    # 최대값 - 최소값
    return x.max() - x.min()
    
# 각 그룹의 최대값과 최소값의 차이를 계산하여 그룹별로 집계
agg_minmax = grouped.agg(min_max)  
print(agg_minmax.head())
print('\n')

# 여러 함수를 각 열에 동일하게 적용하여 집계
agg_all = grouped.agg(['min', 'max'])  
print(agg_all.head())
print('\n')

# 각 열마다 다른 함수를 적용하여 집계
agg_sep = grouped.agg({'fare':['min', 'max'], 'age':'mean'})  
print(agg_sep.head())

```


```python
# 예제 6-16
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]

# class 열을 기준으로 분할
grouped = df.groupby(['class']) 

# 그룹별 age 열의 평균 집계 연산
age_mean = grouped.age.mean()
print(age_mean)
print('\n')

# 그룹별 age 열의 표준편차 집계 연산
age_std = grouped.age.std()
print(age_std)
print('\n') 

# 그룹 객체의 age 열을 iteration으로 z-score를 계산하여 출력
for key, group in grouped.age:
    group_zscore = (group - age_mean.loc[key]) / age_std.loc[key]         
    print('* origin :', key)
    print(group_zscore.head(3))  # 각 그룹의 첫 3개의 행을 출력
    print('\n')

# z-score를 계산하는 사용자 함수 정의
def z_score(x): 
    return (x - x.mean()) / x.std()
   
# transform() 메소드를 이용하여 age 열의 데이터를 z-score로 변환
age_zscore = grouped.age.transform(z_score)  
print(age_zscore.loc[[1, 9, 0]])     # 1, 2, 3 그룹의 첫 데이터 확인 (변환 결과)
print('\n')
print(len(age_zscore))              # transform 메소드 반환 값의 길이
print('\n')
print(age_zscore.loc[0:9])          # transform 메소드 반환 값 출력 (첫 10개)
print('\n')
print(type(age_zscore))             # transform 메소드 반환 객체의 자료형

```


```python
# 예제 6-17
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]

# class 열을 기준으로 분할
grouped = df.groupby(['class']) 

# 데이터 개수가 200개 이상인 그룹만을 필터링하여 데이터프레임으로 반환
grouped_filter = grouped.filter(lambda x: len(x) >= 200)  
print(grouped_filter.head())   
print('\n')
print(type(grouped_filter))

# age 열의 평균이 30보다 작은 그룹만을 필터링하여 데이터프레임으로 반환
age_filter = grouped.filter(lambda x: x.age.mean() < 30)  
print(age_filter.tail())   
print('\n')
print(type(age_filter))

```


```python
# 예제 6-18
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]

# class 열을 기준으로 분할
grouped = df.groupby(['class']) 

# 집계 : 각 그룹별 요약 통계정보를 집계
agg_grouped = grouped.apply(lambda x: x.describe())   
print(agg_grouped)
print('\n')
```


```python
# z-score를 계산하는 사용자 함수 정의
def z_score(x):                          
    return (x - x.mean()) / x.std()

age_zscore = grouped.age.apply(z_score)   #기본값 axis=0 
print(age_zscore.head())
print('\n')

# 필터링 : age 열의 데이터 평균이 30보다 작은 그룹만을 필터링하여 출력
age_filter = grouped.apply(lambda x: x.age.mean() < 30)  
print(age_filter)   
print('\n')
for x in age_filter.index:
    if age_filter[x]==True:
        age_filter_df = grouped.get_group(x)
        print(age_filter_df.head())
        print('\n')
```


```python
# 예제 6-19
import pandas as pd
import seaborn as sns

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]

# class 열, sex 열을 기준으로 분할
grouped = df.groupby(['class', 'sex']) 


# 그룹 객체에 연산 메서드 적용
gdf = grouped.mean()
print(gdf)
print(type(gdf))
print('\n')
print(gdf.index)

# class 값이 First인 행을 선택하여 출력
print(gdf.loc['First'])
print('\n')

# class 값이 First이고, sex 값이 female인 행을 선택하여 출력
print(gdf.loc[('First', 'female')])
print('\n')

# sex 값이 male인 행을 선택하여 출력
print(gdf.xs('male', level='sex'))

```


```python
# 예제 6-20
# 라이브러리 불러오기
import pandas as pd
import seaborn as sns

# IPyhton 디스플레이 설정 변경 
pd.set_option('display.max_columns', 10)    # 출력할 최대 열의 개수
pd.set_option('display.max_colwidth', 20)    # 출력할 열의 너비

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]
print(df.head())
print('\n')

# 행, 열, 값, 집계에 사용할 열을 1개씩 지정 - 평균 집계
pdf1 = pd.pivot_table(df,              # 피벗할 데이터프레임
                     index='class',    # 행 위치에 들어갈 열
                     columns='sex',    # 열 위치에 들어갈 열
                     values='age',     # 데이터로 사용할 열
                     aggfunc='mean')   # 데이터 집계 함수

print(pdf1.head())
print('\n')
```


```python
sns.heatmap(pdf1, annot=True)
```


```python
# 값에 적용하는 집계 함수를 2개 이상 지정 가능 - 생존율, 생존자 수 집계
pdf2 = pd.pivot_table(df,                       # 피벗할 데이터프레임
                     index='class',             # 행 위치에 들어갈 열
                     columns='sex',             # 열 위치에 들어갈 열
                     values='survived',         # 데이터로 사용할 열
                     aggfunc=['mean', 'sum'])   # 데이터 집계 함수

print(pdf2.head())
print('\n')

```


```python
sns.heatmap(pdf2, annot=True)
```


```python
# 행, 열, 값에 사용할 열을 2개 이상 지정 가능 - 평균 나이, 최대 요금 집계
pdf3 = pd.pivot_table(df,                       # 피벗할 데이터프레임
                     index=['class', 'sex'],    # 행 위치에 들어갈 열
                     columns='survived',        # 열 위치에 들어갈 열
                     values=['age', 'fare'],    # 데이터로 사용할 열
                     aggfunc=['mean', 'max'])   # 데이터 집계 함수

# IPython Console 디스플레이 옵션 설정
pd.set_option('display.max_columns', 10)        # 출력할 열의 개수 한도
print(pdf3.head())
print('\n')

# 행, 열 구조 살펴보기
print(pdf3.index)
print(pdf3.columns)
print('\n')
```


```python
sns.heatmap(pdf3, annot=True, fmt='.1f')
```


```python
# xs 인덱서 사용 - 행 선택(default: axis=0)
print(pdf3.xs('First'))              # 행 인덱스가 First인 행을 선택 
print('\n')
print(pdf3.xs(('First', 'female')))   # 행 인덱스가 ('First', 'female')인 행을 선택
print('\n')
print(pdf3.xs('male', level='sex'))  # 행 인덱스의 sex 레벨이 male인 행을 선택
print('\n')
print(pdf3.xs(('Second', 'male'), level=[0, 'sex']))  # Second, male인 행을 선택
print('\n')
```


```python
# xs 인덱서 사용 - 열 선택(axis=1 설정)
print(pdf3.xs('mean', axis=1))        # 열 인덱스가 mean인 데이터를 선택 
print('\n')
print(pdf3.xs(('mean', 'age'), axis=1))   # 열 인덱스가 ('mean', 'age')인 데이터 선택
print('\n')
print(pdf3.xs(1, level='survived', axis=1))  # survived 레벨이 1인 데이터 선택
print('\n')
print(pdf3.xs(('max', 'fare', 0), 
              level=[0, 1, 2], axis=1))  # max, fare, survived=0인 데이터 선택

```



### - 실습

```python
import pandas as pd
import seaborn as sns
import numpy as np

# matplotlib 한글 폰트 오류 문제 해결
from matplotlib import font_manager, rc
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

df = pd.read_csv('./data/product_click.log', header=None, sep=' ')
df.columns = ['oldclicktime','clickpid']
df['oldclicktime'] = df['oldclicktime'].astype('str')  
df['newclicktime'] = pd.to_datetime(df['oldclicktime'], format='%Y%m%d%H%M')
display(df.head())
```


```python
# 문제 1 - 1 상품별 클릭수를 바그래프로 그리는데 클릭수가 많은 순으로 그린다.
from matplotlib import pyplot as plt
import seaborn as sns

aggrProduct = df.groupby('clickpid').clickpid.count().sort_values(ascending=False)
# display(aggrProduct)
prodColors = sns.color_palette('hls', len(aggrProduct))
aggrProduct.plot(kind='bar', color=prodColors, width=0.7, figsize=(12, 10), grid=True)

plt.title('상품별 클릭 횟수', size=20)
plt.ylabel('클릭횟수', size=17)
plt.xlabel('상품ID', size=17)
plt.xticks(rotation=25)

plt.show()
```


```python
# 문제 1 - 2 어떤 요일에 가장 많이 클릭하는지 다음과 같이 출력하시오.
def findKorWeek(numweek) :
    korWeek = ['월', '화', '수', '목', '금', '토', '일']
    return korWeek[numweek]

df['weekday'] = df['newclicktime'].dt.weekday.apply(findKorWeek)
clickByWeek = df.groupby('weekday').clickpid.count().sort_values(ascending=False)

print("클릭 수가 제일 많은 요일은 ", clickByWeek.head(1).index[0] + "요일입니다.", sep='')
```


```python
# 문제 1 - 3 어느 시간대에 가장 많이 클릭하는지 다음과 같이 출력하시오.
df['hour'] = df['newclicktime'].dt.hour
clickByhour = df.groupby('hour').clickpid.count().sort_values(ascending=False)

startTime = clickByhour.head(1).index[0]
endTime = clickByhour.head(1).index[0] + 1

print(startTime.astype('str'), "시와 " ,endTime.astype('str') ,"시 사이에 제일 많이 클릭했습니다.", sep='')
```


```python
# 문제 2 - 1 부서별 월급의 합
emp = pd.read_csv('./data/emp.csv', header=0)
pd.DataFrame(emp.groupby('deptno').sal.sum())

```


```python
# 문제 2 - 2 직무(job)별 월급의 합
pd.DataFrame(emp.groupby('job').sal.sum())
```


```python
# 문제 2 - 3 부서와 직무(job)별 최고 월급과 입사한지 가장 오래된 직원의 입사날짜
pd.DataFrame(emp.groupby(['deptno', 'job']).agg({'sal':'sum', 'hiredate':'min'}))
```


```python
# 문제 2 - 4 직무(job)와 부서별 최고 월급
pd.DataFrame(emp.groupby(['job', 'deptno']).agg({'sal':'max'}))
```

