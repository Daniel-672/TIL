

# 분석Day08

>  pandas, seaborn, folium

### - 교육내용

```python
# 예제 5-1
# 라이브러리 불러오기
import seaborn as sns

# titanic 데이터셋 가져오기
df = sns.load_dataset('titanic')

# deck 열의 NaN 개수 계산하기
nan_deck = df['deck'].value_counts(dropna=False) 
print(nan_deck)

# isnull() 메서드로 누락 데이터 찾기
print(df.head().isnull())

# notnull() 메서드로 누락 데이터 찾기
print(df.head().notnull())

# isnull() 메서드로 누락 데이터 개수 구하기
print(df.head().isnull().sum(axis=0))

```


```python
# 예제 5-2
# 라이브러리 불러오기
import seaborn as sns

# titanic 데이터셋 가져오기
df = sns.load_dataset('titanic')

# for 반복문으로 각 열의 NaN 개수 계산하기
missing_df = df.isnull()
print(missing_df.value_counts() )

for col in missing_df.columns:
    missing_count = missing_df[col].value_counts()    # 각 열의 NaN 개수 파악

    try: 
        print(col, ': ', missing_count[True])   # NaN 값이 있으면 개수를 출력
    except:
        print(col, ': ', 0)                     # NaN 값이 없으면 0개 출력
        
# NaN 값이 500개 이상인 열을 모두 삭제 - deck 열(891개 중 688개의 NaN 값)
df_thresh = df.dropna(axis=1, thresh=500)  
print(df_thresh.columns)

# age 열에 나이 데이터가 없는 모든 행을 삭제 - age 열(891개 중 177개의 NaN 값)
df_age = df.dropna(subset=['age'], how='any', axis=0)  
print(len(df_age))


```


```python
# 예제 5-3
# 라이브러리 불러오기
import seaborn as sns

# titanic 데이터셋 가져오기
df = sns.load_dataset('titanic')

# age 열의 첫 10개 데이터 출력 (5 행에 NaN 값)
print(df['age'].head(10))
print('\n')

# age 열의 NaN값을 다른 나이 데이터의 평균으로 변경하기
mean_age = df['age'].mean(axis=0)   # age 열의 평균 계산 (NaN 값 제외)
df['age'].fillna(mean_age, inplace=True)

# age 열의 첫 10개 데이터 출력 (5 행에 NaN 값이 평균으로 대체)
print(df['age'].head(10))
type(df['age'].head(10))
```


```python
# 예제 5-4
# 라이브러리 불러오기
import seaborn as sns

# titanic 데이터셋 가져오기
df = sns.load_dataset('titanic')

# embark_town 열의 829행의 NaN 데이터 출력
print(df['embark_town'][825:830])
print('\n')

# embark_town 열의 NaN값을 승선도시 중에서 가장 많이 출현한 값으로 치환하기
most_freq = df['embark_town'].value_counts(dropna=True).idxmax()   
print(most_freq)
print('\n')

df['embark_town'].fillna(most_freq, inplace=True)

# embark_town 열 829행의 NaN 데이터 출력 (NaN 값이 most_freq 값으로 대체)
print(df['embark_town'][825:830])
```


```python
# 예제 5-5
# 라이브러리 불러오기
import seaborn as sns

# titanic 데이터셋 가져오기
df = sns.load_dataset('titanic')

# embark_town 열의 829행의 NaN 데이터 출력
print(df['embark_town'][825:830])
print('\n')

# embark_town 열의 NaN값을 바로 앞에 있는 828행의 값으로 변경하기
df['embark_town'].fillna(method='ffill', inplace=True)
print(df['embark_town'][825:830])
```


```python
# 예제 5-6
# 라이브러리 불러오기
import pandas as pd

# 중복 데이터를 갖는 데이터프레임 만들기
df = pd.DataFrame({'c1':['a', 'a', 'b', 'a', 'b','a'],
                  'c2':[1, 1, 1, 2, 2, 1],
                  'c3':[1, 1, 2, 2, 2, 2]})
print(df)
print('\n')

# 데이터프레임 전체 행 데이터 중에서 중복값 찾기
df_dup = df.duplicated()
print(df_dup)
print('\n')

# 데이터프레임의 특정 열 데이터에서 중복값 찾기
col_dup = df['c2'].duplicated()
print(col_dup)
print(col_dup.value_counts())
print(col_dup.value_counts('c2'))
```


```python
# 예제 5-7
# 라이브러리 불러오기
import pandas as pd

# 중복 데이터를 갖는 데이터프레임 만들기
df = pd.DataFrame({'c1':['a', 'a', 'b', 'a', 'b'],
                  'c2':[1, 1, 1, 2, 2],
                  'c3':[1, 1, 2, 2, 2]})
print(df)
print('\n')

# 데이터프레임에서 중복 행을 제거
df2 = df.drop_duplicates()
print(df2)
print('\n')

# c2, c3열을 기준으로 중복 행을 제거
df3 = df.drop_duplicates(subset=['c2', 'c3'])
print(df3.sort_values(by='c2'))

```


```python
# 예제 5-8
# 라이브러리 불러오기
import pandas as pd

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name'] 
print(df.head(3))    
print('\n')

# mpg(mile per gallon)를 kpl(kilometer per liter)로 변환 (mpg_to_kpl = 0.425)
mpg_to_kpl = 1.60934 / 3.78541

# mpg 열에 0.425를 곱한 결과를 새로운 열(kpl)에 추가
df['kpl'] = df['mpg'] * mpg_to_kpl
print(df.head(3))    
print('\n')

# kpl 열을 소수점 아래 둘째 자리에서 반올림 
df['kpl'] = df['kpl'].round(2)
print(df.head(3))     
```


```python
# 예제 5-9
# 라이브러리 불러오기
import pandas as pd

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name'] 

# 각 열의 자료형 확인
print(df.dtypes)   
print('\n')
print(df.info())   
print('\n')
print(df.describe(include='all'))   
print('\n')
# horsepower 열의 고유값 확인
print(df['horsepower'].unique())
print('\n')

# 누락 데이터('?') 삭제 
import numpy as np
df['horsepower'].replace('?', np.nan, inplace=True)      # '?'을 np.nan으로 변경
df.dropna(subset=['horsepower'], axis=0, inplace=True)   # 누락데이터 행을 삭제
df['horsepower'] = df['horsepower'].astype('float')      # 문자열을 실수형으로 변환

# horsepower 열의 자료형 확인
print(df['horsepower'].dtypes)  
print('\n')

# origin 열의 고유값 확인
print(df['origin'].unique())

# 정수형 데이터를 문자형 데이터로 변환 
df['origin'].replace({1:'USA', 2:'EU', 3:'JAPAN'}, inplace=True)

# origin 열의 고유값과 자료형 확인
print(df['origin'].unique())
print(df['origin'].dtypes) 
print('\n')

# origin 열의 문자열 자료형을 범주형으로 변환
df['origin'] = df['origin'].astype('category')     
print(df['origin'].dtypes) 

# 범주형을 문자열로 다시 변환
df['origin'] = df['origin'].astype('str')     
print(df['origin'].dtypes)

# model year 열의 정수형을 범주형으로 변환
print(df['model year'].sample(3))
df['model year'] = df['model year'].astype('category') 
print(df['model year'].sample(3)) 
```


```python
# 예제 5-10
# 라이브러리 불러오기
import pandas as pd
import numpy as np

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name'] 

# horsepower 열의 누락 데이터('?') 삭제하고 실수형으로 변환
df['horsepower'].replace('?', np.nan, inplace=True)      # '?'을 np.nan으로 변경
df.dropna(subset=['horsepower'], axis=0, inplace=True)   # 누락데이터 행을 삭제
df['horsepower'] = df['horsepower'].astype('float')      # 문자열을 실수형으로 변환

# np.histogram 함수로 3개의 bin으로 나누는 경계 값의 리스트 구하기
count, bin_dividers = np.histogram(df['horsepower'], bins=3)
print(df['horsepower'].describe())
print(df['horsepower'].count())
print(count, bin_dividers) 

df['horsepower'].hist(bins='auto')

# 3개의 bin에 이름 지정
bin_names = ['저출력', '보통출력', '고출력']

# pd.cut 함수로 각 데이터를 3개의 bin에 할당
df['hp_bin'] = pd.cut(x=df['horsepower'],     # 데이터 배열
                      bins=bin_dividers,      # 경계 값 리스트
                      labels=bin_names,       # bin 이름
                      include_lowest=True)    # 첫 경계값 포함 

# horsepower 열, hp_bin 열의 첫 15행을 출력
print(df[['horsepower', 'hp_bin']].head(15))
```


```python
# 예제 5-11
# 라이브러리 불러오기
import pandas as pd
import numpy as np

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name'] 

# horsepower 열의 누락 데이터('?') 삭제하고 실수형으로 변환
df['horsepower'].replace('?', np.nan, inplace=True)      # '?'을 np.nan으로 변경
df.dropna(subset=['horsepower'], axis=0, inplace=True)   # 누락데이터 행을 삭제
df['horsepower'] = df['horsepower'].astype('float')      # 문자열을 실수형으로 변환

# np.histogram 으로 3개의 bin으로 나누는 경계 값의 리스트 구하기
count, bin_dividers = np.histogram(df['horsepower'], bins=3)

# 3개의 bin에 이름 지정
bin_names = ['저출력', '보통출력', '고출력']

# pd.cut 으로 각 데이터를 3개의 bin에 할당
df['hp_bin'] = pd.cut(x=df['horsepower'],     # 데이터 배열
                      bins=bin_dividers,      # 경계 값 리스트
                      labels=bin_names,       # bin 이름
                      include_lowest=True)    # 첫 경계값 포함

# hp_bin 열의 범주형 데이터를 더미 변수로 변환
horsepower_dummies = pd.get_dummies(df['hp_bin'])
print(horsepower_dummies.head(15))

```


```python
# 예제 5-12
# 라이브러리 불러오기
import pandas as pd
import numpy as np

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name'] 

# horsepower 열의 누락 데이터('?') 삭제하고 실수형으로 변환
df['horsepower'].replace('?', np.nan, inplace=True)      # '?'을 np.nan으로 변경
df.dropna(subset=['horsepower'], axis=0, inplace=True)   # 누락데이터 행을 삭제
df['horsepower'] = df['horsepower'].astype('float')      # 문자열을 실수형으로 변환

# np.histogram 으로 3개의 bin으로 나누는 경계 값의 리스트 구하기
count, bin_dividers = np.histogram(df['horsepower'], bins=3)

# 3개의 bin에 이름 지정
bin_names = ['저출력', '보통출력', '고출력']

# pd.cut 으로 각 데이터를 3개의 bin에 할당
df['hp_bin'] = pd.cut(x=df['horsepower'],     # 데이터 배열
                      bins=bin_dividers,      # 경계 값 리스트
                      labels=bin_names,       # bin 이름
                      include_lowest=True)    # 첫 경계값 포함

# sklern 라이브러리 불러오기
from sklearn import preprocessing    

# 전처리를 위한 encoder 객체 만들기
label_encoder = preprocessing.LabelEncoder()       # label encoder 생성
onehot_encoder = preprocessing.OneHotEncoder()   # one hot encoder 생성

# label encoder로 문자열 범주를 숫자형 범주로 변환
onehot_labeled = label_encoder.fit_transform(df['hp_bin'].head(15))  
print(onehot_labeled)
print(type(onehot_labeled))

# 2차원 행렬로 형태 변경
onehot_reshaped = onehot_labeled.reshape(len(onehot_labeled), 1) 
print(onehot_reshaped)
print(type(onehot_reshaped))

# 희소행렬로 변환
onehot_fitted = onehot_encoder.fit_transform(onehot_reshaped)
print(onehot_fitted)
print(type(onehot_fitted))
```


```python
# 예제 5-13
# 라이브러리 불러오기
import pandas as pd
import numpy as np

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name']  

# horsepower 열의 누락 데이터('?') 삭제하고 실수형으로 변환
df['horsepower'].replace('?', np.nan, inplace=True)      # '?'을 np.nan으로 변경
df.dropna(subset=['horsepower'], axis=0, inplace=True)   # 누락데이터 행을 삭제
df['horsepower'] = df['horsepower'].astype('float')      # 문자열을 실수형으로 변환

# horsepower 열의 통계 요약정보로 최대값(max)을 확인
print(df.horsepower.describe())
print('\n')

# horsepower 열의 최대값의 절대값으로 모든 데이터를 나눠서 저장
df.horsepower = df.horsepower / abs(df.horsepower.max()) 

print(df.horsepower.head())
print('\n')
print(df.horsepower.describe())
```


```python
# 예제 5-14
# 라이브러리 불러오기
import pandas as pd
import numpy as np

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name']  

# horsepower 열의 누락 데이터('?') 삭제하고 실수형으로 변환
df['horsepower'].replace('?', np.nan, inplace=True)      # '?'을 np.nan으로 변경
df.dropna(subset=['horsepower'], axis=0, inplace=True)   # 누락데이터 행을 삭제
df['horsepower'] = df['horsepower'].astype('float')      # 문자열을 실수형으로 변환

# horsepower 열의 통계 요약정보로 최대값(max)과 최소값(min)을 확인
print(df.horsepower.describe())
print('\n')

# horsepower 열의 최대값의 절대값으로 모든 데이터를 나눠서 저장
min_x = df.horsepower - df.horsepower.min()
min_max = df.horsepower.max() - df.horsepower.min()
df.horsepower = min_x / min_max

print(df.horsepower.head())
print('\n')
print(df.horsepower.describe())
```


```python
# 예제 5-15
# 라이브러리 불러오기
import pandas as pd

# read_csv() 함수로 CSV 파일을 가져와서 df로 변환
df = pd.read_csv('data/stock-data.csv')

# 데이터 내용 및 자료형 자료형 확인
print(df.head())
print('\n')
print(df.info())

# 문자열 데이터(시리즈 객체)를 판다스 Timestamp로 변환
df['new_Date'] = pd.to_datetime(df['Date'])   #df에 새로운 열로 추가

# 데이터 내용 및 자료형 자료형 확인
print(df.head())
print('\n')
print(df.info())
print('\n')
print(type(df['new_Date'][0]))

# 시계열 값으로 변환된 열을 새로운 행 인덱스로 지정. 기존 날짜 열은 삭제
df.set_index('new_Date', inplace=True)
df.drop('Date', axis=1, inplace=True)

# 데이터 내용 및 자료형 자료형 확인
print(df.head())
print('\n')
print(df.info())

```


```python
# 예제 5-16
# 라이브러리 불러오기
import pandas as pd

# 날짜 형식의 문자열로 구성되는 리스트 정의
dates = ['2019-01-01', '2020-03-01', '2021-06-01']

# 문자열 데이터(시리즈 객체)를 판다스 Timestamp로 변환
ts_dates = pd.to_datetime(dates)   
print(ts_dates)
print('\n')

# Timestamp를 Period로 변환
pr_day = ts_dates.to_period(freq='D')
print(pr_day)
pr_month = ts_dates.to_period(freq='M')
print(pr_month)
pr_year = ts_dates.to_period(freq='A')
print(pr_year)
```


```python
# 예제 5-17
# 라이브러리 불러오기
import pandas as pd

# Timestamp의 배열 만들기 - 월 간격, 월의 시작일 기준
ts_ms = pd.date_range(start='2019-01-01',    # 날짜 범위의 시작
                   end=None,                 # 날짜 범위의 끝
                   periods=6,                # 생성할 Timestamp의 개수
                   freq='MS',                # 시간 간격 (MS: 월의 시작일)
                   tz='Asia/Seoul')          # 시간대(timezone)
print(ts_ms)
print('\n')

# 월 간격, 월의 마지막 날 기준
ts_me = pd.date_range('2019-01-01', periods=6, 
                   freq='M',              # 시간 간격 (M: 월의 마지막 날)
                   tz='Asia/Seoul')       # 시간대(timezone)
print(ts_me)
print('\n')

# 분기(3개월) 간격, 월의 마지막 날 기준
ts_3m = pd.date_range('2019-01-01', periods=6, 
                   freq='3M',             # 시간 간격 (3M: 3개월)
                   tz='Asia/Seoul')       # 시간대(timezone)
print(ts_3m)

```


```python
# 예제 5-18
# 라이브러리 불러오기
import pandas as pd

# Period 배열 만들기 - 1개월 길이
pr_m = pd.period_range(start='2019-01-01',     # 날짜 범위의 시작
                   end=None,                   # 날짜 범위의 끝
                   periods=3,                  # 생성할 Period 개수
                   freq='M')                   # 기간의 길이 (M: 월)
print(pr_m)
print('\n')

# Period 배열 만들기 - 1시간 길이
pr_h = pd.period_range(start='2019-01-01',     # 날짜 범위의 시작
                   end=None,                   # 날짜 범위의 끝
                   periods=3,                  # 생성할 Period 개수
                   freq='H')                   # 기간의 길이 (H: 시간)
print(pr_h)
print('\n')

# Period 배열 만들기 - 2시간 길이
pr_2h = pd.period_range(start='2019-01-01',    # 날짜 범위의 시작
                   end=None,                   # 날짜 범위의 끝
                   periods=3,                  # 생성할 Period 개수
                   freq='2H')                  # 기간의 길이 (H: 시간)
print(pr_2h)
```


```python
# 예제 5-19
# 라이브러리 불러오기
import pandas as pd

# read_csv() 함수로 파일 읽어와서 df로 변환
df = pd.read_csv('data/stock-data.csv')

# 문자열인 날짜 데이터를 판다스 Timestamp로 변환
df['new_Date'] = pd.to_datetime(df['Date'])   #df에 새로운 열로 추가
print(df.head())
print('\n')

# dt 속성을 이용하여 new_Date 열의 년월일 정보를 년, 월, 일로 구분
df['Year'] = df['new_Date'].dt.year
df['Month'] = df['new_Date'].dt.month
df['Day'] = df['new_Date'].dt.day
print(df.head())
print('\n')

# Timestamp를 Period로 변환하여 년월일 표기 변경하기
df['Date_yr'] = df['new_Date'].dt.to_period(freq='A')
df['Date_m'] = df['new_Date'].dt.to_period(freq='M')
print(df.head())
print('\n')

# 원하는 열을 새로운 행 인덱스로 지정
df.set_index('Date_m', inplace=True)
print(df.head())

```


```python
# 예제 5-20
# 라이브러리 불러오기
import pandas as pd

# read_csv() 함수로 파일 읽어와서 df로 변환
df = pd.read_csv('data/stock-data.csv')

# 문자열인 날짜 데이터를 판다스 Timestamp로 변환
df['new_Date'] = pd.to_datetime(df['Date'])   # 새로운 열에 추가
df.set_index('new_Date', inplace=True)        # 행 인덱스로 지정

print(df.head())
print('\n')
print(df.index)
print('\n')

# 날짜 인덱스를 이용하여 데이터 선택하기
df_y = df.loc['2018']
print(df_y.head())
print('\n')
df_ym = df.loc['2018-07']    # loc 인덱서 활용
print(df_ym)
print('\n')
df_ym_cols = df.loc['2018-07-02', 'Start':'High']    # 열 범위 슬라이싱
print(df_ym_cols)
print('\n')
df_ymd = df.loc['2018-07-02']
print(df_ymd)
print('\n')
df_ymd_range = df['2018-06-25':'2018-06-20']    # 날짜 범위 지정
print(df_ymd_range)
print('\n')

# 시간 간격 계산. 최근 180일 ~ 189일 사이의 값들만 선택하기
today = pd.to_datetime('2018-12-25')            # 기준일 생성
df['time_delta'] = today - df.index             # 날짜 차이 계산
df.set_index('time_delta', inplace=True)        # 행 인덱스로 지정
df_180 = df['180 days':'189 days']
print(df_180)


```



### - 실습

```python
# 문제 1
import pandas as pd
import seaborn as sns
import numpy as np

iris = sns.load_dataset("iris")
iris_x = iris.loc[:,['sepal_length', 'sepal_width',
            'petal_length', 'petal_width']]
import random
random.seed(1)
for col in range(4):
    iris_x.iloc[[random.sample(range(len(iris)), 20)], col] = float('nan')
display(iris_x.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>NaN</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.4</td>
      <td>NaN</td>
      <td>1.7</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4.6</td>
      <td>NaN</td>
      <td>1.4</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.4</td>
      <td>2.9</td>
      <td>NaN</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 1 - 1
iris_x_1 = iris_x.head(10).dropna(how='any', axis=0)  
display(iris_x_1.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 1 - 2
iris_x_2 = iris_x.dropna(axis=0, thresh=3)  
display(iris_x_2.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>NaN</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.4</td>
      <td>NaN</td>
      <td>1.7</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4.6</td>
      <td>NaN</td>
      <td>1.4</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.4</td>
      <td>2.9</td>
      <td>NaN</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5.4</td>
      <td>3.7</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 1 - 3
iris_x_3 = iris_x.dropna(subset=['sepal_length', 'sepal_width'], how='any', axis=0)  
display(iris_x_3.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.4</td>
      <td>2.9</td>
      <td>NaN</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5.4</td>
      <td>3.7</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>4.8</td>
      <td>3.4</td>
      <td>1.6</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4.8</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4.3</td>
      <td>3.0</td>
      <td>1.1</td>
      <td>0.1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>5.8</td>
      <td>4.0</td>
      <td>1.2</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 1 - 4
# iris_x.fillna(mean_age, inplace=True)
iris_x_4 = iris_x.fillna(0)
display(iris_x_4.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>0.0</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.4</td>
      <td>0.0</td>
      <td>1.7</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4.6</td>
      <td>0.0</td>
      <td>1.4</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.5</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.4</td>
      <td>2.9</td>
      <td>0.0</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 1 - 5
iris_x_mean = round(iris_x.mean(), 1)
# display(iris_x_mean)
iris_x_5 = iris_x.fillna(iris_x_mean) #열별로 잘 찾아 들어감 ^^
display(iris_x_5.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.8</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.1</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.4</td>
      <td>3.1</td>
      <td>1.7</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.4</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>5.8</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.4</td>
      <td>2.9</td>
      <td>3.7</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 1 - 6
iris_x_6 = iris_x.fillna(10)
display(iris_x_6.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10.0</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>10.0</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.4</td>
      <td>10.0</td>
      <td>1.7</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4.6</td>
      <td>10.0</td>
      <td>1.4</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>10.0</td>
      <td>10.0</td>
      <td>1.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.4</td>
      <td>2.9</td>
      <td>10.0</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 1 - 7
# iris_x_7 = iris_x.fillna(subset=['sepal_width', 'petal_length', 'petal_width'], method='ffill') 안됨
# iris_x_7 = iris_x['sepal_width', 'petal_length', 'petal_width'].fillna(method='ffill') 안됨
iris_x_7 = iris_x
iris_x_7['sepal_width'].fillna(method='ffill', inplace=True)
iris_x_7['petal_length'].fillna(method='ffill', inplace=True)
iris_x_7['petal_width'].fillna(method='ffill', inplace=True)
# display(iris_x_7.loc[6:7, 'sepal_length'])
iris_x_7.loc[6:7, 'sepal_length'].fillna(method='ffill', inplace=True)
display(iris_x_7.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.0</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5.4</td>
      <td>3.6</td>
      <td>1.7</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4.6</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>4.6</td>
      <td>3.6</td>
      <td>1.5</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4.4</td>
      <td>2.9</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4.9</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.1</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 2 - 1
ts_d = pd.date_range(start='2020-10-01',
                       end='2020-10-31', 
                       freq='D')
print(ts_d)
```

    DatetimeIndex(['2020-10-01', '2020-10-02', '2020-10-03', '2020-10-04',
                   '2020-10-05', '2020-10-06', '2020-10-07', '2020-10-08',
                   '2020-10-09', '2020-10-10', '2020-10-11', '2020-10-12',
                   '2020-10-13', '2020-10-14', '2020-10-15', '2020-10-16',
                   '2020-10-17', '2020-10-18', '2020-10-19', '2020-10-20',
                   '2020-10-21', '2020-10-22', '2020-10-23', '2020-10-24',
                   '2020-10-25', '2020-10-26', '2020-10-27', '2020-10-28',
                   '2020-10-29', '2020-10-30', '2020-10-31'],
                  dtype='datetime64[ns]', freq='D')



```python
# 문제 2 - 2
ts_m = pd.date_range(start='2020-01-01',
                       end='2020-12-31', 
                       freq='M')
print(ts_m)
```

    DatetimeIndex(['2020-01-31', '2020-02-29', '2020-03-31', '2020-04-30',
                   '2020-05-31', '2020-06-30', '2020-07-31', '2020-08-31',
                   '2020-09-30', '2020-10-31', '2020-11-30', '2020-12-31'],
                  dtype='datetime64[ns]', freq='M')



```python
# 문제 2 - 3
ts_d2 = pd.date_range(start='2020-10-01',
                       end='2020-11-19', 
                       freq='D')
print(ts_d2)
```

    DatetimeIndex(['2020-10-01', '2020-10-02', '2020-10-03', '2020-10-04',
                   '2020-10-05', '2020-10-06', '2020-10-07', '2020-10-08',
                   '2020-10-09', '2020-10-10', '2020-10-11', '2020-10-12',
                   '2020-10-13', '2020-10-14', '2020-10-15', '2020-10-16',
                   '2020-10-17', '2020-10-18', '2020-10-19', '2020-10-20',
                   '2020-10-21', '2020-10-22', '2020-10-23', '2020-10-24',
                   '2020-10-25', '2020-10-26', '2020-10-27', '2020-10-28',
                   '2020-10-29', '2020-10-30', '2020-10-31', '2020-11-01',
                   '2020-11-02', '2020-11-03', '2020-11-04', '2020-11-05',
                   '2020-11-06', '2020-11-07', '2020-11-08', '2020-11-09',
                   '2020-11-10', '2020-11-11', '2020-11-12', '2020-11-13',
                   '2020-11-14', '2020-11-15', '2020-11-16', '2020-11-17',
                   '2020-11-18', '2020-11-19'],
                  dtype='datetime64[ns]', freq='D')



```python
# 문제 2 - 4
ts_h = pd.date_range(start='2020-10-23',
                       periods=24, 
                       freq='H')
print(ts_h)
```

    DatetimeIndex(['2020-10-23 00:00:00', '2020-10-23 01:00:00',
                   '2020-10-23 02:00:00', '2020-10-23 03:00:00',
                   '2020-10-23 04:00:00', '2020-10-23 05:00:00',
                   '2020-10-23 06:00:00', '2020-10-23 07:00:00',
                   '2020-10-23 08:00:00', '2020-10-23 09:00:00',
                   '2020-10-23 10:00:00', '2020-10-23 11:00:00',
                   '2020-10-23 12:00:00', '2020-10-23 13:00:00',
                   '2020-10-23 14:00:00', '2020-10-23 15:00:00',
                   '2020-10-23 16:00:00', '2020-10-23 17:00:00',
                   '2020-10-23 18:00:00', '2020-10-23 19:00:00',
                   '2020-10-23 20:00:00', '2020-10-23 21:00:00',
                   '2020-10-23 22:00:00', '2020-10-23 23:00:00'],
                  dtype='datetime64[ns]', freq='H')



```python
# 문제 2 - 5
ts_3h = pd.date_range(start='2020-10-23',
                       periods=8, 
                       freq='3H')
print(ts_3h)
```

    DatetimeIndex(['2020-10-23 00:00:00', '2020-10-23 03:00:00',
                   '2020-10-23 06:00:00', '2020-10-23 09:00:00',
                   '2020-10-23 12:00:00', '2020-10-23 15:00:00',
                   '2020-10-23 18:00:00', '2020-10-23 21:00:00'],
                  dtype='datetime64[ns]', freq='3H')



```python
# 문제 2 - 6
ts_2m = pd.date_range(start='2020-01-01',
                       periods=8, 
                       freq='2M')
print(ts_2m)
```

    DatetimeIndex(['2020-01-31', '2020-03-31', '2020-05-31', '2020-07-31',
                   '2020-09-30', '2020-11-30', '2021-01-31', '2021-03-31'],
                  dtype='datetime64[ns]', freq='2M')



```python
# 문제 3 - 1
df = pd.read_csv('./data/product_click.log', header=None, sep=' ')
display(df.head())
df.info()
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201612120944</td>
      <td>p001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201612120944</td>
      <td>p003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201612120944</td>
      <td>p003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201612120945</td>
      <td>p008</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201612121052</td>
      <td>p008</td>
    </tr>
  </tbody>
</table>

</div>


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 746 entries, 0 to 745
    Data columns (total 2 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   0       746 non-null    int64 
     1   1       746 non-null    object
    dtypes: int64(1), object(1)
    memory usage: 11.8+ KB



```python
# 문제 3 - 2
df.columns = ['oldclicktime','clickpid']
display(df.head())
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>oldclicktime</th>
      <th>clickpid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201612120944</td>
      <td>p001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201612120944</td>
      <td>p003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201612120944</td>
      <td>p003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201612120945</td>
      <td>p008</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201612121052</td>
      <td>p008</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 3 - 3
df['oldclicktime'] = df['oldclicktime'].astype('str')  
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 746 entries, 0 to 745
    Data columns (total 2 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   oldclicktime  746 non-null    object
     1   clickpid      746 non-null    object
    dtypes: object(2)
    memory usage: 11.8+ KB



```python
# 문제 3 - 4
df['newclicktime'] = pd.to_datetime(df['oldclicktime'], format='%Y%m%d%H%M')
df.info()
display(df.head())
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 746 entries, 0 to 745
    Data columns (total 3 columns):
     #   Column        Non-Null Count  Dtype         
    ---  ------        --------------  -----         
     0   oldclicktime  746 non-null    object        
     1   clickpid      746 non-null    object        
     2   newclicktime  746 non-null    datetime64[ns]
    dtypes: datetime64[ns](1), object(2)
    memory usage: 17.6+ KB



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>oldclicktime</th>
      <th>clickpid</th>
      <th>newclicktime</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201612120944</td>
      <td>p001</td>
      <td>2016-12-12 09:44:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201612120944</td>
      <td>p003</td>
      <td>2016-12-12 09:44:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201612120944</td>
      <td>p003</td>
      <td>2016-12-12 09:44:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201612120945</td>
      <td>p008</td>
      <td>2016-12-12 09:45:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201612121052</td>
      <td>p008</td>
      <td>2016-12-12 10:52:00</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 문제 3 - 5
df['year'] = df['newclicktime'].dt.year
df['month'] = df['newclicktime'].dt.month
df['day'] = df['newclicktime'].dt.day
df['hour'] = df['newclicktime'].dt.hour
df['minute'] = df['newclicktime'].dt.minute
df.info()
display(df.head())
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 746 entries, 0 to 745
    Data columns (total 8 columns):
     #   Column        Non-Null Count  Dtype         
    ---  ------        --------------  -----         
     0   oldclicktime  746 non-null    object        
     1   clickpid      746 non-null    object        
     2   newclicktime  746 non-null    datetime64[ns]
     3   year          746 non-null    int64         
     4   month         746 non-null    int64         
     5   day           746 non-null    int64         
     6   hour          746 non-null    int64         
     7   minute        746 non-null    int64         
    dtypes: datetime64[ns](1), int64(5), object(2)
    memory usage: 46.8+ KB



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>oldclicktime</th>
      <th>clickpid</th>
      <th>newclicktime</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>hour</th>
      <th>minute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201612120944</td>
      <td>p001</td>
      <td>2016-12-12 09:44:00</td>
      <td>2016</td>
      <td>12</td>
      <td>12</td>
      <td>9</td>
      <td>44</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201612120944</td>
      <td>p003</td>
      <td>2016-12-12 09:44:00</td>
      <td>2016</td>
      <td>12</td>
      <td>12</td>
      <td>9</td>
      <td>44</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201612120944</td>
      <td>p003</td>
      <td>2016-12-12 09:44:00</td>
      <td>2016</td>
      <td>12</td>
      <td>12</td>
      <td>9</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201612120945</td>
      <td>p008</td>
      <td>2016-12-12 09:45:00</td>
      <td>2016</td>
      <td>12</td>
      <td>12</td>
      <td>9</td>
      <td>45</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201612121052</td>
      <td>p008</td>
      <td>2016-12-12 10:52:00</td>
      <td>2016</td>
      <td>12</td>
      <td>12</td>
      <td>10</td>
      <td>52</td>
    </tr>
  </tbody>
</table>

</div>

