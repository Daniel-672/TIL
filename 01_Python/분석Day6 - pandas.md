

# 분석Day06

>  pandas

### - 교육내용

```python
# 예제 3-1
import pandas as pd

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name']

# 데이터프레임 df의 내용을 일부 확인 
display(df.head())     # 처음 5개의 행
print('\n')
display(df.tail())     # 마지막 5개의 행
```


```python
# df의 모양과 크기 확인: (행의 개수, 열의 개수)를 투플로 반환 
print(df.shape)
print('\n')
```


```python
# 데이터프레임 df의 내용 확인 
print(df.info())
print('\n')
```


```python
# 데이터프레임 df의 자료형 확인 
print(df.dtypes)
print('\n')

# 시리즈(mog 열)의 자료형 확인 
print(df.mpg.dtypes)
print('\n')
```


```python
# 데이터프레임 df의 기술통계 정보 확인 
print(df.describe())
print('\n')
print(df.describe(include='all'))
```


```python
sr1 = pd.Series([11,20,30,25,100,40,57,8])
sr2 = pd.Series(['AA', 'BB', 'AA', 'BB', 'AA', 'AA', 'CC', 'AA'])
print('[숫자로 구성된 시리즈]')
print(sr1.describe())
print('[문자열로 구성된 시리즈]')
print(sr2.describe())
```


```python
# 예제 3-2
import pandas as pd

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name']

# 데이터프레임 df의 각 열이 가지고 있는 원소 개수 확인 
print(df.count())
print('\n')
```


```python
# df.count()가 반환하는 객체 타입 출력
print(type(df.count()))
print('\n')

# 데이터프레임 df의 특정 열이 가지고 있는 고유값 확인 
unique_values = df['origin'].value_counts() 
print(unique_values)
print('\n')

# value_counts 메소드가 반환하는 객체 타입 출력
print(type(unique_values))
```


```python
# 예제 3-3
import pandas as pd

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name']

# 평균값 
print(df.mean())
print('\n')
print(df['mpg'].mean())
print(df.mpg.mean())
print('\n')
print(df[['mpg','weight']].mean())
```


```python
# 중간값 
print(df.median())
print('\n')
print(df['mpg'].median())
```


```python
# 최대값 
print(df.max())
print('\n')
print(df['mpg'].max())
```


```python
# 최소값 
print(df.min())
print('\n')
print(df['mpg'].min())
```


```python
# 표준편차 
print(df.std())
print('\n')
print(df['mpg'].std())
```


```python
# 상관계수 
print(df.corr())
print('\n')
print(df[['mpg','weight']].corr())
```


```python
# 예제 3-4
import pandas as pd

df = pd.read_excel('./data/남북한발전전력량.xlsx')  # 데이터프레임 변환 

df_ns = df.iloc[[0, 5], 2:]            # 남한, 북한 발전량 합계 데이터만 추출
df_ns.index = ['South','North']        # 행 인덱스 변경hnn
df_ns.columns = df_ns.columns.map(int) # 열 이름의 자료형을 정수형으로 변경
print(df_ns.head())
print('\n')

# 선 그래프 그리기
df_ns.plot()

# 행, 열 전치하여 다시 그리기
tdf_ns = df_ns.T
print(tdf_ns.head())
print('\n')
tdf_ns.plot()
```


```python
# 예제 3-5
import pandas as pd

df = pd.read_excel('./data/남북한발전전력량.xlsx')  # 데이터프레임 변환 

df_ns = df.iloc[[0, 5], 3:]            # 남한, 북한 발전량 합계 데이터만 추출
df_ns.index = ['South','North']        # 행 인덱스 변경
df_ns.columns = df_ns.columns.map(int) # 열 이름의 자료형을 정수형으로 변경

# 행, 열 전치하여 막대 그래프 그리기
tdf_ns = df_ns.T
print(tdf_ns.head())
print('\n')
tdf_ns.plot(kind='bar')
tdf_ns.plot(kind='area')
tdf_ns.plot(x='South',y='North', kind='scatter')
```


```python
# 예제 3-6
import pandas as pd

df = pd.read_excel('./data/남북한발전전력량.xlsx')  # 데이터프레임 변환 

df_ns = df.iloc[[0, 5], 3:]            # 남한, 북한 발전량 합계 데이터만 추출
df_ns.index = ['South','North']        # 행 인덱스 변경
df_ns.columns = df_ns.columns.map(int) # 열 이름의 자료형을 정수형으로 변경

# 행, 열 전치하여 히스토그램 그리기
tdf_ns = df_ns.T
tdf_ns.plot(kind='hist')
```


```python
# 예제 3-7
import pandas as pd

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name']

# 2개의 열을 선택하여 산점도 그리기
df.plot(x='weight',y='mpg', kind='scatter')
```


```python
# 예제 3-8
import pandas as pd

# read_csv() 함수로 df 생성
df = pd.read_csv('./data/auto-mpg.csv', header=None)

# 열 이름을 지정
df.columns = ['mpg','cylinders','displacement','horsepower','weight',
              'acceleration','model year','origin','name']

# 열을 선택하여 박스 플롯 그리기
df[['mpg','cylinders']].plot(kind='box')
```


```python
data = {
    'name':['둘리', '또치', '도우너', '희동이'],
    '국어':[90, 80, 70, 70],
    '영어':[99, 98, 97, 46],
    '수학':[90, 70, 70, 60],
}
df = pd.DataFrame(data)
display(df)
df.set_index('name', inplace=True)
display(df)
```


```python
from matplotlib import font_manager, rc
font_path = "data/malgun.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
df.plot()
```


```python
display(df.T)
df.T.plot()
```


```python
df.plot(kind='bar')
```


```python
df.plot(kind='bar', stacked=True)
df.T.plot(kind='bar', stacked=True)
```


```python
df.plot(kind='barh')
df.T.plot(kind='barh')
```


```python
df.plot(kind='box')
df.T.plot(kind='box')
```


```python
df.plot(kind='pie',y='국어')
```


```python
df.plot(kind='pie',y='영어')
```


```python
df.plot(kind='pie',y='수학')
```


```python
sr = pd.Series([10, 35, 20, 15, 30], index=['둘리', '도우너', '또치', '희동이', '마이콜'])
sr.plot()
```


```python
sr.plot(kind='bar')
```


```python
sr.plot(kind='barh')
```


```python
r=sr.plot(kind='box')
r.set_xticklabels(['둘리,도우너,또치,희동이,마이콜의 점수'])
import matplotlib.pyplot as plt
plt.savefig('./output/test.png')


```


```python
sr.plot(kind='box')
```



### - 실습

```python
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns

# matplotlib 한글 폰트 오류 문제 해결
from matplotlib import font_manager, rc
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

df = pd.read_csv('./data/cctv_seoul.csv', index_col=None)
# display(df.head())
df.set_index('구별', inplace=True)
# display(df.head())
df_cctv = df['CCTV수']
# display(df_cctv.head())
print(type(df_cctv))

cctvColors = sns.color_palette('hls', len(df_cctv))
df_cctv.plot(kind='barh', color=cctvColors, width=0.7, figsize=(10, 13), alpha=.7, grid=True)

plt.title('시각화 과제(1) 각 국의 CCTV설치 현황', size=20)
plt.xlabel('각 구에 설치된 CCTV 댓수', size=17)
plt.ylabel('구이름', size=17)
# plt.grid(True, color='grey', linestyle='-')
plt.savefig("output/hw1.png")   
plt.show()


df_cctv2 = df_cctv.sort_values(ascending=False)
df_cctv2 = df_cctv2.T
cctvColors2 = sns.color_palette('PRGn', len(df_cctv2))
df_cctv2.plot(kind='bar', color=cctvColors2, width=0.7, figsize=(15, 10), alpha=.7)

plt.title('시각화 과제(2) 각 국의 CCTV설치 현황', size=20)
plt.ylabel('각 구에 설치된 CCTV 댓수', size=17)
plt.xlabel('구이름', size=17)
plt.grid(True, color='grey', linestyle='-')
plt.xticks(rotation=25)
plt.savefig("output/hw2.png")   
plt.show()



cctvColors2 = sns.color_palette('PRGn', len(df_cctv2))
plt.figure(figsize=(15,10))
plt.bar(x=df_cctv2.index, height=df_cctv2, color=cctvColors2, width=0.7,  alpha=.7)

plt.title('시각화 과제(3) 각 국의 CCTV설치 현황', size=20)
plt.ylabel('각 구에 설치된 CCTV 댓수', size=17)
plt.xlabel('구이름', size=17)
plt.grid(True, color='grey', linestyle='-')
plt.xticks(rotation=25)
plt.savefig("output/hw3.png")   
plt.show()
```



```python
import pandas as pd
#from matplotlib import pyplot as plt
import seaborn as sns

# matplotlib 한글 폰트 오류 문제 해결
from matplotlib import font_manager, rc
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

df = pd.read_csv('./data/cctv_seoul.csv', index_col=None)
# display(df.head())
df.set_index('구별', inplace=True)
# display(df.head())
df_cctv = df['CCTV수']
# display(df_cctv.head())


cctvColors = sns.color_palette('hls', len(df_cctv))
# df_cctv.plot(kind='line', figsize=(10, 13))
# df_cctv.plot(kind='bar', figsize=(10, 13))
# df_cctv.plot(kind='barh', figsize=(10, 13))
# df_cctv.plot(kind='box', figsize=(10, 13))
# df_cctv.plot(kind='kde', figsize=(10, 13))
# df_cctv.plot(kind='area', figsize=(10, 13))
# df_cctv.plot(kind='pie', figsize=(10, 13))

plt.title('시각화 과제(1) 각 국의 CCTV설치 현황', size=20)
plt.xlabel('각 구에 설치된 CCTV 댓수', size=17)
plt.ylabel('구이름', size=17)
plt.grid(True, color='grey', linestyle='-')
plt.savefig("output/hw1.png")   
plt.show()

```

